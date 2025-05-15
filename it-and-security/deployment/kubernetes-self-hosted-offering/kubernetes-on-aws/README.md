# Kubernetes on AWS

## Context

The purpose of this page is to describe how to create the necessary infrastructure to deploy Vectice on a Kubernetes cluster in AWS, followed by instructions to deploy the Vectice software

## 1. Understanding prerequisites

### Infrastructure requirements

| #                         | Requirement        | Notes or Details                                                                     |
| ------------------------- | ------------------ | ------------------------------------------------------------------------------------ |
| Note: Within the same VPC |                    |                                                                                      |
| 1                         | Security Groups    | <p>Port 443 (HTTPS)</p><p>3128 Outbound (pip install)</p><p>SMTP Port (e.g 2525)</p> |
| 2                         | Kubernetes Cluster | <p>v1.16+ deployed</p><p>2 nodes with t3.xlarge</p>                                  |
| 3                         | S3 Bucket          | In the same region                                                                   |
| 4                         | Managed PostgreSQL | 13.x RDS instance                                                                    |

### Other requirements

| #                                                | Requirement     | Notes or Details                                                                                        |
| ------------------------------------------------ | --------------- | ------------------------------------------------------------------------------------------------------- |
| 5                                                | Domain Name     | Example: https://vectice.my-company.com                                                                 |
| 6                                                | SSL Certificate | <p>Must be associated with the domain name above</p><p>Self-signed certificates are not recommended</p> |
| Deployment environment with the following tools: |                 |                                                                                                         |
| 7                                                | Helm v3         | [Installation Guide](https://helm.sh/docs/intro/install/)                                               |
| 8                                                | Kubectl         | [Installation Guide](https://kubernetes.io/docs/tasks/tools/)                                           |
| 9                                                | AWS CLI         | [Installation Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)     |
| 10                                               | Eksctl          | [Installation Guide](https://github.com/eksctl-io/eksctl/blob/main/README.md#installation)              |
| 11                                               | Openssl         | [Installation Guide](https://wiki.openssl.org/index.php/Binaries)                                       |

## 2. How to provision the infrastructure

You have two ways to create the infrastructure necessary for running Vectice.

### Provisioning via Terraform (with Terragrunt Wrapper)

* Expected Time: 40 minutes
* Steps:
  * Complete instructions, including the Terraform script, are found in the package your Vectice account team provided you. Contact [support@vectice.com](mailto:support@vectice.com) if you require assistance.

### Provisioning via AWS console

* Expected Time: 2 hours
* Steps:
  * Create a VPC, or reuse an existing one
  * PostgreSQL Instance creation, see [Appendix 1: Creating the SQL Instance ](appendices.md#appendix-1-creating-the-parameter-group-and-sql-instance)
  * IAM roles and Bucket creation, see [Appendix 2: Creating the S3 Bucket](appendices.md#appendix-2-create-iam-roles-for-eks-and-bucket)
  * Kubernetes cluster creation, see[ Appendix 3: Cluster Creation](appendices.md#appendix-3-creating-the-kubernetes-cluster)
  * Tag the VPC subnets for the Load Balancer, see [AWS Guide](https://repost.aws/knowledge-center/eks-vpc-subnet-discovery)

## 3. How to deploy the Vectice application

The provisioning of Vectice on Kubernetes will happen in 6 steps:

* [Step 1](./#step-1-connect-to-the-cluster-and-create-the-vectice-namespace): Connect to the cluster and create the Vectice namespace
* [Step 2](./#step-2-install-the-aws-application-load-balancer-alb): Install the AWS Application Load Balancer (ALB)
* [Step 3](./#step-3-create-postgresql-databases): Create PostgreSQL databases
* [Step 4](./#step-4-install-the-cert-manager): Install the Cert Manager
* [Step 5](./#step-5-create-secrets-for-ingress-and-docker-image-retriever): Create secrets for Ingress and Docker image retriever
* [Step 6](./#step-6-install-the-vectice-stack): Install the Vectice stack&#x20;

For any questions or assistance with deployment, please reach out to [support@vectice.com](mailto:support@vectice.com)

***

### Step 1: Connect to the cluster and create the Vectice namespace 

First, define the variables for the next steps and retrieve connections from your deployment machine. Below, sample values are provided between brackets:

```bash
CONTEXT=<arn:aws:eks:us-west-1:023286044634:cluster/vectice-cluster>
REGION=<us-west-1>
CLUSTER_NAME=<vectice-cluster>
ID_ACCOUNT=<0232860634>
VPC_ID=<vpc-z4564rfgre46>
aws eks --region $REGION update-kubeconfig --name $CLUSTER_NAME
```

The expected output should look like this:

```
Updated context arn:aws:eks:us-west-1:0232860634:cluster/vectice-cluster in /home/wsl/.kube/config
```

Next, test the connection:

```bash
kubectl --context $CONTEXT get namespaces
```

The expected output should look like this:

```bash
NAME              STATUS   AGE
default           Active   3h54m
kube-node-lease   Active   3h54m
kube-public       Active   3h54m
kube-system       Active   3h54m

```

Finally, create the Vectice namespace where applications will be deployed:

```bash
kubectl --context $CONTEXT create namespace vectice
```

### Step 2: Install the AWS Application Load Balancer (ALB)

{% hint style="info" %}
For further reference please see the [AWS Guide to Installing the Load Balancer Controller](https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html)
{% endhint %}

First, download the ALB policy:

```bash
curl -o iam_policy.json https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.11.0/docs/install/iam_policy.json
```

Then, create the ALB policy:

```bash
aws iam create-policy \
--policy-name AWSLoadBalancerControllerIAMPolicy \
--policy-document file://iam_policy.json
```

Next, associate the OIDC provider to the cluster:

```bash
eksctl utils associate-iam-oidc-provider --region=$REGION --cluster=$CLUSTER_NAME --approve
```

If a Service account already exists, update it accordingly:

```bash
eksctl update iamserviceaccount \
--cluster=$CLUSTER_NAME \
--namespace=kube-system \
--name=aws-load-balancer-controller \
--region=$REGION \
--attach-policy-arn=arn:aws:iam::$ID_ACCOUNT:policy/AWSLoadBalancerControllerIAMPolicy \
--approve
```

Otherwise, create a Service account associated with the Load Balancer Policy:

```bash
eksctl create iamserviceaccount \
--cluster=$CLUSTER_NAME  \
--namespace=kube-system \
--name=aws-load-balancer-controller \
--region=$REGION \
--attach-policy-arn=arn:aws:iam::$ID_ACCOUNT:policy/AWSLoadBalancerControllerIAMPolicy \
--override-existing-serviceaccounts \
--approve
```

\
Check if the Service account was really created:

```bash
kubectl --context $CONTEXT -n kube-system get serviceaccount | grep aws
```

The expected output should look like this:

```bash
aws-cloud-provider                     0         24m
aws-load-balancer-controller           0         50s
aws-node                               0         23m
```

If the `aws-load-balancer-controller` item is not on the output list, delete the ghost service account:

```bash
eksctl delete iamserviceaccount --cluster=$CLUSTER_NAME  --namespace=kube-system --name=aws-load-balancer-controller --region $REGION
```

\
The expected output should look like this:

```
2023-10-31 18:58:05 [ℹ]  1 iamserviceaccount (kube-system/aws-load-balancer-controller) was included (based on the include/exclude rules)
2023-10-31 18:58:06 [ℹ]  1 task: { 
    2 sequential sub-tasks: { 
        delete IAM role for serviceaccount "kube-system/aws-load-balancer-controller" [async],
        delete serviceaccount "kube-system/aws-load-balancer-controller",
    } }2023-10-31 18:58:06 [ℹ]  will delete stack "eksctl-vectice-cluster-addon-iamserviceaccount-kube-sy
And recreate it with the create command previously given.
```

Next, install the load balancer with Helm, then add the Helm repository to the repository list:

```bash
helm  --kube-context $CONTEXT repo add eks https://aws.github.io/eks-charts
helm --kube-context $CONTEXT repo update
```

Deploy the AWS helm chart on the cluster:

<pre class="language-bash"><code class="lang-bash">helm --kube-context $CONTEXT install aws-load-balancer-controller eks/aws-load-balancer-controller \
  -n kube-system \
  --set clusterName=$CLUSTER_NAME \
  --set serviceAccount.create=false \
  --set serviceAccount.name=aws-load-balancer-controller \
<strong>  --set region=$REGION \
</strong><strong>  --set vpcId=$VPC_ID
</strong>
</code></pre>

Finally, verify that the controller is installed:

```bash
kubectl --context $CONTEXT get deployment -n kube-system aws-load-balancer-controller

```

The expected output should look like this:

```
NAME                           READY   UP-TO-DATE   AVAILABLE   AGE
aws-load-balancer-controller   2/2     2            2           84s
```

### Step 3: Create PostgreSQL databases

Follow the instructions in [Appendix 4](appendices.md#appendix-4-creating-the-databases-from-the-kubernetes-cluster) to create the databases on the RDS instance. This creates a temporary deployment, connecting to a Kubernetes pod with PSQL installed.

Run commands to create the databases “vectice” and “keycloak.” Once it’s done, the temporary deployment can be deleted.

***

### Step 4: Install the Cert Manager

Next, install the cert-manager and cert-manager-csi-driver applications on the cluster.

{% hint style="info" %}
Cert-manager is used to implement SSL for internal communication between Vectice pods, Cert-manager-csi-driver will attach a csi volume containing the certificates to the Vectice pods
{% endhint %}

```bash
helm --kube-context $CONTEXT repo add jetstack https://charts.jetstack.io
helm --kube-context $CONTEXT repo update
helm --kube-context $CONTEXT install cert-manager jetstack/cert-manager -n cert-manager --create-namespace --set crds.enabled=true
helm --kube-context $CONTEXT install cert-manager-csi-driver jetstack/cert-manager-csi-driver --create-namespace -n cert-manager
```

Next, generate a custom Certificate Authority and create its associated secret:

```bash
openssl req -x509 -nodes -newkey rsa:4096 -days 3650 -keyout /tmp/ca.key -out /tmp/ca.crt -subj '/CN=vectice-internal-ca' -addext "keyUsage = keyCertSign"
kubectl --context $CONTEXT create secret tls vectice-internal-ca -n vectice --cert=/tmp/ca.crt --key=/tmp/ca.key
```

### Step 5: Create Secrets for Ingress and Docker image retriever

First, create a self-signed certificate using the following command, replacing the item highlighted with your own Common Name (CN). Below are sample values:

```bash
CNVALUE=<vectice.my-company.com>
openssl req -x509 -nodes -newkey rsa:2048 -days 3650 -keyout /tmp/vectice-cert.key -out /tmp/vectice-cert.crt -subj "/CN=$CNVALUE"
```

Then, use the command below to install your certificates in the cluster:

```bash
kubectl --context $CONTEXT create secret tls vectice-private-https -n vectice --cert=/tmp/vectice-cert.crt --key=/tmp/vectice-cert.key
```

Next, import the certificate into Amazon Certificate Manager, and copy the Amazon Resource Name (ARN) to reference it later:

```bash
aws acm import-certificate --certificate fileb:///tmp/vectice-cert.crt  --private-key fileb:///tmp/vectice-cert.key --region $REGION
```

The expected output should look like this:

```
CertificateArn: arn:aws:acm:us-west-1:023286044634:certificate/599df091-8579-4bca-9388-f192341
```

To deploy the software, you can retrieve the necessary Docker images directly from the Vectice Registry. Alternatively, if you prefer, we can provide the images via an alternative delivery method that would be defined together.\
\
If your Kubernetes cluster is configured to pull images directly from the Vectice Registry, navigate to the location of the “vectice-image-puller.json” file. This is found in the package your Vectice account team provided you. Contact [support@vectice.com](mailto:support@vectice.com) if you require assistance. Use this file to create the secret that will be used to pull the docker images from the Vectice GAR registry.

```bash
kubectl --context $CONTEXT create secret docker-registry vectice-gar-secrets -n vectice \
--docker-server=https://us-docker.pkg.dev \
--docker-username=_json_key \
--docker-password="$(cat vectice-image-puller.json)" \
--docker-email=$(cat vectice-image-puller.json | grep "client_email" | cut -d '"' -f 4)
```

### Step 6: Install the Vectice Stack

\
From the package your account team provided, untar helm vectice chart and create `myvalues.yml` from `values.yml file`. Below, sample values are provided between brackets:

{% hint style="info" %}
Please refer to the [configuration page](../configuration.md) and comments inside the file `myvalues.yaml` to customize values.
{% endhint %}

```bash
VERSION=<241.1.0>
tar -xvf vectice-$VERSION.tgz
cd vectice-$VERSION
cp values.yaml myvalues.yaml

```

Next, fill in the values in `myvalues.yaml` according to your environment deployment, and deploy Vectice global objects using Helm:

```bash
cd ..
helm --kube-context $CONTEXT upgrade --install vectice vectice -f vectice/myvalues.yaml -n vectice --create-namespace --wait 
```

Once this is done, retrieve the Vectice ingress CNAME. <mark style="color:orange;">Note:</mark> this might take up to 5 minutes to appear

```bash
kubectl --context $CONTEXT get ingress vectice -n vectice 
```

The expected output should look like this, below are example values:

```
NAME     CLASS HOSTS                    ADDRESS                          PORTS    AGE
vectice  alb   vectice.my-company.com   lb.us-west-1.elb.amazonaws.com   80, 443  1d
```

Finally, add the CNAME as a new entry in your DNS resolver.

{% hint style="info" %}
Learn more about [CNAME DNS records](https://www.cloudflare.com/learning/dns/dns-records/dns-cname-record/).
{% endhint %}

In this example, the CNAME record would look like below.

```
DOMAIN             RECORD TYPE     NAME        CONTENT
my-company.com     CNAME           vectice     lb.us-west-1.elb.amazonaws.com
```
