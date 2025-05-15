# Dataset resources

Use the resources below to wrap data from any source, allowing you to log your dataset's columnar data and artifacts in Vectice.

For instructions on using these resources, refer to the [Vectice API Reference ](https://api-docs.vectice.com/)guide's Resources section.

{% hint style="info" %}
Vectice stores the artifacts of your datasets, **not** your actual datasets.
{% endhint %}

<table><thead><tr><th width="326">Resources</th><th width="482">Description</th></tr></thead><tbody><tr><td><code>Resource()</code></td><td>Wrap your dataset's columnar data and artifacts from your storage location. It can be extended for any data source. (example: <strong>Redshift, RDS, etc.</strong>)</td></tr><tr><td><code>FileResource(...)</code></td><td>Wrap your dataset's columnar data and artifacts from a <strong>local file</strong>.</td></tr><tr><td><code>GCSResource(...)</code></td><td>Wrap your dataset's columnar data and artifacts from your <strong>Google Cloud Storage (GCS)</strong> source.</td></tr><tr><td><code>S3Resource(...)</code></td><td>Wrap your dataset's columnar data and its artifacts from your <strong>AWS</strong> <strong>S3</strong> source.</td></tr><tr><td><code>BigQueryResource(...)</code></td><td>Wrap your dataset's columnar data and artifacts from your <strong>BigQuery</strong> source.</td></tr><tr><td><code>DatabricksTableResource(...)</code></td><td>Wrap your dataset's columnar data and artifacts from your <strong>Databricks</strong> source.</td></tr></tbody></table>

## Resource usage examples

Below we highlight how you can use the available Resources to wrap your dataset's columnar and artifacts to later [log your dataset](../../../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-datasets.md) to Vectice.

### A Custom Data Source&#x20;

To wrap data from a custom data source, create a custom resource inherited from the base `Resource` class and implement your own `_build_metadata()` and `_fetch_data()` methods.&#x20;

View our guide [How to add a custom data source](../../../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-a-custom-data-source.md) for more information and examples.
