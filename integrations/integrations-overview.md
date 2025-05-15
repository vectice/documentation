# Integrations Overview

Vectice easily integrates with the tools you already use—from AI/ML platforms and notebooks to MLOps and data platforms—making your workflow smoother and more efficient. Our integrations are flexible and quick to set up, allowing you to start using Vectice with minimal changes to your current process.

_Explore our available integrations:_

## 🧠 AI/ML Platforms & Libraries

Manage models, experiments, and data directly within your favorite AI/ML tools to enhance your machine learning workflows.

<table data-header-hidden><thead><tr><th></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td><p></p><ul><li>Python</li><li>R</li><li>scikit-learn</li><li>spaCy</li><li>TensorFlow</li><li>XGBoost (XGB)</li><li>Keras (K)</li><li>MLflow</li><li>SAS Py</li><li>SAS Viya</li><li>Azure ML</li></ul></td><td><p></p><ul><li>Spark MLlib</li><li>PyTorch </li><li>H2O.ai</li><li>MindsDB </li><li>DataRobot</li><li>PyCaret </li><li>Ludwig</li><li>W&#x26;B</li><li>Vertex AI</li><li>Sagemaker</li><li>IBM Watsonx</li></ul></td><td></td></tr></tbody></table>

### Vectice x IBM watsonx

Our integration with IBM Watsonx delivers a seamless, end-to-end solution that streamlines compliance throughout the model lifecycle.

Vectice complements Watsonx by:

* **Automating AI documentation:** Ensuring Model Development Documents (MDDs) and Model Validation Documents (MVDs) are automatically generated and audit-ready.
* ‍**Enriching metadata integration**: Capturing granular model metadata across the AI lifecycle, enhancing watsonx traceability capabilities.
* ‍**Simplifying evidence gathering and ensuring audit readiness**: Vectice captures and organizes critical evidence, including code, model and dataset lineage, testing outcomes, and version history.
* ‍**Expanding cross-platform governance support:** Allowing metadata from various AI development environments (e.g. IBM Watson Studio, Jupyter Notebooks, Databricks, SageMaker) to integrate seamlessly with Watsonx governance.

## 💻 Notebooks, IDEs, CI/CD, & Pipelines

Streamline development using Vectice alongside your notebooks, IDEs, and CI/CD tools for a cohesive coding and deployment experience.

{% hint style="info" %}
You can integrate Vectice within these environments by [installing the Vectice library package](../log-and-manage-assets-with-vectice-api/connect-to-api.md).
{% endhint %}

<table data-header-hidden><thead><tr><th></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td><ul><li>Jupyter notebook</li><li>RStudio </li><li>VS Code </li><li>GitHub Actions</li><li>Databricks</li></ul></td><td><ul><li>Jenkins</li><li>Collab notebook</li><li>Python IDE</li><li>Atom</li><li>Sagemaker</li></ul></td><td></td></tr></tbody></table>

### Proxy support

You can use Vectice with an `HTTP` and a `HTTPS` proxy server. This is used to connect your ecosystems to the Vectice instance. To route all Vectice traffic through the proxy server, set the environment variable to the proxy URL.

#### HTTPS Example <a href="#http-example" id="http-example"></a>

```
HTTPS_PROXY = "https://user:password@proxy.host.com:port"
```

Environment variables:

* `HTTP_PROXY` is the proxy to use for HTTP requests.
* `HTTPS_PROXY` is the proxy to use for HTTPS requests. In most cases, this is the same as `HTTPS_PROXY`.
* `PROXY` is your personal proxy.
* `NO_PROXY` is a comma-separated list of DNS suffixes or IP addresses that can be accessed without passing through the proxy.

## 🔄 MLOps Platforms

Simplify model management and deployment with Vectice integrations for popular MLOps platforms, automating workflows and improving consistency.

