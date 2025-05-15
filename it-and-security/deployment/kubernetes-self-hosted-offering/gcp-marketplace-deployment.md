---
description: Deploy Vectice with on Google Kubernetes Engine (GKE) using GCP Marketplace
---

# GCP Marketplace deployment

This guide walks you through deploying Vectice's global objects as a Kubernetes application on your Google Kubernetes Engine (GKE) cluster using a pre-packaged Helm chart available in GCP Marketplace.

## Preparing the deployment from Marketplace

Please refer to the documentation [Kubernetes on GCP](kubernetes-on-gcp/) until the [cert-manager](kubernetes-on-gcp/#step-2-install-the-cert-manager) step.\
You can then follow the procedure as described below.

### Step 1: Install the Cert Manager

Next, install the cert-manager and cert-manager-csi-driver applications on the cluster.

{% hint style="info" %}
Cert-manager is used to implement SSL for internal communication between Vectice pods, Cert-manager-csi-driver will attach a CSI volume containing the certificates to the Vectice pods
{% endhint %}

```bash
helm --kube-context $CONTEXT repo add jetstack https://charts.jetstack.io 
helm --kube-context $CONTEXT repo update 
helm --kube-context $CONTEXT install cert-manager jetstack/cert-manager -n cert-manager --create-namespace --set installCRDs=true 
helm --kube-context $CONTEXT install cert-manager-csi-driver jetstack/cert-manager-csi-driver --create-namespace -n cert-manager
```

Next, generate a custom Certificate Authority and create its associated secret:

```bash
openssl req -x509 -nodes -newkey rsa:4096 -days 3650 -keyout /tmp/ca.key -out /tmp/ca.crt -subj '/CN=vectice-internal-ca' -addext "keyUsage = keyCertSign"
```

### Step 2: Create secrets for Ingress and Docker image retriever

First, create a self-signed certificate using the following command, replacing the item highlighted with your own Common Name (CN). Below, sample values are provided between brackets

```bash
CNVALUE=<vectice.my-company.com>
openssl req -x509 -nodes -newkey rsa:2048 -days 3650 -keyout /tmp/vectice-cert.key -out /tmp/vectice-cert.crt -subj "/CN=$CNVALUE"
```

Once this is done, navigate to the location of the `vectice-image-puller.json` file. This is found in the package your Vectice account team provided you. Contact [support@vectice.com](mailto:support@vectice.com) if you require assistance. Use this file to create the secret that will be used to pull the docker images from the Vectice GCR registry

```bash
kubectl --context $CONTEXT create secret docker-registry vectice-gcr-secrets -n vectice \
--docker-server=gcr.io \
--docker-username=_json_key \
--docker-password="$(cat vectice-image-puller.json)" \
--docker-email=$(cat vectice-image-puller.json | grep "client_email" | grep -Po '"client_email": "\K[^"]*')
```

### Step 3: Install the Vectice stack

Please view the [Vectice GKE deployment page](https://console.cloud.google.com/marketplace/product/vectice-public/vectice?hl=en-GB) for more information.

{% hint style="info" %}
If you already agreed to the terms and conditions, CONFIGURE will appear instead of GET STARTED and you will be redirected to the deployment form
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (62).png" alt=""><figcaption></figcaption></figure>

1. Click on **GET STARTED**
2. Agree to the terms and conditions
3. Fill in the fields in the deployment form &#x20;
4. Press **Deploy**

You should see the progress on the submenu Applications of your Kubernetes Cluster.

Once this is done, retrieve the Vectice Ingress IP. **Note**: this might take up to 5 minutes to appear:

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
