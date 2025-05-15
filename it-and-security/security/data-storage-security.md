# Data storage security

## Data stored by Vectice

{% hint style="success" %}
Vectice stores metadata and documentation of AI projects. Vectice does not store or access any data from datasets or any customer data.
{% endhint %}

<table><thead><tr><th>Model Versions</th><th width="190">Iterations</th><th>Dataset Versions</th><th>Documentation</th></tr></thead><tbody><tr><td><ul><li>Hyperparameters of models</li><li>Metrics of models</li><li>Performance graphs</li></ul></td><td><ul><li>Metadata about jobs execution</li><li>Comments</li><li>Images to illustrate the iteration</li></ul></td><td><ul><li>Metadata about datasets e.g. table names, number of files, column names, size, etc</li></ul></td><td><ul><li>Documentation of AI projects and documentation history based on user inputs: text, images</li></ul></td></tr></tbody></table>

{% hint style="info" %}
**Note:** We never store or access your actual data—only metadata about your datasets is handled, and we never directly interact with your data or PII.
{% endhint %}

The metadata is retrieved exclusively from the dataframe objects in your notebooks or from the database tables you loaded during your modeling exercises. Vectice does not have or maintain any credentials to access the source of data directly. Using functions like dataframe.describe, we extract summary-level metadata (e.g., column names, data types, and statistical summaries) and send it back to Vectice. This process ensures that no actual data or PII is accessed, stored, or transmitted as part of the Vectice auto-logging process.

Additionally, all automatic metadata extraction is processed entirely within your Python environment, ensuring that sensitive data never leaves your controlled infrastructure.

## JIRA Security and Data Handling

The JIRA integration ensures secure access through OAuth-based user credentials. Metadata such as epic titles, story statuses, and selected fields are retrieved and displayed in the Vectice Documentation page as a widget. Importantly, only metadata is extracted—Vectice does not retrieve or store the content of stories or epics.

Metadata refresh occurs only when a user with the appropriate JIRA credentials re-opens the documentation page in Vectice. This approach ensures that the platform:

1. Does not automatically pull data, and
2. Does not use system credentials with broad access to JIRA.

Metadata retrieval is performed solely at the user's explicit request, maintaining security and minimizing data exposure.

## Encrypted database

{% hint style="info" %}
For self-hosted Vectice deployments, we recommend using a secure Databases solution.  Our SaaS offering comes pre-configured with this setup.
{% endhint %}

**Encryption at rest**

* By default, Vectice employs 256-bit Advanced Encryption Standard (AES-26) symmetric keys to encrypt your data stored in database tables, temporary files, and backups.
* These keys are themselves secured using a separate, robust key encryption process. Vectice manages these keys and rotates them regularly for enhanced security.

**Encryption in transit**

The SQL instance only allows connections from clients that use a valid client certificate and SSL encryption. IAM-based authentication requires Cloud SQL connectors for certificate verification enforcement.

## Encrypted data storage

{% hint style="info" %}
For self-hosted Vectice deployments, we recommend using a secure Storage solution.  Our SaaS offering comes pre-configured with this setup.
{% endhint %}

**Server-side encryption**&#x20;

* This is the default encryption mechanism applied to all data stored in Cloud Storage.
* Vectice employs AES-256 encryption to encrypt your data on the server side before it's written to disk. Google manages the encryption keys and rotates them regularly for enhanced security.

## Identity storage

### Username/password authentication

For basic authentication, Keycloak only stores the information needed to manage your account securely. This typically includes:

* Username
* Email address
* Login credentials (hashed and salted for maximum security)

No sensitive data like financial information or personally identifiable information (PII) beyond what's necessary for account management.

**How does Keycloak protect my data?**

Keycloak utilizes several industry-standard security practices to safeguard your information:

* **Encryption:** Passwords are always stored in encrypted format using strong hashing algorithms.
* **Access Control:** Only authorized personnel have access to user data, and their access is strictly limited based on their roles.
* **Regular Security Audits:** Keycloak undergoes regular security assessments to identify and address any potential vulnerabilities.

### Single Sign-on (SSO)

Vectice enhances security and efficiency with advanced Access Control capabilities, utilizing SAML-based Single Sign-On (SSO) integration with Keycloak.

For added security, Keycloak never holds onto your actual passwords for these providers. Instead, it securely verifies your identity with them directly.

## Backups

At Vectice, we understand that your data is important. That's why we take data security very seriously and implement robust backup procedures to protect your information. Here's what you need to know:

### Regular backups

* For an extra layer of security, we perform a complete backup of our Cloud SQL instance before every single deployment. This ensures we have a clean and recent snapshot of your data in case any unforeseen issues arise during the update process.
* We perform daily backups of our Cloud SQL instance, which houses the core data for our application.&#x20;
* Once a day, automated snapshots of both individual databases within the Cloud SQL instance are taken. These snapshots capture the state of your data at a specific point in time, providing an extra layer of protection.
* In addition to the database backups, we perform daily backups of all the content stored in our Cloud Storage bucket. This ensures that all your files and information are safeguarded against potential loss.

### Benefits of backups

* **Disaster Recovery:** In the unlikely event of a system outage or data corruption, our backups allow us to quickly restore your information and minimize downtime.
* **Accidental Deletion:** Backups provide a safety net if any data is accidentally deleted. We can easily restore it using the latest backup.
* **Peace of Mind:** Knowing your data is securely backed up allows you to use our platform with confidence.

### **Security measures:**

We take several steps to ensure the security of your data backups:

* **Encryption:** Backups are encrypted at rest and in transit, adding an extra layer of protection against unauthorized access.
* **Access controls:** Only authorized personnel have access to manage and restore backups.
* **Regular testing:** We regularly test our backups and [recovery procedures](best-practices.md) to ensure they function properly. Know more about [our backup strategy](data-storage-security.md#backups).

## Data retention policies

We are committed to only retaining the information we need to operate our services effectively and comply with legal requirements. This page explains how long we typically retain different types of data associated with your Vectice SaaS products.

### Customer data

* **Active accounts:** We store your customer data as long as your account is active. This data is essential for providing you with the full functionality of our SaaS products.
* **Terminated accounts:** After your contract terminates, we will retain your customer data for up to 60 days. This buffer period allows you time to retrieve any necessary information before it's permanently deleted. In some cases, legal requirements may necessitate extended retention periods for certain data.

### **Backups of customer data**

We maintain separate backups of your customer data for an extended period of 1 year. These backups serve as an additional safety measure in case of unforeseen circumstances. They are stored securely and separately from the actively used data and are only accessed in rare cases, such as during a disaster recovery scenario.

### **Vectice logs**

We collect logs containing customer instances and metadata, along with debugging data, to maintain system performance and troubleshoot any issues that may arise. We typically retain these logs for 1 year. This allows us to analyze trends, identify potential problems, and continuously improve our services.

### **Your control over your data**

* You have the right to access and update your data during your subscription period.
* Upon contract termination, you can request deletion of your customer data (subject to any legal requirements).

### **Security measures**

We implement robust security measures to protect your data throughout its retention period. This includes:

* Encryption of data at rest and in transit
* Access controls restricting who can view or modify your information
* Regular security audits and testing of our systems
