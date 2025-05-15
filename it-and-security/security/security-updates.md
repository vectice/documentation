# Security updates

We take security seriously at Vectice. This page outlines our approach to keeping your deployments secure.

## OS updates

* **Frequent Kubernetes Updates:** We leverage a Kubernetes managed service to ensure our Kubernetes environment receives monthly updates. These updates include critical security patches and improvements to the underlying platform.
* **Lightweight, Community-Maintained Docker Images:** Our software uses minimal Docker images, reducing attack surface and potential vulnerabilities. The open-source community actively maintains these images, benefiting from continuous security improvements.

## Packages update

* **Regular Package Updates:** We release security patches and functionality updates for our core software components every two weeks.&#x20;

## SLA

Vectice follows CVSS 3.1 vulnerability assessment and commits to vulnerability resolution with the SLA below:

{% hint style="info" %}
CVSS 3.1, or the **Common Vulnerability Scoring System version 3.1**, is a standardized framework used to rate the severity of security vulnerabilities in software. It provides a numerical score reflecting a vulnerability's potential impact and exploitability, helping organizations prioritize their remediation efforts effectively.
{% endhint %}

| **Vulnerability** | **Resolution target time** | **Mechanism**            |
| ----------------- | -------------------------- | ------------------------ |
| Critical          | << 14 days                 | Patch or regular release |
| High              | << 14 days                 | Patch or regular release |
| Medium            | << 1 month                 | Regular release          |
| Low               | << 2 months                | Regular release          |

**For more information:**

* [Understand the benefits of lightweight container images](https://dev.to/techworld_with_nana/top-8-docker-best-practices-for-using-docker-in-production-1m39)&#x20;
* [CVSS 3.1 specifications document](https://www.first.org/cvss/v3-1/cvss-v31-specification_r1.pdf)
