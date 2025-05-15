# VPC segregation

## A dedicated Virtual Private Cloud (VPC)

{% hint style="info" %}
For self-hosted Vectice deployments, we recommend using a dedicated Virtual Private Cloud (VPC). Our SaaS offering comes pre-configured with this setup.
{% endhint %}

To further safeguard your data and applications, we leverage a dedicated Virtual Private Cloud (VPC) deployment model for our infrastructure. Here's what this means for you:

* **Network segregation:** A dedicated VPC creates a logically isolated network environment for our software. This separation ensures that your data and applications remain distinct from other tenants or services, minimizing the risk of unauthorized access or exposure.
* **Increased control:** Dedicated VPCs offer greater control over network traffic. We configured security groups and firewall rules to define precisely how data flows within the VPC, further strengthening our security posture.
* **Improved visibility:** Operating within a dedicated VPC allows us to monitor network activity more effectively. This enhanced visibility helps us identify and address potential security threats more promptly.

**Benefits for you:**

* **Peace of mind:** Knowing your data resides in a secure, isolated environment provides peace of mind.
* **Reduced risk:** Dedicated VPCs minimize the risk of security breaches or unauthorized access attempts.
* **Enhanced compliance:** This deployment model may align with specific industry regulations or compliance requirements.
