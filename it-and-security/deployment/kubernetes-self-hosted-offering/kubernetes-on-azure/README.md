# Kubernetes on Azure

## Context

The purpose of this document is to describe how to create the necessary infrastructure to deploy Vectice on a Kubernetes cluster in Azure, followed by instructions to deploy the Vectice software

## Understanding prerequisites

### Infrastructure requirements

| # | Requirement                                   | Notes or Details                                                                                          |
| - | --------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| 1 | Security Groups                               | <p>Port 443 (HTTPS)</p><p>3128 Outbound (pip install)</p><p>SMTP Port (e.g 2525)</p>                      |
| 2 | Kubernetes Cluster                            | <p>v1.16+ deployed<br>agentpool: 1 node Standard_D4s_v4</p><p>userpool: 2 nodes with Standard_D4as_v4</p> |
| 3 | Azure Blob Storage Container                  | In the same region                                                                                        |
| 4 | Azure Database for PostgreSQL flexible server | 13.x Cloud SQL instance                                                                                   |

### Other requirements

| #                                                | Requirement     | Notes or Details                                                                                        |
| ------------------------------------------------ | --------------- | ------------------------------------------------------------------------------------------------------- |
| 5                                                | Domain Name     | Example: https://vectice.my-company.com                                                                 |
| 6                                                | SSL Certificate | <p>Must be associated with the domain name above</p><p>Self-signed certificates are not recommended</p> |
| Deployment environment with the following tools: |                 |                                                                                                         |
| 7                                                | Helm v3         | [Installation Guide](https://helm.sh/docs/intro/install/)                                               |
| 8                                                | Kubectl         | [Installation Guide](https://kubernetes.io/docs/tasks/tools/)                                           |
| 9                                                | Azure CLI       | [Installation Guide](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)                     |
| 11                                               | Openssl         | [Installation Guide](https://wiki.openssl.org/index.php/Binaries)                                       |

\


## 2. How to provision the infrastructure

You have two ways to create the infrastructure necessary for running Vectice.

### Provisioning via Terraform (with Terragrunt Wrapper)

* Expected Time: 40 minutes
* Steps:
  * Complete instructions, including the Terraform script, are found in the package your Vectice account team provided you. Contact [support@vectice.com](mailto:support@vectice.com) if you require assistance.

### Provisioning via Azure portal

* Expected Time: 2 hours
* Steps:
  * Create a resource group in your chosen subscription
  * PostgreSQL Instance creation, see [Appendix 1: Creating the SQL Instance ](appendices.md#appendix-1-creating-the-cloud-sql-instance-and-the-2-databases)
  * Kubernetes cluster creation, see [Appendix 2: Cluster Creation](appendices.md#appendix-2-creating-the-kubernetes-cluster)
  * Blob Storage Creation, see [Appendix 3: Creating the Blob Storage container](appendices.md#appendix-3-create-azure-blob-storage-and-access)
  * Creating network links, see [Appendix 4: Creating the network links ](appendices.md#appendix-4-creating-the-network-links-between-the-sql-instance-and-the-aks-cluster)

## 3. How to deploy the Vectice application

The provisioning of Vectice on Kubernetes will happen in 5 steps:

* [Step 1](./#step-1-connect-to-the-cluster-and-create-the-vectice-namespace): Connect to the Cluster and Create the Vectice Namespace
* [Step 2](./#step-2-install-the-cert-manager): Install the Cert Manager
* [Step 3](./#step-3-set-up-the-application-gateway-on-the-cluster): Set up the Application Gateway on the cluster
* [Step 4](./#step-4-create-secrets-for-ingress-and-docker-image-retriever): Create Secrets for Ingress and Docker Image Retriever
* [Step 5](./#step-5-install-the-vectice-stack): Install the Vectice Stack&#x20;

For any questions or assistance with deployment, please reach out to [support@vectice.com](mailto:support@vectice.com)

### Step 1: Connect to the cluster and create the Vectice namespace

First, define the variables for the next steps and retrieve connections from your deployment machine. Below, sample values are provided between brackets:

```bash
AZURE_SUBSCRIPTION=<080kkb88-bf7d-44d-b46e-3302454g5r>
CLUSTER_NAME=<vectice-cluster>
RESOURCE_GROUP=<my-resource_group>
KUBE_RESOURCE_GROUP=<kubernetes resource group>
az account set --subscription $AZURE_SUBSCRIPTION
az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME
CONTEXT=`kubectl config get-contexts | grep '*' |  grep '*' | awk '{print $2}'`
```

The expected output should look like this:

```
Merged "vectice-cluster" as current context in /home/wsl/.kube/config
```

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

Finally, create the Vectice namespace where applications will be deployed:

```bash
kubectl --context $CONTEXT create namespace vectice
```

### Step 2: Install the Cert Manager

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

### Step 3: Set up the Application Gateway on the cluster

{% hint style="info" %}
#### You can reuse an existing application gateway through the Azure portal.
{% endhint %}

To enable the AGIC add-on, go to the  [Kubernetes services ](https://portal.azure.com/?feature.aksagic=true#view/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerService%2FmanagedClusters)page and select your Cluster. Go to the Settings > Networking and Virtual Network Integration tab to find the application gateway ingress controller section. Click on the ManageCheck box next to Enable ingress controller, and Create a new Application Gateway or Select your existing one.

<figure><img src="../../../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

If you did not have an existing Application Gateway, the creation could be blocked because of a permission issue. The AG needs to create a subnet on the Vnet used by the AKS Cluster.

\
As the AG belongs to the Managed Resource Group of the AKS cluster, permission is needed to add on the Managed Identity of the AG.

\
Navigate to the AKS managed Resource group created along with the cluster and Click on the managed Identity that contains the name of your AG (it might take a few minutes to appear).

<figure><img src="../../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Navigate to the Azure role assignment menu, and add the role "Network Contributor" to the general resource group you use for the resources (not the AKS managed resource group).

<figure><img src="../../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

#### Add root-certificate to the application gateway

Once the application gateway is created, add the root certificate created at the [Step 2 ](./#step-2-install-the-cert-manager)to the application gateway.\
Below, sample values are provided between brackets.

```bash
az network application-gateway root-cert create --cert-file /tmp/ca.crt --gateway-name ingress-appgateway -n vectice-internal-ca --resource-group $KUBE_RESOURCE_GROUP
```

### Step 4: Create Secrets for Ingress and Docker Image Retriever

First, create a self-signed certificate using the following command, replacing the item highlighted with your own Common Name (CN). Below, sample values are provided between brackets.

```bash
CNVALUE=<vectice.my-company.com>
openssl req -x509 -nodes -newkey rsa:2048 -days 3650 -keyout /tmp/vectice-cert.key -out /tmp/vectice-cert.crt -subj "/CN=$CNVALUE"
```

Then, use the command below to install your certificates in the cluster

```bash
kubectl --context $CONTEXT create secret tls vectice-private-https -n vectice --cert=/tmp/vectice-cert.crt --key=/tmp/vectice-cert.key
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

### Step 5: Install the Vectice Stack

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

Next, fill in the values in `myvalues.yaml` according to your environment deployment, and deploy Vectice global objects using Helm

```bash
cd ..
helm --kube-context $CONTEXT upgrade --install vectice vectice -f vectice/myvalues.yaml -n vectice --create-namespace --wait 
```

Once this is done, retrieve the Vectice ingress IP. <mark style="color:orange;">Note:</mark> this might take up to 5 minutes to appear

```bash
kubectl --context $CONTEXT get ingress vectice -n vectice 
```

The expected output should look like this. Below are example values:

```
NAME      CLASS                      HOSTS                    ADDRESS   PORTS     AGE
vectice   azure-application-gateway  vectice.my-company.com   2.3.4.5   80, 443   1d
```

Finally, add the A record as a new entry in your DNS resolver.

{% hint style="info" %}
Learn more about [A DNS records](https://www.cloudflare.com/learning/dns/dns-records/dns-a-record/).
{% endhint %}

In this example, the A record would look like below:

```
DOMAIN             RECORD TYPE     NAME        CONTENT
my-company.com     A               vectice     2.3.4.5
```
