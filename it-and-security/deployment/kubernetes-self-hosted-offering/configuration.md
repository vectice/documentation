# Configuration

This page provides an overview of key variables used during the deployment process. These variables allow for customization based on your specific environment. For detailed descriptions and advanced configuration options, please refer to the `values.yaml` file within the Vectice Helm chart.

## Global Values

Global values in Helm deployments with subcharts allow you to define variables accessible by all charts (main and sub) for consistent configuration across your application.

<table data-header-hidden><thead><tr><th width="254"></th><th width="284"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>baseURL</td><td><br>Repository base URL</td><td>gcr.io</td></tr><tr><td>projectId</td><td>Project ID of the Container Repository</td><td>vectice-public</td></tr><tr><td>secrets</td><td>Secret that will be used to pull images</td><td>vectice-gcr-secrets</td></tr><tr><td>cloudProvider</td><td>Your Cloud provider, set value to gcp, aws or azure</td><td>gcp</td></tr><tr><td>database.host</td><td>Your SQL Instance Private IP address or name</td><td></td></tr><tr><td>database.username</td><td>Your SQL Instance Username</td><td></td></tr><tr><td>database.password</td><td>Your SQL Instance Password</td><td></td></tr><tr><td>database.name</td><td>Your Vectice SQL database name</td><td>vectice</td></tr><tr><td>database.nameKeycloak</td><td>Your Keycloak SQL database name</td><td>keycloak</td></tr><tr><td>database.sslEnabled</td><td>SSL communication with the SQL instance</td><td>true</td></tr><tr><td>appUrl</td><td>Your future Vectice url</td><td></td></tr><tr><td>keycloak.admin.user</td><td>Your Keycloak Admin User</td><td></td></tr><tr><td>keycloak.admin.password</td><td>Your Keycloak Admin Password</td><td></td></tr><tr><td>keycloak.config.session_idle_timeout</td><td>In seconds, session expiration after inactivity</td><td></td></tr><tr><td>keycloak.config.session_max_lifespan</td><td>In seconds, session expiration regardless of activity </td><td></td></tr><tr><td>keycloak.config.access_token_lifespan</td><td>In seconds, validity of acces token<br></td><td></td></tr></tbody></table>

## Database connection configuration

### GCP

Fill in the 3 values with the certificates from your SQL instance:

<table data-header-hidden><thead><tr><th width="259"></th><th width="280"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>database.ssl.key</td><td>Your SQL Instance private SSL Key, encoded in base64</td><td></td></tr><tr><td>database.ssl.cert</td><td>Your SQL Instance private SSL Certificate, encoded in base64</td><td><br></td></tr><tr><td><p>database.ssl.cacert</p><p><br></p></td><td>Your SQL Instance private SSL Root Certificate, encoded in base64</td><td></td></tr></tbody></table>

### AWS

Leave these 3 values empty:

<table data-header-hidden><thead><tr><th width="264"></th><th width="276"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>database.ssl.key</td><td>Your SQL Instance private SSL Key, encoded in base64</td><td></td></tr><tr><td>database.ssl.cert</td><td>Your SQL Instance private SSL Certificate, encoded in base64</td><td><br></td></tr><tr><td><p>database.ssl.cacert</p><p><br></p></td><td>Your SQL Instance private SSL Root Certificate, encoded in base64</td><td></td></tr></tbody></table>

### Azure

