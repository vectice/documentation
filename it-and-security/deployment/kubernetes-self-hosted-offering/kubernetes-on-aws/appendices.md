# Appendices

## Appendix 1: Creating the parameter group and SQL instance

Here are the instructions for creating the RDS PostgreSQL Instance and the necessary RDS parameters.

### Create a parameter group

To force SSL on your SSL instance, you need to use a parameter group where  `rds_force_ssl=1` and `rds.allowed_extensions = unaccent`. Type RDS in the search bar and go to the first page.\
Go into the Parameter group:

<figure><img src="https://lh7-us.googleusercontent.com/l1gixiBR312nHUYvI_B5Lyyl6KCvBB9ygitYjYXQQ79Nmu5gFAiX-7u96FHREWGE2JQZjyD7Iqv0nH88C4fGLVzBmsOBeGBjvOGUeoMFRN0HpVdAHOM7Wm-pBely1ycjfl31YfCV4iqav1bz5f2xhS8" alt=""><figcaption></figcaption></figure>

Go on `mysslparametergroup` and search `ssl` on the parameters search bar.\
We need to set `rds_force_ssl` at value 1 instead of 0. To do so, check the box, and click on Edit Parameters.

<figure><img src="https://lh7-us.googleusercontent.com/rQLCd2w0-90TxK96USMZ46FAi4oJ0c33jcpwUusrmU_5qORF_V8nV2Hc5TJRrJqhQpO_qvf6f8pN7yCFEjbCIoy0zB3hKOZL9JciC97_Ab46LHK-401XBQRM2qq776Bfd2phAYn3XU8xEbYdhd2P3mI" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/_uChY_d_Hq8jN5kmeTFowU4CGNsP5K8mcJtcTviq70aj24kIaGj9S2nn-raP6Ap9SNBdzHg0h_MxfXGUQoTEF-K9ITgfM-lvhwdJLTXdPNcU_tSV4eZzdinY3vNzPyn5P8mys2tjKndfgwsaUG0b_Vs" alt=""><figcaption></figcaption></figure>

Set the value to 1.\
Then perform the same action for `rds.allowed_extensions = unaccent`.

<figure><img src="https://lh7-us.googleusercontent.com/xLXtUT3CaIZEw0Fut3aWN_EWnIem-fP1nmgGh1GneMVkeIA8F1VsLJ50SfTETFN-29IMkTBaRF76SVhDVWuJEYwuI94jWg5Q1MQEzOh7sY49H-LCu0B4UMg5BZR2PzSR-RdNTxgCtUTBi1ykbsUXm3I" alt=""><figcaption></figcaption></figure>

Apply by clicking on “Save Changes”.

<figure><img src="https://lh7-us.googleusercontent.com/JoQTCZvewxMdnpmbeCkYj02K0rRyvKO6Db-n5nyyBsHcvSGoqIhdtQTRI7sHmtu4RjDT0GsdNIKgbAdNspga9Cw1JAfWk5GZQEJCtF-uM1sE--SxyVoLj6NqQQsVQ3R7EWWaQRJ0kQkFmRBbh79ZbI8" alt=""><figcaption></figcaption></figure>

### Create an RDS instance

To Create the RDS instance, go to the RDS menu, then press “Create database”.

<figure><img src="https://lh7-us.googleusercontent.com/ErZooqa2uopSxdkqRd87l8rJ9QpIfj_Q6y-l9-1vt-KGs-6D9p0NMyFz6Axel8oc2G-THvM7voRY06RkoUH9JaixCCx9TIEldehbkWP7X6oBI2Lgu4auiVSZGF38_IJ8C_NM0THu1Oq2F95jR1sQ3qg" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/yIAl1HYltsmhMDFya4tb_JyE6D4fMF6vf5Y9cEgi20yZNNXQe8YXT_QuM6APx2kRyvFMApBBx9s3nIPyEl1Jz_w9pFQRrC4P52eWjM9hge62McetAyNgf5IFjcw6L7i98_Oc7rmQ5qTQkjF_TrgPtJc" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/XVDMeGkepoX2_RP_BzMVopZP-E2EOGbxRyC2yPjHJzY2CunvgJOJmF7_mnSqmgfRqXmhjxAdEx7sXE7Q8FWFELBab0KM3iaYVDdvTrvI3nE4upU1X7olN8SoMbTimOALWVUm-i411FWlk1XDgFpNLlQ" alt=""><figcaption></figcaption></figure>

