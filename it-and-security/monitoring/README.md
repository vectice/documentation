# Monitoring

Proactive infrastructure monitoring is an essential practice for ensuring the reliability and performance of critical IT services. This section provides an overview of deploying a monitoring solution based on the [kube-prometheus-stack ](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack)on your Kubernetes cluster. Kube-prometheus-stack is a popular open-source solution that simplifies deploying and managing a comprehensive monitoring stack for Kubernetes environments. It leverages Prometheus for time-series data collection and storage, and Grafana for data visualization and alerting.

{% hint style="info" %}
Deployment monitoring is a distinct process from Vectice software deployment.
{% endhint %}

**Benefits:**

* Easy setup with pre-configured monitoring for core Kubernetes components.
* Reduced maintenance with automated Prometheus management.
* Scalable to handle increased monitoring demands.

**Components:**

* Prometheus: Collects and stores metrics.
* Grafana: Visualizes metrics through dashboards.
* Alertmanager (optional): Groups and routes alerts.

**Deployment:**

* Use the official Helm chart for streamlined installation.
* Access Grafana dashboards for cluster health insights.

**Prerequisites:**

<table data-header-hidden><thead><tr><th width="215"></th><th></th></tr></thead><tbody><tr><td><strong>Requirement</strong></td><td><strong>Notes or Details</strong></td></tr><tr><td>Domain Name</td><td>Example:<a href="https://monitoring-vectice.my-company.com"> https://monitoring-vectice.my-company.com</a></td></tr><tr><td>SSL Certificate</td><td><p>Must be associated with the domain name above</p><p>Self-signed certificates are not recommended</p></td></tr><tr><td>Helm v3</td><td><a href="https://helm.sh/docs/intro/install/">Installation Guide</a></td></tr><tr><td>Kubectl</td><td><a href="https://kubernetes.io/docs/tasks/tools/">Installation Guide</a> </td></tr><tr><td>Openssl</td><td><a href="https://wiki.openssl.org/index.php/Binaries">Installation Guide</a></td></tr></tbody></table>

**Additional Notes:**

* Consider RBAC for enhanced Grafana security in production.
* Customize alert rules based on your needs and notification preferences.
* Deploy application-specific metrics exporters for deeper monitoring.

Proceed with the deployment following the [installation guide](installation-guide.md).
