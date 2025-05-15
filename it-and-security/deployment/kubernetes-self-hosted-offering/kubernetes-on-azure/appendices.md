# Appendices

## Appendix 1: Creating the Cloud SQL instance and the two databases

Here we have the instructions for creating the Cloud SQL Instance with PostgreSQL 13.X and the two databases necessary: keycloak and vectice.&#x20;

First, go the menu “Azure Database for PostgreSQL flexible servers” and Press “Create”.

<figure><img src="https://lh7-us.googleusercontent.com/wdHqUVEK0vxwRDiLFiGKkb6DGyU66Bkdk_PauuIBtg0HtTimTtwpgNIs7cO56_wvJajQuAW89TpN05k-BNkm7CbgLcHFvJVxTj19nxYzV9TCrM4D6nmgmJm6n6BOd4E_8ID8n4VheGm9HqEMMjHbhi0" alt=""><figcaption></figcaption></figure>

You can then choose the resource group, which will also include the AKS Cluster and the Storage Account. Choose **PostgreSQL 13**. Then select **Press Next: Networking >**.

<figure><img src="https://lh7-us.googleusercontent.com/E7ooyrAGG5MN1AVi9I0sp-MpDxp3NgCQu0y9t9M63plgtDFR6kTwhTB7hkw9dA1Yxcs5vInkNYXH3hqssGkmNCAxU97t6ennfAW_oj6aVAMK0Q-5dA_KE1bLhYeuYTERjSWT05zIxtmELGzsB2b-SKE" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/SYZHa450EJ29FgcChlBG9WJUZCsgmGFTHHzvXel5JQJsGJKsWCO5fJUpQdjCkKSvJ8lqIMsUOs4FPtEjCLvgMpxmBZpzTOyGB7o-31WSbFTOgzduc6JBM1V7usb-Lf3iSYW39KLWIrkQeSVU1VYRGUc" alt=""><figcaption></figcaption></figure>

We can use Private Access for the Networking part, as it’s more secure.

<figure><img src="https://lh7-us.googleusercontent.com/GHjUPhkgrKIYIKKcTHhjGriAORUMEgOX0R2xrhG2f3dvmufAH3pgUiS58Z4aq6qkojBFdc1KUb59SqcaJU7_JQkYoOtU9Ng5yP_Pwue9GPLhDykEvapWDSmXnEr-u52wlHOAa7lsaBfWdGfuR-bulOI" alt=""><figcaption></figcaption></figure>

We’ll have a dedicated VNet for the PostgreSQL instance that will be created along with the instance.\
It will also create a dedicated Private DNS zone. For the pods to communicate with the SQL instance, we’ll perform two more actions:

1. Create a Peering between the AKS VNet and the PostgreSQL VNet
2. Create a Virtual Network Link from the Private DNS Zone to the AKS VNet

<figure><img src="https://lh7-us.googleusercontent.com/WV3FXg_bie3NQ6mGPMKuc1_HNecOdbgWWAklX5SNA2lVNE6RYZswmSzGu8GVkTZKrHhYU4eqF_GIJPT0JuuvJLPkIb4HuM59Nsu-YtAhC_KP1TBCaX91t27ipTqPq8cjAB0BXcrO3-qzdX4MO2VtvWw" alt=""><figcaption></figcaption></figure>



You can select the button “Review + Create” and create the SQL Instance.&#x20;

Then create the two databases (vectice and keycloak) from the menu “Databases”, CREATE DATABASE, create vectice, then redo the operation for keycloak\


<figure><img src="../../../../.gitbook/assets/image (65).png" alt=""><figcaption></figcaption></figure>

\
We will also enable the extension "UNACCENT"&#x20;

<figure><img src="../../../../.gitbook/assets/image (72).png" alt=""><figcaption></figcaption></figure>

Check in the Settings > Networking menu that Server CA is required, here are the links from offical documentation to retrieve them.&#x20;

