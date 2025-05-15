# Business continuity

### Built-in resilience: Ensuring business continuity

We understand that uninterrupted service is critical for your business. That's why we leverage a Kubernetes managed service to ensure your application remains available despite potential disruptions.

Here's how we achieve high availability:

* **Multiple pods:** Your application is spread across several separate pods or "containers" within our cloud environment. Think of these containers as small, independent workers. If one stops working, the others keep going, which means less chance of your service going down.
* **Load balancing:** Our "traffic manager" intelligently sends visitors to the healthiest container. This ensures that your service remains smooth and uninterrupted, even if some containers are experiencing temporary issues.
* **Highly available Cloud SQL instance:** We leverage Cloud SQL's high availability option, guaranteeing database accessibility in case of a regional outage. This means your data is safe and always accessible, even during a major disruption.

This multi-layered approach provides a strong foundation for business continuity. Even during unexpected events, your application can maintain functionality and minimize disruptions to your operations.
