# Reverse proxy

## Load balancing with enhanced security

{% hint style="info" %}
For self-hosted Vectice deployments, we recommend using a secure load-balancing solution such as [Application Gateway (Azure)](https://learn.microsoft.com/en-us/azure/application-gateway/overview), [AWS Load Balancer](https://docs.aws.amazon.com/eks/latest/userguide/aws-load-balancer-controller.html), or [Google Kubernetes Engine Load Balancer](https://cloud.google.com/kubernetes-engine/docs/concepts/ingress).  Our SaaS offering comes pre-configured with this setup.
{% endhint %}

### Simplified traffic management and enhanced security

* **Single entry point:** The Load Balancer is a single entry point for all incoming traffic. This centralized approach simplifies traffic management and efficiently routes requests to the appropriate backend services within the cluster.
* **Restricted access:** We take security further by restricting incoming traffic to designated ports and protocols. This additional control layer minimizes the attack surface and strengthens our security posture.
* **HTTPS enforcement:** By default, the Load Balancer can be configured to enforce HTTPS encryption for all incoming traffic. This ensures your data is always encrypted in transit, safeguarding it from potential interception.
* **Granular access control:** We can implement granular access control rules within the Load Balancer, restricting access to specific services or resources based on predefined criteria. This provides an extra layer of security.

### Performance and scalability

* **High performance:** Load Balancers are known for their scalability and high-performance capabilities. This ensures our platform can efficiently handle fluctuating traffic volumes, maintaining a smooth user experience.

Combined, Load balancing, which focuses on secure communication protocols and port restrictions, along with a Kubernetes Ingress for traffic management, delivers a robust and secure solution for accessing our software.
