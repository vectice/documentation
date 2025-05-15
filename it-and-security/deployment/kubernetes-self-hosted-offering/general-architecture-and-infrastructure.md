# General Architecture & Infrastructure

## Architecture Diagram

The diagram represents an overview of the core Vectice Infrastructure, including a Kubernetes Cluster, a SQL instance, and a Bucket.

<figure><img src="../../../.gitbook/assets/Simplified Cloud Infrastructure (1).jpg" alt=""><figcaption></figcaption></figure>

## Infrastructure description

* **Kubernetes cluster:** Vectice will be containerized and deployed within your existing Kubernetes cluster. This ensures scalability, resource efficiency, and simplified management.
* **SQL instance :** a PostgreSQL 13.X instance to store application content.
* **Bucket/container:** A designated storage bucket will be used to house documentation attachments.
* **Cloud-Provisioned load balancer:** An external load balancer, provisioned through your preferred cloud provider, will efficiently distribute incoming traffic to the Kubernetes cluster. This ensures high availability and scalability.
* **DNS resolution:** Configure your internal DNS server to resolve a designated hostname to the IP address or name of the cloud load balancer. This allows users to access Vectice through a user-friendly domain name.
