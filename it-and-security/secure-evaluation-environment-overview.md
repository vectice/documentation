# Secure Evaluation Environment Overview

At Vectice, we understand the importance of security and data privacy, especially during product evaluations. To ensure your organization can confidently test our solution, we’ve designed an isolated and secure evaluation environment. This environment is fully isolated from your corporate systems and requires no real data.

### Key Security Features of the Evaluation Environment

1. **No Real Data Required**
   1. **Synthetic Data Usage:** The evaluation can be performed entirely using synthetic or mock data provided by you or we provide in our example projects. By default, employee email addresses may be used unless temporary emails are requested to ensure no personal information is shared.
   2. **No Sensitive Data Needed:** Vectice does not require access to any proprietary, production, or sensitive data during the evaluation process. However, email addresses of participating employees are used by default unless temporary ones are requested.
2. **No Access to Your Systems**
   1. During evaluation, Vectice does not access your internal network, production systems, internal databases, or IT infrastructure.&#x20;
   2. All evaluations are conducted in a completely disconnected environment to ensure no impact on your systems.
   3. Vectice does not typically require any modifications to your internal systems, firewalls, or existing workflows during the evaluation process. However, in certain cases, such as accessing our services from an internet restricted corporate network, whitelisting our evaluation environment might be necessary.
3. **Full Evaluation Environment Provided**
   1. We provide a SaaS evaluation instance of Vectice to evaluate the software, along with a fully-contained Jupyter Notebook environment to simulate data preparation, model training, and evaluating Vectice.
   2. There is no need to download or run any code locally on your systems. All evaluations are conducted outside of your internal network in the environment we provide.
   3. The evaluation environment is isolated from Vectice’s SaaS production infrastructure to avoid any data leakage with our production system.
4. **No Personally Identifiable Information (PII)**
   1. By default, Vectice set up your evaluation test environment without any personal information, except for the email addresses of your participating employees. At the customer’s request, you can also ask Vectice to set up the evaluation test environment with temporary email addresses to ensure absolutely no personal information or other identifying details from your organization are used.

### FAQ: Common Security Questions

**Q: How does Vectice retrieve metadata, and does it have access to the source of the data?**&#x20;

A: Metadata is retrieved exclusively from the dataframe objects in your notebooks or from the database tables you loaded during your modeling exercises. Vectice does not have or maintain any credentials to access the source of data directly. You can find more information in our [Data storage security](security/data-storage-security.md) guide.

**Q: What happens to the data I upload during the evaluation?**

A: Vectice does not require real data. If you choose to upload synthetic data, it remains contained within the evaluation environment and is not shared or stored outside your evaluation environment.

**Q: Do I need to grant Vectice access to internal systems?**

A: No. Vectice does not require or request any access to your IT infrastructure, databases, or proprietary systems.

**Q: What are the processes used by Vectice to secure the data?**

A: Vectice uses industry-standard security measures, including data encryption at rest and in transit, isolated environments for evaluation, and strict access controls, ensuring that all data remains protected throughout the evaluation. You can find more information in our [Data storage security](security/data-storage-security.md) guide.

**Q: What kind of data is collected by Vectice?**

A: During evaluation, Vectice collects only minimal metadata related to the evaluation process, such as system usage statistics and configuration details. No sensitive or proprietary data is collected or stored. You can refer to our [https://www.vectice.com/privacy-and-terms-of-service](https://www.vectice.com/privacy-and-terms-of-service) for more information.

**Q: What is the impact of Vectice’s GenAI features on data privacy?**

A: Vectice uses Microsoft's Windows Azure services to power its AskAI feature, which guarantees data privacy and compliance with industry standards, so your data is always protected.