* [Microsoft RSA Root CA 2017](https://www.microsoft.com/pkiops/certs/Microsoft%20RSA%20Root%20Certificate%20Authority%202017.crt)
* [DigiCert Global Root G2](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem)
* [Digicert Global Root CA](https://cacerts.digicert.com/DigiCertGlobalRootCA.crt)

Once downloaded, you need to format them in pem format, using the command below, a default value is proposed in the myvalues file, already encoded in base64.

```
openssl x509 -inform DER -in certificate_downloaded.crt -out certificate.pem -outform PEM
```

## Appendix 2: Creating the Kubernetes Cluster

### Cluster creation

Follow the steps in the console, like in the screenshots below.



<figure><img src="../../../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (69).png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/yItpwctzDKC8kGhxMaCnfuw4n-gzd5FxzM-kba96_u0YBjum3cXq3rDbuZNwJmqieqI16LApf2dbsVzywWgtZXjmJtgOQ60KJK_ObuDsbXxueCULCiOV74nNQHIA8IVilxgH03WGIOAQDDUwFx4CjL0" alt=""><figcaption></figcaption></figure>

## Appendix 3: Create Azure Blob Storage and access

Here are the instructions for creating the storage account, the container blob storage, and the service principals to get access to the container.\
\
The service principals will have permission to read/write the container blob storage. The Bucket is used for storing asset metadata from Models, Datasets, Notes, and Graphs.

### Storage account Creation

First, create a storage account. Go to the “Storage accounts” menu and press Create.

Then fill in the fields and make sure to set it in the same resource group as the AKS Cluster and the Azure PostgreSQL instance in the same Region.

<figure><img src="https://lh7-us.googleusercontent.com/VJwCX9b3BoWvxN-DnTnQi4jVp07F6Scleg_8NYqU5rdqO70timF5-rGoXoY1i-8hFBl_Cgf9hc063puG7R-IMN2O82PDUzdiWDjI5tmEUQ-W4XJPGlWrVKImboa4DUlWC-ZVzs4sHWd1-j2I0iVX-gw" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/izGbN9S4j6dHc9X94QhoABdKGeFv8uGDATzejrH5Hdw8KAhpOP_wFL-HvfcYGKSozICf45daCYEzgPwxLO8vPPFRVgQCa-Jovium_DFJutoIWMQIAcWJnBGdpucXa8ON50BlUK-cWkYx_BmJqqOG_9E" alt=""><figcaption></figcaption></figure>

In the Networking part, we select the AKS VNet, so that the content of the storage account can be accessed from the AKS Cluster.

<figure><img src="https://lh7-us.googleusercontent.com/6N1P5fKOtPttFQGVK9EEsdlGPBGSOg_dtsrRSKr9ZSzpIDtfJRJumVqtWytOLn7If0JW8DQohBLIwwHGE8nDGwzkVIzfgv37S0RFVpBFefCdUVmp-A-O4HR1aIgo-3HaEIyuXiJlLo2B5hyQQO0FMKI" alt=""><figcaption></figcaption></figure>

### Blob storage container creation

Create the container within the storage account:

<figure><img src="https://lh7-us.googleusercontent.com/QYao6AzaRDzv_yxCT9HuOIA9GXU71OQ8qU81IepI0otzUM9pTRlD6T206bwzCVBM1SnVJnj6bU9qnBFtHHNj8PwwmIzWD4khOBZSLYY6xTaJff7xnYxnqtZi_qp_1R-yctpg0Uuz54OwHAISuRU9H3E" alt=""><figcaption></figcaption></figure>

### Creating the Service Principal

First, create a Service Principal. To do so, go to “Azure Active Directory”, then the “App registration” menu, and press “New registration”:

<figure><img src="https://lh7-us.googleusercontent.com/lybkf4HQEyLITvO0PaFqeIiHYgkX-IA22wuVb5PFiON-8lq3ao-VB4gCKs1ejW5JaPmBCB4uFFOAa3Q8nAtiB87-WoLzP_I8E__YYGVIb1ws28TuSDlwsE8whDrDtF--PRapb5_z1yRNBahlK6ipdhk" alt=""><figcaption></figcaption></figure>

Then, name the Service Principal and Register it.

<figure><img src="https://lh7-us.googleusercontent.com/KgzkpTxYjXKAXSzu18KjUAz4xpBUZOYE1X3YB0koYBXi35dM-8AhXb-ntyMNik1mHoMtjffkLnaw3bA6CL3PfPKsx-xInKrnMrNikZz-ej32huihx9gz8K9pMsUI56RTShQEOXAF539rR7zAQMfMiKc" alt=""><figcaption></figcaption></figure>

After that, create a secret for the Service Principal:

<figure><img src="https://lh7-us.googleusercontent.com/1qtzq6lEq0Y78JPuttLkArlvDhnmKUsJQVajk9wu2YnJgW2PfylHZ5wxOeZ0H_uvicmA8Lar0WxebALzOKSDAO9vnstkHkUmcptQGIlogrkVpFPvP9DdUwnFkRZT3oE_iMzSVSOaLJfdThx8PmdxwLQ" alt=""><figcaption></figcaption></figure>

We then retrieve the value of the secret now, because after that, the content of the value will not be visible.

<figure><img src="https://lh7-us.googleusercontent.com/SQ1vI8RayRGzg3TJVauVITGHpyxEnpDaZzEb_0e6SUEXZ-369oJA3V-7d17-IosjgIZQkEejBE7Qag3QYQcycuHfensMDjXnwY1aTlkIBgoK6u53w-qf4p1tgx3eWfRgtIKhbmDJsTvkBONV37dv9mQ" alt=""><figcaption></figcaption></figure>

Retrieve the values of the Application (client) ID and Directory (tenant) ID.\


<figure><img src="https://lh7-us.googleusercontent.com/0lrxCP05L8rh4Sf_8noFbELDh6YMZox4_qOQNKGnmcA_tOSbtnDj2WEIA47f3_dTWgghYC1ftaV7y0cqUGCljC8uqMILBsaNau3WiG0Zw6teZHGMQ8TaPB60__UGuvOjYXxISEBwOoz6JBSb5Q7JupI" alt=""><figcaption></figcaption></figure>

Come back to the storage account previously created, in order to grant the Service Principal access to the Container.

Go to the Access Control (IAM) menu, and in the “Role assignment” tab, Click on Add, Add role assignment.

Set the role “Storage Blob Data Contributor”, and click on Next to define the members:

<figure><img src="https://lh7-us.googleusercontent.com/sSTZ6ppcdzNWNaPHik8UcGeG9uEAEpNKY3tcIdIQSQWyBPuNRaWDA1DTYwyVrg66JnW9fskDQ_2Z1fZsIZyJAfvdCF3pIa33THa97ULqNGZZ8ZUhercr9KhOE9_4izFBwZoPV8HcAXgfBcMGcQBI1DY" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/GsRPqaUjqmgWLCR0Cp_pX02fVDs2bCVtBDXPd3NNkXGuMs26m108cbQPOuzPRvYTWkN4K20-rcYcAwKzQ70GFNdrlmaMsbj2ycJpI0n2yHCCmtz9AwbEszStNwuniNAu43mWjbeRHwHFQcFWuOLpii0" alt=""><figcaption></figcaption></figure>

Select the Service Principal created earlier:

<figure><img src="https://lh7-us.googleusercontent.com/eZUrXrYzGzsYjr9SaVcEpm-cO6rkOJ6Zq5FcOK2pkqQedJvZNOLNVHO0NsN2Dl9S3uhWj6P0nULfJQeTjSJ8-uDJMoNO3HRp6Og5d5hskMQtFAsyOmQFOleZkGeShDIxrKnCvgeAIvS2ZWzq2rBDOR4" alt=""><figcaption></figcaption></figure>

Review and assign the role.



## Appendix 4: Creating the network links between the SQL Instance and the AKS Cluster

### Virtual network link creation

On the Private DNS Zone created along with the SQL instance, go to the “Virtual network links” menu, and press **Add**:

<figure><img src="https://lh7-us.googleusercontent.com/uSxJScg0po9rVWpWpKw_hNUl2pluMFh0HQ3aVFV2Krqw33g7XyEsR8wya7IibIMsdu6fJp3QpyAaRbnOpEr036TME79uq-MkkjIsHZ4HXaFUSs8cW55R8JHdXP-GyJZEGM87i__fezyDukGU2ZZjMCQ" alt=""><figcaption></figcaption></figure>

Add the link between the Private DNS Zone and the AKS VNet, and enable auto-registration:

<figure><img src="https://lh7-us.googleusercontent.com/PhHPftunt6V0bA9XRpB-og-dPrDX2In0TqTVPzxk-p1AXBk1SQE13PX4DoWm0koiC3zgjsbtjsC7UbJW5FiXRlSENAp0EmciSX4w27egOKDSfb-nVamO7iXZbOxGbDLEZh0bCTK_3X7AX4ZI_D93QiM" alt=""><figcaption></figcaption></figure>

### VNet Peering

Create the VNet Peering between the PostgreSQL VNet and the AKS VNet.\
To do so, go to the “Virtual Networks” menu and Click on the AKS VNet

Proceed to the peering of the 2 VNets:

<figure><img src="../../../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

## Appendix 5: Disaster recovery plan

{% hint style="info" %}
Learn more about our [data storage](../../../security/data-storage-security.md) and [backup policies](appendices.md#backup-strategy).
{% endhint %}

### Backup strategy

As there is no persistent data on the Kubernetes Cluster, no backup of the Cluster is necessary. At the minimum, we recommend a daily Backup of the Azure Blob Storage Container and the Cloud SQL instance.

The default Cloud SQL instance backup strategy is a daily backup of the whole instance. Backups can also be customized; more information can be found in this [Azure documentation](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/concepts-backup-restore).\


For the Azure Blob Storage Container, we recommend making a copy of the Azure Blob Storage Container content and placing it in another Azure Blob Storage Container in a folder named with a timestamp to create at each backup.

### Recovery Mechanism

Depending on the nature of the disaster, recovery solutions might change. In case of an infrastructure issue, please refer to the section; [Provisioning the infrastructure](./#id-2.-how-to-provision-the-infrastructure) to recreate the defaulting infrastructure elements.

\
The restoration of Bucket content consists of copying the content of the time-stamped folder described in the Backup strategy section to the application Azure Blob Storage Container on which the helm vectice configuration aims at. The restoration of the Cloud SQL instance consists of restoring the database backup following the [Azure documentation](https://learn.microsoft.com/en-us/azure/postgresql/flexible-server/concepts-backup-restore).

\
If the issue requires the creation of a new Kubernetes Cluster, for example, in a new region, please refer to the section: [Application deployment](./#id-3.-how-to-deploy-the-vectice-application) to redeploy the software. Make sure to fill in the values according to your new environment deployment.
