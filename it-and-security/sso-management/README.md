# SSO management

## Single Sign-On authentication

### Access Control & SSO

Vectice enhances security and efficiency with advanced Access Control capabilities, utilizing SAML-based Single Sign-On (SSO) integration, automatic user provisioning, and Role-Based Access Control (RBAC). These features ensure a unified and streamlined authentication and authorization process, allowing secure Vectice access.&#x20;

{% hint style="info" %}
We support integration with any generic SAML identity providers.
{% endhint %}

Our SSO configuration is manageable via the Vectice admin interface, guaranteeing straightforward and secure authentication for all users, including data scientists and model owners.\
\
Such centralization simplifies Vectice access administration, providing role-specific control and privilege management that caters to the unique needs of data science teams and their stakeholders.

### Generic SAML integration

{% hint style="info" %}
This guide is for [**Admins**](../../admin-guides/user-management/user-roles-and-permissions.md) who have permission to make these changes.
{% endhint %}

For Single Sign-On (SSO), Vectice offers maximum flexibility. We integrate seamlessly with any SAML-based identity provider, not just the usual suspects. Our expert team is happy to help you customize the configuration to perfectly match your specific requirements, ensuring a secure and efficient login process for your users.

{% content-ref url="generic-saml-integration.md" %}
[generic-saml-integration.md](generic-saml-integration.md)
{% endcontent-ref %}

### Okta integration

{% hint style="info" %}
This guide is for [**Admins**](../../admin-guides/user-management/user-roles-and-permissions.md) who have permission to make these changes.
{% endhint %}

This setup enables IT administrators to manage user access, remove users, modify roles, and adjust privileges—directly within the Okta SSO management console. Such centralization simplifies Vectice access administration, providing role-specific control and privilege management that caters to the unique needs of data science teams and their stakeholders.

Please refer to our dedicated user guide for SSO configuration:

{% content-ref url="okta-sso-integration.md" %}
[okta-sso-integration.md](okta-sso-integration.md)
{% endcontent-ref %}
