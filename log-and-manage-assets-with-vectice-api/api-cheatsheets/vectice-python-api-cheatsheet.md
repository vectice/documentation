# Vectice Python API cheatsheet

This API guide provides a quick overview of Vectice's simple Python API calls to help you get started auto-documenting your datasets, models, and notes.&#x20;

{% hint style="info" %}
Be sure to [create your API key](../connect-to-api.md) first!
{% endhint %}

## Install Vectice

Start by installing the Vectice library.

```python
# Install Vectice latest package
pip install vectice

# Install a specific version of the Vectice package
pip install vectice==<version number>
```

## Connect to Vectice

Get started by connecting to the Vectice API and starting an iteration.

{% tabs %}
{% tab title="Connect with API key" %}
```python
#import and connect to Vectice
import vectice
connect = vectice.connect(
    api_token = 'your-api-key',        # Paste your api key
    host = 'https://app.vectice.com',  # Paste your host
)

# Connect to your project phase using your phase ID
phase = connect.phase("PHA-XXX") #You can fetch the relevant phase ID from your chosen Vectice project in the app.

#Create an iteration
iteration = phase.create_or_get_current_iteration()
```
{% endtab %}

{% tab title="Connect with JSON file" %}
```python
#import and connect to Vectice
import vectice
connect = vectice.connect(config="your-api-config.json") #Enter your API key JSON file

# Connect to your project phase using your phase ID
phase = connect.phase("PHA-XXX") #You can fetch the relevant phase ID from your chosen Vectice project in the app.

#Create an iteration
iteration = phase.create_or_get_current_iteration()
```
{% endtab %}
{% endtabs %}

## Auto-document your assets

Auto-document your notes, datasets, and models directly to Vectice.

### Auto-document NOTES

```python
# Auto-document your first comments or notes
iteration.log("this is a comment")
```

### Auto-document DATASETS

For instructions on using these resources, refer to the [Vectice API Reference ](https://api-docs.vectice.com/)guide's Resources section.

{% tabs %}
{% tab title="Local file" %}
<pre class="language-python"><code class="lang-python">from vectice import FileResource, Dataset
<strong>
</strong><strong># Auto-document your first dataset from a local file
</strong>file_resource = FileResource(paths="my/file/path", dataframe=your_df)
clean_dataset = Dataset.clean(resource=file_resource, name="your_dataset_name")
iteration.log(clean_dataset)
</code></pre>
{% endtab %}

{% tab title="BigQuery" %}
```python
from vectice import BigQueryResource, Dataset

# Auto-document your first dataset from BigQuery
bq_resource = BigQueryResource(paths="your-bq-table", dataframes=your_df)
clean_dataset = Dataset.clean(resource=bq_resource, name="your_dataset_name")
iteration.log(clean_dataset)
```
{% endtab %}

{% tab title="S3" %}
```python
from vectice import S3Resource, Dataset

# Auto-document your first dataset from S3
s3_resource = S3Resource(uris="s3://.../<file_path_inside_bucket>", dataframes=your_df)
clean_dataset = Dataset.clean(resource=s3_resource, name="your_dataset_name")
iteration.log(clean_dataset)
```
{% endtab %}

{% tab title="GCS" %}
```python
from vectice import GCSResource, Dataset

# Auto-document your first dataset from GCS
gcs_resource = GCSResource(uris="gs://.../<file_path_inside_bucket>", dataframes=your_df)
clean_dataset = Dataset.clean(gcs_resource, name, attachments)
iteration.log(clean_dataset)
```
{% endtab %}

{% tab title="Databricks" %}
```python
from vectice import DatabricksTableResource, Dataset

# Auto-document your first dataset from Databricks
db_resource = DatabricksTableResource(paths="my-table", dataframes=your_df)
clean_dataset = Dataset.clean(resource=gcs_resource, name="your_dataset_name")
iteration.log(clean_dataset)
```
{% endtab %}

{% tab title="Snowflake" %}
```python
from vectice import SnowflakeResource, Dataset

# Auto-document your first dataset from Snowflake

connection_parameters = {
    ...
}
new_session = Session.builder.configs(connection_parameters).create()

sf_resource = SnowflakeResource(
    dataframes=your_df
    snowflake_client=new_session,
    paths="SNOWFLAKE_SAMPLE_DATA.TPCH_SF10.PART",
)
clean_dataset = Dataset.clean(resource=sf_resource, name="your_dataset_name")
iteration.log(clean_dataset)
```
{% endtab %}

{% tab title="SparkTable" %}
```python
from vectice import SparkTableResource, Dataset

# Auto-document your first dataset from SparkTable
st_resource = SparkTableResource(
    dataframes=your_df
    spark_client=spark,
    paths="my_table",
)
clean_dataset = Dataset.clean(resource=st_resource, name="your_dataset_name")
iteration.log(clean_dataset)
```
{% endtab %}
{% endtabs %}

### Auto-document MODELS

{% tabs %}
{% tab title="Default" %}
```python
from vectice import Model

# Auto-document your first model
model = Model(metrics, properties, attachments, predictor)
iteration.log(model)
```
{% endtab %}

{% tab title="MLFlow" %}
```python
import mlflow
from mlflow.client import MlflowClient
from vectice import Model

# Auto-document your first model
model = Model.mlflow(
        run_id="your-mlflow-run-id",
        client=MlflowClient() #also work with client=mlflow
    )
iteration.log(model)
```
{% endtab %}
{% endtabs %}

## Close your iteration

Once you are done logging your assets for an iteration, mark it complete.

```python
# Completes and closes the current iteration once you are happy with it
iteration.complete()
```