Leave `ssl.key` and `ssl.cert` empty. \
\
Retrieve cacert value from [Digicert website](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt.pem)  as documented in this [Azure official documentation ](https://learn.microsoft.com/en-us/azure/postgresql/single-server/concepts-ssl-connection-security)

<table data-header-hidden><thead><tr><th width="269"></th><th width="273"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>database.ssl.key</td><td>Your SQL Instance private SSL Key, encoded in base64</td><td></td></tr><tr><td>database.ssl.cert</td><td>Your SQL Instance private SSL Certificate, encoded in base64</td><td><br></td></tr><tr><td><p>database.ssl.cacert</p><p><br></p></td><td>Your SQL Instance private SSL Root Certificate, encoded in base64</td><td></td></tr></tbody></table>

## Backend values

### General configurations

<table data-header-hidden><thead><tr><th width="275"></th><th width="269"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>defaultPassword</td><td>Your initial Admin password</td><td></td></tr><tr><td>internalSupportEmail</td><td>Email shown at the bottom of the UI, to get help</td><td>support@vectice.com</td></tr><tr><td>adminEmail</td><td>Your initial Admin user</td><td></td></tr></tbody></table>

### SMTP configurations

<table data-header-hidden><thead><tr><th width="277"></th><th width="268"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>smtpTransporter</td><td>Enable email notifications or not, set to true or false</td><td></td></tr><tr><td>smtpOptions.host</td><td>Your SMTP host. eg. smtp.google.com</td><td></td></tr><tr><td>smtpOptions.port</td><td>Your SMTP port. eg. 2525<br></td><td><br></td></tr><tr><td>smtpOptions.secure</td><td>Set to true to enable HTTPS protocol, or false for HTTP protocol</td><td></td></tr><tr><td>smtpOptions.user</td><td>Your SMTP user. eg. admin</td><td></td></tr><tr><td>smtpOptions.password</td><td>Your SMTP password. eg. MySuperPassword123!</td><td></td></tr></tbody></table>

### Storage configurations

<table data-header-hidden><thead><tr><th width="279"></th><th width="267"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>projectStorage.bucket</td><td>Your Vectice Bucket/Container to store attachments</td><td></td></tr></tbody></table>

#### GCP

<table data-header-hidden><thead><tr><th width="284"></th><th width="267"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>projectStorage.gcp.jsonkey</td><td>Your JSON key to access your Vectice GCS Bucket, encoded in base64</td><td></td></tr></tbody></table>

#### AWS

<table data-header-hidden><thead><tr><th width="288"></th><th width="265"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>projectStorage.aws.region</td><td>Your AWS region</td><td></td></tr><tr><td>projectStorage.aws.secretAccessKey</td><td>Your IAM User Secret Key to access your Vectice S3 Bucket</td><td></td></tr><tr><td>projectStorage.aws.accessKeyId</td><td>Your IAM User Key ID to access your Vectice S3 Bucket</td><td></td></tr></tbody></table>

#### Azure

<table data-header-hidden><thead><tr><th width="291"></th><th width="267"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>projectStorage.azure.accountName</td><td>Your Storage Account Name that stores your Blob Container</td><td></td></tr><tr><td>projectStorage.azure.clientid</td><td>Your Client ID</td><td></td></tr><tr><td>projectStorage.azure.tenantid</td><td>Your Tenant ID</td><td></td></tr><tr><td>projectStorage.azure.clientsecret</td><td>Your Client Secret</td><td></td></tr></tbody></table>

### OpenAI configurations

<table data-header-hidden><thead><tr><th width="287"></th><th width="271"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>api_endpoint</td><td>Endpoint to generate auto doc through OpenAI API</td><td></td></tr><tr><td>api_key</td><td>API Key used to communicate with the OpenAI API</td><td></td></tr><tr><td>api_summarize_generate_documentation_parameters</td><td>JSON parameters to fine tune the OpenAI API call (temperature etc.)</td><td></td></tr><tr><td>api_chat_completion_generate_documentation_parameters</td><td>JSON parameters to fine tune the OpenAI API call (temperature etc.)</td><td></td></tr><tr><td>prompts</td><td>Override prompts for iteration templates</td><td></td></tr><tr><td>system_contents</td><td>Override system contents for prompt generation</td><td></td></tr></tbody></table>

## Ingress values

### GCP & Azure

<table><thead><tr><th width="291"></th><th width="272"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>annotations</td><td>Optional, <a href="https://kubernetes.io/docs/concepts/services-networking/ingress/">ingress annotations  documentation</a></td><td></td></tr><tr><td>tls.hosts</td><td>Your future Vectice url (same as global value appUrl)</td><td></td></tr><tr><td>hosts.host</td><td>Your future Vectice url (same as global value appUrl)</td><td></td></tr></tbody></table>

### AWS

<table><thead><tr><th width="292"></th><th width="275"></th><th></th></tr></thead><tbody><tr><td><strong>Variable</strong></td><td><strong>Description</strong></td><td><strong>Default Value</strong></td></tr><tr><td>annotations</td><td>Optional, <a href="https://kubernetes.io/docs/concepts/services-networking/ingress/">ingress annotations  documentation</a></td><td></td></tr><tr><td>certificatearn</td><td>arn reference of your certificate imported in Amazone Certificate Manager</td><td></td></tr><tr><td>tls.hosts</td><td>Your future Vectice url (same as global value appUrl)</td><td></td></tr><tr><td>hosts.host</td><td>Your future Vectice url (same as global value appUrl)</td><td></td></tr></tbody></table>
