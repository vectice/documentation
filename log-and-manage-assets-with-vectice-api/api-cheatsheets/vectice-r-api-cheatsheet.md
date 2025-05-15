# Vectice R API cheatsheet

This API guide provides a quick overview of Vectice's simple R API calls to help you get started auto-documenting your datasets, models, and notes.&#x20;

{% hint style="info" %}
Be sure to [create your API key](../connect-to-api.md) first!
{% endhint %}

## Install Vectice

Start by installing the Vectice library.

```r
# Install reticulate if not already installed
install.packages("reticulate")

# Install the latest Vectice library
reticulate::py_install("vectice", pip = TRUE)

# Or install a specific version of Vectice
reticulate::py_install("vectice==<desired_version_number>", pip = TRUE)
```

## Connect to Vectice

Get started by connecting to the Vectice API and starting an iteration.

```r
#import and connect to Vectice
vectice <- reticulate::import("vectice")
connect <- vectice$connect(
    api_token = 'your-api-key',        # Paste your api key
    host = 'https://app.vectice.com',  # Paste your host
)

# Connect to your project phase using your phase ID
phase = connect$phase("PHA-XXX") #You can fetch the relevant phase ID from your chosen Vectice project in the app.

#Create an iteration
iteration <- phase$create_or_get_current_iteration()
```

## Auto-document your assets

Auto-document your notes, datasets, and models directly to Vectice.

### Auto-document NOTES

```r
# Auto-document your first comments or notes
iteration$log("this is a comment")
```

### Auto-document DATASETS

{% tabs %}
{% tab title="Local file" %}
```r
# Auto-document your first dataset from a local file
ds_resource <- vectice$FileResource(paths, dataframes)
raw_ds <- vectice$Dataset$origin(name=name, resource=ds_resource, attachments = attachments)
iteration$log(raw_ds)
```
{% endtab %}
{% endtabs %}

### Auto-document MODELS

{% tabs %}
{% tab title="Default" %}
<pre class="language-r"><code class="lang-r"><strong># Auto-document your first model
</strong>model &#x3C;- vectice$Model(library, technique, metrics, properties, name, attachments, predictor)
iteration$log(model)
</code></pre>
{% endtab %}
{% endtabs %}

## Close your iteration

Once you are done logging your assets for an iteration, mark it complete.

```r
# Completes and closes the current iteration once you are happy with it
iteration$complete()
```

## Additional resources

<table data-card-size="large" data-view="cards"><thead><tr><th></th><th></th><th data-hidden></th><th data-hidden data-type="content-ref"></th><th data-hidden data-card-target data-type="content-ref"></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><mark style="color:blue;"><strong>Vectice R Sample</strong></mark></td><td>Learn how you can use Vectice with R!</td><td></td><td></td><td><a href="https://github.com/vectice/Customer-Success/blob/develop/RStudio%20Sample/Vectice_R_Sample.R">https://github.com/vectice/Customer-Success/blob/develop/RStudio%20Sample/Vectice_R_Sample.R</a></td><td><a href="../../.gitbook/assets/Screen Shot 2023-10-19 at 1.23.07 PM.png">Screen Shot 2023-10-19 at 1.23.07 PM.png</a></td></tr><tr><td></td><td></td><td></td><td></td><td></td><td></td></tr></tbody></table>
