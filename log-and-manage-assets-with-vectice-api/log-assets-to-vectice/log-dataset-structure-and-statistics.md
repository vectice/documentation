# Log dataset structure and statistics

Data scientists can document dataset structure and statistics in Vectice by using Pandas or Spark dataframes (version 3.0 and newer) when logging datasets.

Most common statistics are currently not captured with Spark Dataframes.

{% hint style="info" %}
Statistics will be captured for the first 100 columns of your dataframe. \
\
Statistics are **not** captured if the numbers of rows are below 100 to keep the data anonymous. The Org Admin can adjust this threshold in organization settings.
{% endhint %}

Here are the automatically captured statistics based on column types in your dataframes.&#x20;

* If no dataframe is provided, it will retrieve schema columns and rows from the resource (if available).&#x20;
* If dataframes are provided, it will infer schema columns and rows based on the dataframe.

<table><thead><tr><th width="150.5">Stats</th><th width="220">Dataframe Column Type</th><th>Description</th></tr></thead><tbody><tr><td>Unique</td><td>Text</td><td>The count of unique values in the dataframe.</td></tr><tr><td>Most Common</td><td>Text</td><td>The most recurrent value in the dataframe and percentage of occurrences.</td></tr><tr><td>Mean</td><td>Numeric, Date</td><td>The average value of the data points in the dataframe.</td></tr><tr><td>Median</td><td>Numeric, Date</td><td>The middle value in the dataframe.</td></tr><tr><td>Variance</td><td>Numeric</td><td>The measure of the distribution of data points in the dataframe from the mean value.</td></tr><tr><td>St. Deviation</td><td>Numeric</td><td>The square root of the variance is a commonly used measure of the data distribution.</td></tr><tr><td>Minimun</td><td>Numeric, Date</td><td>The smallest data point in the dataframe.</td></tr><tr><td>Maximum</td><td>Numeric, Date</td><td>The largest data point in the dataframe.</td></tr><tr><td>Quantiles</td><td>Numeric</td><td>The value in which the data falls within the 25%, 50%, and 75% percentiles and their min and max.</td></tr><tr><td>Missing</td><td>Text, Numeric, Date</td><td>The percentage of missing values in the data column.</td></tr><tr><td>True</td><td>Boolean</td><td>The count of true values with the percentage of occurrence in the column.</td></tr><tr><td>False</td><td>Boolean</td><td>The count of false values with the percentage of occurrence in the column.</td></tr></tbody></table>

### Capture schema without statistic

By default, both schema and column statistics are captured. Setting `capture_schema_only` to `True` captures **only** schema information, excluding column stats.

```python
resource = FileResource(paths, dataframes, capture_schema_only=True)
```

Column stats computation can impact processing time, so it is recommended to set `capture_schema_only` to `True` if performance is a concern or detailed stats are not needed.

### Log origin and cleaned dataset statistics

To log your origin and cleaned resource's structure and statistics for each column type, pass a dataframe to your `Resource` class using the `dataframes` parameter:

<pre class="language-python"><code class="lang-python">df = dataframe...  # load your pandas or spark dataframe

<strong>gcs_resource = GCSResource(
</strong>    uris="gs://my_bucket_name/my_folder/my_filename",
    dataframes=df
)

# Log origin or cleaned datasets and its structure and statistics to Vectice
dataset = Dataset.clean(gcs_resource, name="Clean_Dataset")
</code></pre>

### Log modeling dataset statistics

To log the structure and statistics of your modeling resources, you need to specify which resource statistics you want. You can collect statistics for all modeling resources (training, testing, and validation) or choose specific resources for statistics.&#x20;

For instance, if you only want statistics for your testing resource, use the "dataframe" parameter in the Resource class to log testing\_resource statistics.

#### Pandas dataframe statistics logging example

```python
# Create your pandas (or spark) dataframes for your modeling datasets  
training_dataframe = pd.DataFrame(pd.read_csv("train_clean.csv"))
testing_dataframe = pd.DataFrame(pd.read_csv("train_reduced.csv"))
validation_dataframe = pd.DataFrame(pd.read_csv("validation.csv"))

# Create your dataset resources to wrap your datasets and collect statistics
training_resource = FileResource(paths="train_clean.csv", dataframes=training_dataframe)
testing_resource = FileResource(paths="train_reduced.csv", dataframes=testing_dataframe)

# Data resource without collecting statistics
validation_resource = FileResource(paths="validation.csv")

# Log all modeling datasets and its structure and statistics to Vectice
modeling_dataset = Dataset.modeling(
                    name = "Modeling",
                    training_resource = training_resource,
                    testing_resource = testing_resource,
                    validation_resource = validation_resource,
                  )
```

<figure><img src="../../.gitbook/assets/update-dataset-v2.png" alt=""><figcaption></figcaption></figure>
