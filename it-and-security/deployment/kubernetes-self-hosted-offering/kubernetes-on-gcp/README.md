# Kubernetes on GCP

## Context

The purpose of this page is to describe how to create the necessary infrastructure to deploy Vectice on a Kubernetes cluster in GCP, followed by instructions to deploy the Vectice software

## 1. Understanding prerequisites

### Infrastructure requirements

| **#**                     | **Requirement**    | **Notes or details**                                                                 |
| ------------------------- | ------------------ | ------------------------------------------------------------------------------------ |
| Note: Within the same VPC |                    |                                                                                      |
| 1                         | Security Groups    | <p>Port 443 (HTTPS)</p><p>3128 Outbound (pip install)</p><p>SMTP Port (e.g 2525)</p> |
| 2                         | Kubernetes Cluster | <p>v1.16+ deployed</p><p>2 nodes with e2-standard-4</p>                              |
| 3                         | GCS Bucket         | In the same region                                                                   |
| 4                         | Managed PostgreSQL | 13.x Cloud SQL instance                                                              |

### Other requirements

| **#**                                            | **Requirement** | **Notes or Details**                                                                                    |
| ------------------------------------------------ | --------------- | ------------------------------------------------------------------------------------------------------- |
| 5                                                | Domain Name     | Example: https://vectice.my-company.com                                                                 |
| 6                                                | SSL Certificate | <p>Must be associated with the domain name above</p><p>Self-signed certificates are not recommended</p> |
| Deployment environment with the following tools: |                 |                                                                                                         |
| 7                                                | Helm v3         | [Installation Guide](https://helm.sh/docs/intro/install/)                                               |
| 8                                                | Kubectl         | [Installation Guide](https://kubernetes.io/docs/tasks/tools/)                                           |
| 9                                                | Gcloud          | [Installation Guide](https://cloud.google.com/sdk/docs/install)                                         |
| 10                                               | Gsutil          | [Installation Guide](https://cloud.google.com/storage/docs/gsutil_install)                              |
| 11                                               | Openssl         | [Installation Guide](https://wiki.openssl.org/index.php/Binaries)                                       |





## 2. How to provision the infrastructure

You have two ways to create the infrastructure necessary for running Vectice.

### Provisioning via Terraform (with Terragrunt wrapper)

* Expected time: 40 minutes
* Steps:
  * Complete instructions, including the Terraform script, are found in the package your Vectice account team provided you. Contact [support@vectice.com](mailto:support@vectice.com) if you require assistance.

### Provisioning via GCP console

* Expected time: 2 hours
* Steps:
  * Create a VPC, or reuse an existing one
  * PostgreSQL Instance creation, see [Appendix 1: Creating the SQL Instance ](appendices.md#appendix-1-creating-the-cloud-sql-instance-and-the-two-databases)
  * Service account role and Bucket creation, see [Appendix 2: Creating the Bucket and Service](appendices.md#appendix-2-create-bucket-and-service-account) Account
  * Kubernetes cluster creation, see [Appendix 3: Cluster Creation](appendices.md#appendix-3-creating-the-kubernetes-cluster)

## 3. How to deploy the Vectice application

The provisioning of Vectice on Kubernetes will happen in 4 steps:

* [Step 1](./#step-1-connect-to-the-cluster-and-create-the-vectice-namespace): Connect to the cluster and create the Vectice namespace
* [Step 2](./#step-2-install-the-cert-manager): Install the Cert Manager
* [Step 3](./#step-3-create-secrets-for-ingress-and-docker-image-retriever): Create secrets for Ingress and Docker image retriever
* [Step 4](./#step-4-install-the-vectice-stack): Install the Vectice stack&#x20;

\
For any questions or assistance with deployment, please reach out to [support@vectice.com](mailto:support@vectice.com)

***

### Step 1: Connect to the cluster and create the Vectice namespace

\
First, define the variables for the next steps and retrieve connections from your deployment machine. Below, sample values are provided in between brackets

```bash
ZONE=<us-west1> 
CLUSTER_NAME=<vectice-cluster> 
PROJECT=<my-project-id> 
gcloud container clusters get-credentials $CLUSTER_NAME --zone $ZONE --project $PROJECT 
CONTEXT=`kubectl config get-contexts | grep '*' | awk '{print $2}'`
```

The expected output should look like this:

```bash
# Fetching cluster endpoint and auth data.
# kubeconfig entry generated for vectice-cluster.
```

\
Next, test the connection:

```bash
kubectl --context $CONTEXT get namespaces
```

The expected output should look like this:

```
NAME              STATUS   AGE
default           Active   3h54m
kube-node-lease   Active   3h54m
kube-public       Active   3h54m
kube-system       Active   3h54m
```

\
Finally, create the Vectice namespace where applications will be deployed:

```bash
kubectl --context $CONTEXT create namespace vectice
```

### Step 2: Install the Cert Manager

Next, install the cert-manager and cert-manager-csi-driver applications on the cluster.

{% hint style="info" %}
Cert-manager is used to implement SSL for internal communication between Vectice pods, Cert-manager-csi-driver will attach a CSI volume containing the certificates to the Vectice pods
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

### Step 3: Create secrets for Ingress and Docker image retriever

First, create a self-signed certificate using the following command, replacing the item highlighted with your own Common Name (CN). Below, sample values are provided between brackets

```bash
CNVALUE=<vectice.my-company.com>
openssl req -x509 -nodes -newkey rsa:2048 -days 3650 -keyout /tmp/vectice-cert.key -out /tmp/vectice-cert.crt -subj "/CN=$CNVALUE"
```

Then, use the command below to install your certificates in the cluster

```bash
kubectl --context $CONTEXT create secret tls vectice-private-https -n vectice --cert=/tmp/vectice-cert.crt --key=/tmp/vectice-cert.key
```

\
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

### Step 4: Install the Vectice stack

\
From the package your account team provided, untar helm vectice chart and create `myvalues.yml` from `values.yml` file. Below, sample values are provided between brackets.

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

Once this is done, retrieve the Vectice Ingress IP. Note: this might take up to 5 minutes to appear:

```bash
kubectl --context $CONTEXT get ingress vectice -n vectice 
```

The expected output should look like this, below are example values:

```
NAME      CLASS    HOSTS                    ADDRESS         PORTS     AGE
vectice   <none>   vectice.my-company.com   2.3.4.5         80, 443   211d
```

Finally, add the A record as a new entry in your DNS resolver.

{% hint style="info" %}
Learn more about [A DNS records](https://www.cloudflare.com/learning/dns/dns-records/dns-a-record/).
{% endhint %}

In this example, the A record would look like below.

```
DOMAIN             RECORD TYPE     NAME        CONTENT
my-company.com     A               vectice     2.3.4.5
```
