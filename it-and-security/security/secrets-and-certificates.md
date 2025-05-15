# Secrets and certificates

While this page highlights our use of Keycloak, a Secret Manager, and secret rotation, it's important to remember that these are just two parts of a comprehensive security strategy. We implement a layered approach encompassing various security measures to safeguard your data.

## Secrets management

{% hint style="info" %}
For self-hosted Vectice deployments, we recommend using a secret manager such as [GCP's secret manager](https://cloud.google.com/security/products/secret-manager) or [Hashicorp's Vault](https://www.vaultproject.io/) to securely store sensitive information. Our SaaS offering comes pre-configured with this setup.
{% endhint %}

### Secrets storage

For our SaaS environment, we leverage a Secret Manager to securely store critical secrets, such as passwords, API keys, and other sensitive data. The Secret Manager encrypts this data at rest and in transit, ensuring it remains protected even in the event of a breach.

Access to the Secret Manager is strictly limited. Only authorized personnel with a legitimate need to access specific secrets are granted the necessary permissions. This minimizes the risk of unauthorized access or misuse of sensitive information.

### Secrets rotation

We implement a rigorous secret rotation strategy for our SaaS environment to further safeguard your data. All critical secrets are rotated monthly. This means these secrets are regularly replaced with new, unique values, significantly reducing the potential impact if a secret were compromised.

## Passwords and authentication token

We prioritize user security and access control. To achieve this, we rely on a powerful tool called Keycloak, an open-source identity and access management (IAM) solution. Keycloak plays a vital role in how you log in and interact with our system.

### Secure logins with password grants

When you log in, Keycloak utilizes a secure protocol called the "password grant." This involves you entering your username and password. Keycloak verifies your credentials against a secure user database, ensuring only authorized users gain access.

### Password policy

Password must be configured for at least 8 characters long, with a mix of uppercase, lowercase, digits, and special characters.

Passwords are then encrypted with 256-SHA and Salt before being stored in the Database.\
API Keys are signed using the HMAC algorithm before being stored in the Database.

### SSO

Vectice enhances security and efficiency with advanced Access Control capabilities, utilizing SAML-based Single Sign-On (SSO) integration, automatic user provisioning, and Role-Based Access Control (RBAC). These features ensure a unified and streamlined authentication and authorization process, allowing secure Vectice access.

We support integration with leading SAML identity providers, such as [Okta](https://www.okta.com/), alongside LDAP user directories, offering a cohesive user management experience. This setup enables IT administrators to manage user access directly within the Okta SSO management console by adding or removing users, modifying roles, and adjusting privileges. Such centralization simplifies Vectice access administration, providing role-specific control and privilege management that caters to the unique needs of data science teams and their stakeholders.

### Beyond passwords: Authentication tokens

Once your login credentials are validated, Keycloak doesn't simply grant direct access. Instead, it issues a secure "authentication token." This token acts like a digital key, granting you temporary access to specific resources within the system. These tokens have a limited lifespan, further enhancing security.

### Keycloak policy update

Independently of vulnerability resolution, the Keycloak version is upgraded at least once every quarter.
