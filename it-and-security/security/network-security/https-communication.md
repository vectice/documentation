# HTTPS communication

## Securing external communications

At Vectice, we understand the importance of safeguarding your data when you use our software. That's why we prioritize secure communication through HTTPS encryption.

{% hint style="info" %}
For self-hosted Vectice deployments, we recommend using a DNS provider such as [Cloudflare](https://www.cloudflare.com/) with secured certificates.  Our SaaS offering comes pre-configured with this setup.
{% endhint %}

* **Cloudflare certificates:** We utilize high-quality SSL/TLS certificates from Cloudflare for our vectice.com domain. These certificates encrypt all communication between your web browser and our servers. This encryption scrambles the data, making it unreadable to anyone who might try to intercept it as it travels across the internet.
* **Cloudflare protection:** In addition to the certificates, we benefit from Cloudflare's industry-leading security expertise. CloudFlare acts as an extra shield in front of our infrastructure, filtering out malicious traffic and further safeguarding your connection.

This combined approach with Cloudflare certificates and protection offers robust encryption and an additional layer of security for your data transmitted to and from vectice.com.

## Securing internal communications

{% hint style="info" %}
Understand more about [cert-manager mechanisms](https://cert-manager.io/).
{% endhint %}

We take secure communication within our system very seriously. Here's how we achieve this:

* **Automated certificate management:** We utilize cert-manager, a powerful tool within our Kubernetes cluster. This tool automates the entire lifecycle of SSL/TLS certificates for our internal services.
* **HTTPS encryption:** With these certificates in place, all application instances within the cluster can communicate with each other securely using HTTPS encryption. This encryption safeguards your data by scrambling it during transmission, making it unreadable to anyone who might intercept it.
* **Streamlined certificate handling:** Cert-manager obtains, renews, and deploys certificates automatically. This ensures our certificates are always valid and readily available, minimizing the risk of expired certificates interrupting communication.

By prioritizing secure communication within our infrastructure, we foster a robust and trustworthy internal network for your data.