Assign [the parameter group previously created](appendices.md#create-a-parameter-group) to the SQL instance.

<figure><img src="https://lh7-us.googleusercontent.com/jw9EC2EdyIDlwICRQEfd1unwFcCUQqXFgm2OY2KKSaamhJoN78gf3AHuXAIlWsK2RKdw4C8fr5xNcDUkXHWjsHKF9wgHXNxSvsu_aT2-vdAKYjM5ogUGNDuxukxPrQr-Uz2-ELlYS8OdmPUgYmbe1M0" alt=""><figcaption></figcaption></figure>

## Appendix 2: Create IAM roles for EKS and Bucket

### IAM roles for EKS

Two IAM roles are used by AWS in order to manage the EKS Cluster and Cluster Resources:

1\) Cluster IAM role policies\
\
![](<../../../../.gitbook/assets/image (61).png>)\
\
2\) NodeGroup IAM role policies

![](https://lh7-us.googleusercontent.com/Tzy_YUhXUsIU10dtdlc0jOb_6nrV6SvhlHwccSQlWSD7WTshz4FSg7h1CR0_OaJo7Fn-a5R2j4dRGzQKY8V44xHSQ41C4ud3vpWALoDrdjazR2kU06ZefHRXAJY8_V9FI2aKLD_aywcvG838gJF78Fc)\
\
You can create them through the AWS Management Console:

<figure><img src="https://lh7-us.googleusercontent.com/KByWzKEeO757UYjZ38DmdyVyqoxtt9FlSQT0zXzJ9Vg5bNTSMiP3wM8tbJ6s4Ns0jC4216B3nCpoXjl3sf0COvEcLY5ORy0FR_MW3JIuQQ_0FWM9Cwm4gs2DDgL4ug2BQjZBMvmoz_6UjE03-G7gKAo" alt=""><figcaption></figcaption></figure>

### IAM role for the Bucket

IAM user credentials from the AWS project, which has permission to read/write the S3 Bucket on client Amazon S3. The Bucket stores asset metadata from Models, Datasets, Notes, and Graphs.

Create the S3 bucket. Below, sample values are provided between brackets:

```bash
aws s3 mb s3://<vectice-storage-bucket>
```

1\. Create the IAM User:

```bash
aws iam create-user \
  --user-name vectice-service-account
```

2\. Attach the Policy to the User:

```bash
aws iam attach-user-policy \
  --user-name vectice-service-account \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3FullAccess
```

3\. Create an Access Key for the User:

```bash
aws iam create-access-key \
  --user-name vectice-service-account
```

## Appendix 3: Creating the Kubernetes cluster

### Cluster creation

Follow the steps in the console, like in the screenshots below.

<figure><img src="https://lh7-us.googleusercontent.com/JQ0SNFQcfhrWDcAuV8Cx2P5_kI9WX0vmVo6TkQtuSew3ZfU_Uhr60fwdN4bCYAnn6x8ROLKXPhleZseZ1Mgn--wzcPZol1YSPaji_jDMcMpY3V8FTFepNMiTk0g8BXD2fNXsHPQN1XS7tIbilhIELTY" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/c_RWxz3CSVseuCKXyq4QBqFxn7sRf3mOjT6nrl3bOpyC1kzLoTeDGV1_H97SsBgxaSHDYlKV_16Ulw3lFrZlGrjuJDbc7rhsUtUxhqtBlf8dxLuLG8ozg9qrVQ73KxwQ2dGfM6yMb0bais4ClDGJcBM" alt=""><figcaption></figcaption></figure>

The Cluster needs the private Endpoint to connect the nodes that are created after with the node group and the Public Endpoint to connect from an outside computer.\
The Private endpoint is used to attach the nodes to the Cluster.\
The Public endpoint is used to reach the Cluster from outside the VPC.&#x20;

<figure><img src="https://lh7-us.googleusercontent.com/-T2wtCSjNgwTsla9iK34m0we6NdH42RdI458ag8FOZyt48qGx-t6jGJPtUwEZwxoDHE96_OE0aq-ab9vFBHQRqABzNrXUT_HH2Ta-wOaC2CGj3spHdDeRR8fqqCgEkD9rT_prKtXJYezfavCpk-RQSk" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/Xg2b_JAPLx_MQ1gFH-dFrHFAVzNmFLjTN7YJwnQhUed5_lXAibh66zWYciOgyqrpzYx9C673EleSKzTIvMzcCyAqwJ6xfvLoYq5tZNdrVEPbXptQ3XXkHAhHHNZG3HgFQz7Qz68GtZMxE701m1vntkw" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/QM3TZjL2Y9oa89C-p3qv6pKibR0TLgeynkVQJFLhltLxEdYvk_I9fXPNe7Iw-nN37AjJHkArGVq9IEA-Iin0RXuWCMD_3sp5VSyUTWUQELjj8d93G23OoXZC-netF_g5psgNSly4jwLCY0VYpD03cMs" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/ZiR2G8Kc-CyO6DLzECoFxcSjJM9NYsD_HizkstHZHrJVvivW9Jjvh3LyIB2If3Of26141G9Xqkjys22YJa9TnRr73d7J3v096FZy10BW_oW1RRWGdfef0JRe2WQVnD2ogoqfcTVGhKvzYoFpwuZz6AM" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/SxVAIaAWZPozTjkk-eCOAQy5_klyBGidnO2UK1sFiPXtpPreP0WVaJfK3sOMQKvo9A4k_GkLHVeQiEZLOER9LaRWCt2Zsytk2Lq0BW1XbmYSAazAzKenk5Rq_007yDfD9uCOV-p2FYcI7sYFcKdGr9U" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/I0ozxI55t23lgylwqUDC2TlLe0coSWIqgK3syrbkOmZuxCi7bWLae-SjXLB_AvTJDS66L-hfzUlRPxi_pIKlkRVhOsv7R3K7Y_9MYfF53drnYCU4YAkVW9_lsNMYfq-ytG8zlo57LfaiiAsRivaoyDw" alt=""><figcaption></figcaption></figure>

Once you select the **Create** button, the creation of the Cluster Control Plan will take about 10 minutes.&#x20;

### Node group creation

You will then need to create the Node Group, selecting how many nodes you want and with which machine type. For that, you need to go to your freshly created cluster on the AWS Management Console and Click on the Button “Add node group”.

<figure><img src="https://lh7-us.googleusercontent.com/hbyHgHxs6mx_obZ136SUiscHIg5V5MCV3OdLieN_GI7Wd3Nof70Aje5XAVSxEJJ3-ry2RBl07gU_7V0yAWrpyXKAplj1i1010Vwy4Zi9s3zPFbmxjDiHIzlKwxzHeZpIVswoGv64wmIoB09GTLNgYBA" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/n7LkiXrE8uIl8AI4vTSu7lELitMiqfHsE-JmQ8BP0x53_L1n7brjJmIncUcM4bEEAjxgU8ah-9zX4qO1mwt2EU_IXmYQvq0vZC8cdAKNZGeK1ItpQrDrNrFBgh-17eAAz1BfmX7a5FFv0VDX46eWIE0" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/p7M5K0AH2EUS3yGkJ2h60Wt5N5DRKqJrBzZtnM5PXTehQSQOhUTmm9fCe0GICI_Ddy8WzDlRh04h3eEDVEkF-JzadFse85bRrCwD0oVI9TqndurBPdnTSWlRJmYQGZf21dKIkh9mVngHRK2fNwTEJ4k" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/n7LkiXrE8uIl8AI4vTSu7lELitMiqfHsE-JmQ8BP0x53_L1n7brjJmIncUcM4bEEAjxgU8ah-9zX4qO1mwt2EU_IXmYQvq0vZC8cdAKNZGeK1ItpQrDrNrFBgh-17eAAz1BfmX7a5FFv0VDX46eWIE0" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/n7LkiXrE8uIl8AI4vTSu7lELitMiqfHsE-JmQ8BP0x53_L1n7brjJmIncUcM4bEEAjxgU8ah-9zX4qO1mwt2EU_IXmYQvq0vZC8cdAKNZGeK1ItpQrDrNrFBgh-17eAAz1BfmX7a5FFv0VDX46eWIE0" alt=""><figcaption></figcaption></figure>

## Appendix 4: Creating the databases from the Kubernetes cluster

We’ll use the image of Postgresql client from this [public repository](https://github.com/andreswebs-public-images/postgresql-client), just changing the namespace from `postgresql-client` to `vectice`.\
\
The file to deploy will be the one shown below, save it as `postgresql-client.yml`:

```yaml
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: postgresql-client
  namespace: vectice

---
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: postgresql-client
  namespace: vectice

---
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: postgresql-client
  namespace: vectice
roleRef:
  kind: Role
  name: postgresql-client
  apiGroup: rbac.authorization.k8s.io
subjects:
  - kind: ServiceAccount
    name: postgresql-client

---
apiVersion: v1
kind: Pod
metadata:
  name: postgresql-client
  namespace: vectice
  labels:
    app: postgresql-client
  annotations:
    cluster-autoscaler.kubernetes.io/safe-to-evict: "true"    
spec:
  serviceAccountName: postgresql-client
  securityContext:
    runAsNonRoot: true
    supplementalGroups: [ 10001] 
    fsGroup: 10001    
  containers:
    - name: postgresql-client
      image: andreswebs/postgresql-client
      imagePullPolicy: Always
      securityContext:
        runAsUser: 1000      
      stdin: true
      tty: true
      command: ["/bin/sh"]
```

Apply the content to create the resources we need:

```bash
kubectl --context $CONTEXT -n vectice apply -f postgresql-client.yml
kubectl --context $CONTEXT attach --namespace=vectice -ti postgresql-client
```

Enter the bash inside the postgresql-client pod, we can create the two databases, and check after the list of databases on the instance. Below, sample values are provided between brackets:

```sql
psql "host=<yourhost>  user=<master rds user> password=<yourmasterpassword> dbname=postgres"
CREATE DATABASE vectice;
CREATE DATABASE keycloak;
\l
```

Get out of the pod and delete the resources just created on the cluster:

```bash
kubectl --context $CONTEXT -n vectice delete -f postgresql-client.yml
```

## Appendix 5: Disaster recovery plan

{% hint style="info" %}
Learn more about our [data storage](../../../security/data-storage-security.md) and [backup policies](appendices.md#backup-strategy).
{% endhint %}

### Backup strategy

As there is no persistent data on the Kubernetes Cluster, no backup of the Cluster is necessary. We recommend a minimum daily Backup of the S3 Bucket and the RDS instance.

The default RDS instance backup strategy is a daily backup of the whole instance. Backups can also be customized, more information can be found on this [AWS documentation](https://aws.amazon.com/getting-started/hands-on/amazon-rds-backup-restore-using-aws-backup/?sc_icampaign=Product_Launch_m5y21_psc_core-infra_storage_rds-backup-restore_sm-cnsl\&sc_ichannel=ha\&sc_icontent=awssm-7418_pac\&sc_ioutcome=CSI_Digital_Marketing\&sc_iplace=console-rds_standard\&trk=ha_a134p0000078QrQAAU~ha_awssm-7418_pac\&trkCampaign=psc_core-infra_storage_rds-backup-restore_get-started).

For the Bucket, we recommend making a copy of the Bucket content and placing it in another Bucket, in a folder named with a timestamp to create at each backup.

### Recovery Mechanism

Depending on the nature of the disaster, recovery solutions might change. In case of an infrastructure issue, please refer to the section; [Provisioning the infrastructure ](./#id-2.-how-to-provision-the-infrastructure)to recreate the default infrastructure elements.\
\
The restoration of Bucket content consists of copying the content of the time-stamped folder described in the Backup strategy section to the application S3 Bucket on which the helm vectice configuration aims at. The restoration of the RDS instance consists of restoring the database backup following the [AWS documentation](https://aws.amazon.com/getting-started/hands-on/amazon-rds-backup-restore-using-aws-backup/?sc_icampaign=Product_Launch_m5y21_psc_core-infra_storage_rds-backup-restore_sm-cnsl\&sc_ichannel=ha\&sc_icontent=awssm-7418_pac\&sc_ioutcome=CSI_Digital_Marketing\&sc_iplace=console-rds_standard\&trk=ha_a134p0000078QrQAAU~ha_awssm-7418_pac\&trkCampaign=psc_core-infra_storage_rds-backup-restore_get-started).\
\
If the issue requires the creation of a new Kubernetes Cluster, for example, in a new region, please refer to the section: [Application deploymen](./#id-3.-how-to-deploy-the-vectice-application)t to redeploy the software. Make sure to fill in the values according to your new environment deployment. If the issue did not require the creation of a new RDS instance, the subsection[ Creation of PostgreSQL databases](./#step-3-create-postgresql-databases) can be ignored.