<table data-header-hidden><thead><tr><th></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td><ul><li>GitHub</li><li>MLFlow</li><li>Weights &#x26; Biases</li><li>Jenkins</li><li>Great Expectations</li></ul></td><td><ul><li>Bitbucket</li><li>CodeCommit</li><li>Arize</li><li>Sagemaker</li><li>Other git based systems</li></ul></td><td></td></tr></tbody></table>

## :timer: Productivity Platforms

**JIRA Integration \[BETA]**

Vectice integrates with JIRA to display epics and their associated stories, including statuses, directly within your documentation as interactive widgets. Data refreshes automatically when users with proper JIRA credentials reopen the page, ensuring on demand, up-to-date information.

The JIRA integration allows teams to:

* **Unify Documentation**: Automatically include JIRA metadata, keeping stakeholders informed without switching tools.
* **Maintain Context**: Link technical progress with business objectives by embedding relevant JIRA details into documentation.

With this integration, your team can ensure project updates are always aligned with documentation, fostering better collaboration and transparency.

**Confluence Compatibility**

Documentation can be exported seamlessly in Word formats, making it easy to integrate with Confluence. Users can import these files through the Confluence UI, incorporating Vectice documentation into their workflows effortlessly.

**Google Docs Compatibility**

Documentation is compatible with Google Docs, supporting imports from Word format and exports to Google Docs for streamlined workflows.

## 🗄️ Data Platforms

Connect Vectice with leading data storage platforms to keep your data secure and accessible, enabling seamless data handling and compliance.

{% hint style="info" %}
To learn more about the code wrappers, visit our [API reference docs](https://api-docs.vectice.com/reference/vectice/).
{% endhint %}

<table data-header-hidden><thead><tr><th></th><th></th><th data-hidden></th></tr></thead><tbody><tr><td><p></p><ul><li>Snowflake</li><li>AWS S3</li><li>Google Cloud Storage</li><li>Azure Blob Storage</li><li>Redshift </li><li>Synapse </li></ul></td><td><p></p><ul><li>Databricks</li><li>BigQuery</li><li>SparkTable</li><li>Delta Table</li><li>Postgres</li><li>Amazon Redshift</li></ul></td><td></td></tr></tbody></table>

## :gear: Developer Tools & APIs

Vectice offers powerful tools for developers who want more control over their integrations. With our APIs, you can connect directly with Vectice, automate key tasks, and customize how Vectice fits into your workflow.

### Python API&#x20;

The Vectice Python API makes it easy to interact with Vectice right from your Python environment. Automate tasks, document your data and track versions—directly in your code.

* **Key Uses**:
  * Upload and manage data in formats like CSV or JSON
  * Connect with data storage (Google Cloud Storage, Amazon S3, Databricks)
  * Auto-document datasets, models, and notes
  * Track data and model versions over time
  * Handle errors and logging

Please refer to the dedicated [installation guide](../log-and-manage-assets-with-vectice-api/connect-to-api.md#install-vectice) to install the Vectice Python API and view the official [Vectice Python API documentation](https://api-docs.vectice.com) for the latest details and code examples.

### R

Use Vectice in R with the `reticulate` package, bringing Vectice’s API capabilities directly to your R workflows. It’s a smooth, flexible way to extend Vectice into R.

{% hint style="info" %}
Understand more about the [**reticulate**](https://cran.r-project.org/web/packages/reticulate/vignettes/calling_python.html) package.
{% endhint %}

Please refer to the dedicated [installation guide](../log-and-manage-assets-with-vectice-api/connect-to-api.md#install-vectice) for installing `reticulate` and view the official [Vectice Python API documentation](https://api-docs.vectice.com) for the latest details and code examples.

### GraphQL / Rest

For advanced setups, our GraphQL and REST APIs let you integrate Vectice in a custom way. Available for self-hosted deployments, these APIs are perfect for unique workflows or internal tools.

* **Key Uses**:
  * Custom integrations with in-house systems
  * Full control over Vectice data through API access
  * Support for creating workflows that meet specific needs

This solution offers seamless on-demand integration. Our expert team is available to assist with advanced customization needs. Just contact us at support@vectice.com to discuss your specific requirements.
