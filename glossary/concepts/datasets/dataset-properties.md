# Dataset properties

You can use Dataset properties to document the unique qualities, features, or characteristics of a dataset. These properties can be added as a dictionary when logging the dataset or after it's created.

Properties are _optional_ and work with `Dataset.origin`, `Dataset.clean` and `Dataset.modeling` by assigning to the properties parameter, as shown below:

```python
origin_resource = FileResource(paths="items.csv")
properties = {"test":10, "QA":"Approved", "Bool":True}
 
# Assigning properties while logging an origin dataset 
origin_dataset = Dataset.origin(
                  name = "Origin_Dataset",
                  resource = origin_resource,
                  properties=properties)

iteration.log(origin_dataset)
```

You can also **update** **or add dataset properties** after a dataset has been logged. You must re-log your dataset to an iteration to save your updated dataset properties.

<pre class="language-python"><code class="lang-python"># Updating or adding properties after logging origin dataset
origin_dataset.properties = {"test":1, "QA":"Not started", "Bool":False}

# Re-log dataset to save updated properties
<strong>iteration.log(origin_dataset)
</strong></code></pre>
