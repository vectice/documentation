# Appendices

## Appendix 1: Creating the Cloud SQL instance and the two databases

Find here the instructions for creating the Cloud SQL Instance with PostgreSQL 13.X and the two databases necessary: keycloak and vectice&#x20;

Type Cloud SQL in the search bar and reach the first page.\
Go to the SQL menu, and press **CREATE INSTANCE**[\
\
](https://console.cloud.google.com/sql/instances?referrer=search\&project=my-project)![](https://lh7-us.googleusercontent.com/VbQbqlfBgtGMWpzNLVs2OF9cFYioH6GaTAHmHrOGptYu3ZX65zQ5sp5iy7LGFmNgqTBOfN4pEoGiQTtyzTF-kmv6iaODoCJuY7S-VM_dKhR4Ol4haLJCQ_h0b0RtsxV0WxkXsTZlHAXQPX1Jem01u-Q)

<figure><img src="https://lh7-us.googleusercontent.com/--RFlIzOz1M0_zSg9akT68VErgNblmEc2FeLV3afKZXMmU70MS02NRdjoZiWB3uw2HkmrkbdbkvRnVAhjjcGqoVXvhNOvfXucCBaLBVaMH6T6tN782d5JDL1vSbkkwNwpM4JpqPNt3uW2qQ0GyNx5Tc" alt=""><figcaption></figcaption></figure>

We’ll then input the instance name, the master user, and password.

<figure><img src="https://lh7-us.googleusercontent.com/s6A0FwxFjkpxgFDEXAc1AhGDFqcIZhXORNdlB0P4PQsN5HlQsv0qIyUeFufyLUnAHQOJU9KYSxn1PK_oLlXM_ale5dzlufNAQUi45XLGjY17A16AvB-0e284J-B29sDHBBbfHx9NB3oz0p8k30KK2y4" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/1yOC4GUyDQBHKC2bmsMIMgkZ6wIT82ZboQtuHogtZkbGYlDzHD7nB-jKP5ea5XJ42uqwysAU-JuAE47jUdmb4ws09PNfhMioOe2IELQUMhiXyt3qEvVFrOlC9LkNU8_euz1D1gtNTWVuc3CQlFZntW0" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/DYgX9zCp_8BKZAoWVqrJNNL7mL0LMg5oLiN_wk8UjAcesVAmRLxh1e9GtPxoQwrgZHy-AO38f2_E0x1SjCHzG76HKapVlTc10FAHGY1LP3aYSCjw01gcldzGhoB_xlWyAGNMFx56fnms9sXO1LMYDlM" alt=""><figcaption></figcaption></figure>

Then, create the two databases, vectice and keycloak, from the menu “Databases,” CREATE DATABASE, create Vectice, and then redo the operation for keycloak.

## Appendix 2: Create Bucket and Service account

Find the instructions for creating the role, the service account, and the GCS Bucket.

The role will be attached to the service account to obtain permission to read/write the GCS Bucket. The Bucket is used for storing asset metadata from Models, Datasets, Notes, and Graphs.

### Bucket creation

1. Type Cloud Storage in the search bar and view the first page.
2. Go to Cloud Storage, Buckets menu, and Press **CREATE**.
3. Fill in the settings as in the screenshot below.

<figure><img src="https://lh7-us.googleusercontent.com/GarRntYB4KjH9XCSQA-yCcNQuBkL7rYL2ndh9FwoHOjwXW1HpV_ygPdZAS_uwUK3Z2YYduw3rAZnls7ZSQwuD_AOBGvK9ZpZbYNgKXe0FbyBaIrCnJE8kgsZLXkCZhx8cbVDfNUl9JuUpWZTP3VwL6Y" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/JU546k3TDznYy3yl1wlAot-03p6dq6DnBBmiExTUx4H5TP1ptH6rWWMn-Y6lQMHG1si0EUJbnM3gz4s8I2b-qryKJ0Vy_4nd5Hc1rTasyTjnY-F8qVDArdRPaCwGucdrFnkHzB42TpykZhqP_L9DCnk" alt=""><figcaption></figcaption></figure>

### IAM role creation

1. Type IAM in the search enginer.
2. Create an IAM role with the following permissions:

In this example, it will be named “bucket-storage”.

<figure><img src="https://lh7-us.googleusercontent.com/x43aW07Co0Txfknl3cMD-Lu3QUvD9CFF1KSxFUXC9oANKjz18snabzWUQN4WTpWvuuY_3qvkRLzv_e1YwsIi8EElI9B6Zc3UDZN98vmkNbU6yEo2b2twt1OE4a9lquZWkFxHV3GvZHcufUJn-yjRS8c" alt=""><figcaption></figcaption></figure>

#### Service account creation

<figure><img src="https://lh7-us.googleusercontent.com/s800dbR7xOWbjSQbaECBrKhox0pQwMRrjItq_ZmWgJdGJkUZ5Dz6em2XxI5nzIHIUAFaSGFeLruUvcj6EabzZbibBERDd1d6WQwwpoKsTGK6fU1ns7igw9zXmHfQgZoDdeese_MPCYChSe9bUcCwTmA" alt=""><figcaption></figcaption></figure>

Assign the IAM role previously created to the service account.

<figure><img src="https://lh7-us.googleusercontent.com/xQz5bEMBhLrp8TJOougv-3qIO_EmLFxwIXzuyJv8O8fpefhS6hnqTJ4OHhcMPNd5tYBK5FsG-ndAhIvI4Aa7UMPXqimUGu209xCZbpBYXQlkRcq762oG3sj3n5PETGo8VWlOmiPG2G4OYFIVj9YHP84" alt=""><figcaption></figcaption></figure>

## Appendix 3: Creating the Kubernetes cluster

### Cluster creation

Type Kubernetes Engine in the search bar and reach the first page. Then click on the **CREATE** button.

Follow the steps in the console, like in the screenshots below.

<figure><img src="https://lh7-us.googleusercontent.com/vTCb5w6ii2fevewQ1TqsCEy9lM7JHoWufzsYOA_OtqpomSqN_BqpSK4Ak9ZO4kuncQC-2khJoIZZrPIXyMqDowBR_Ef0NpgHoUxRFAenFsqh2rOSaUEyi8v-ukW5RH-t0Acrvrnv0erzfleLzmyqtgY" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/n4gMOec0AMTufanfDjsayiD12eWKSvJSvTEJhs4r0mwCgY-PPwgzvDk8tfefpqvQj4a5awmo4P3POY6XSNGLDnfyzViFeDokMxJtGYQVHUQusgwsWk1_8u155P-mlbCrrUFUsn_l-Ah_sDNf0dz73yA" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/Ouig8AbV9MxzCV_OvAfkokRtnytO_hRUl4fhclZtUtn1SrXPFQMTKpkijVWm11Y7Tmk1YKEd06O-7wsjFjwLBQvcuG4ObhgTdqh2VlOl9uHVrWHXUzoFqITj_b0y23DvMGy6LXrb8f83AYoZgyXMsGs" alt=""><figcaption></figcaption></figure>

<figure><img src="https://lh7-us.googleusercontent.com/ydQQHi1TEfti3BesYK1lr1oK5FV9rsSNumVhAY0hn2SvIFmvBB7TXQNWbdXWCi99Cnn9M_-IkEPWgEiKgmBm4Ma46nSKh-3qFy45OYR2fUwAu4UrYQPIB5sWy8UFDjdlXirs8IwYxf59P-VP9y7IKrQ" alt=""><figcaption></figcaption></figure>

Once you select the create button, the cluster creation will take about 30 minutes to build the Cluster, Control Plan, NodePool, and Nodes.

## Appendix 4: Disaster recovery plan

{% hint style="info" %}
Learn more about our [data storage](../../../security/data-storage-security.md) and [backup policies](appendices.md#backup-strategy).
{% endhint %}

### Backup strategy

As there is no persistent data on the Kubernetes Cluster, no backup of the Cluster is necessary. At the minimum, we recommend a daily Backup of the GCS Bucket and the Cloud SQL instance.

The default Cloud SQL instance backup strategy is a daily backup of the whole instance. Backups can also be customized. More information can be found in this [GCP documentation](https://cloud.google.com/sql/docs/postgres/backup-recovery/backups).\
\
For the Bucket, we recommend making a copy of the Bucket content and placing it in another Bucket, in a folder named with a timestamp to create at each backup.

### Recovery mechanism

Depending on the nature of the disaster, recovery solutions might change. In case of an infrastructure issue, please refer to the section; [Provisioning the infrastructure](./#id-2.-how-to-provision-the-infrastructure) to recreate the defaulting infrastructure elements.\
\
The restoration of Bucket content consists of copying the content of the time-stamped folder described in the Backup strategy section to the application GCS Bucket on which the helm vectice configuration aims at. The restoration of the Cloud SQL instance consists of restoring the database backup following the [GCP documentation](https://cloud.google.com/sql/docs/postgres/backup-recovery/restore).\
\
If the issue requires the creation of a new Kubernetes Cluster, for example, in a new region, please refer to the section: [Application deployment](./#id-3.-how-to-deploy-the-vectice-application) to redeploy the software. Make sure to fill in the values according to your new environment deployment.\
