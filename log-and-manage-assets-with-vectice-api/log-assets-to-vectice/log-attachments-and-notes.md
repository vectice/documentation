# Log attachments and notes

When exploring assets or creating analyses, adding attachments can be helpful in showcasing charts and data. To add an attachment, log it directly to your iteration.

## Log attachments and notes

To log an image and note to an iteration, use the following:

```python
# Log an image to an iteration
iteration.log("path/data_analysis_chart.png")

# Log a note to an iteration
iteration.log("This is a good model output.")
```

{% hint style="info" %}
You can have multiple images and notes for each iteration.
{% endhint %}

## Dataset attachments

<pre class="language-python" data-overflow="wrap"><code class="lang-python">from vectice import Dataset, FileResource

<strong>origin_dataset = Dataset.origin(name="performance ds", resource=FileResource(paths="./perfs.csv"), attachments=["attachment1.png", "attachment2.png"])
</strong></code></pre>

To log the dataset and its attachments to the Vectice app, simply log them to your current iteration:

```
iteration.log(origin_dataset)
```

## Model attachments

<pre class="language-python" data-overflow="wrap"><code class="lang-python"><strong>from vectice import Model
</strong>
model = Model(name="Unit Sales Predictor", library="scikit-learn", technique="linear regression", metrics=metrics, attachments="regression_graph.png")
</code></pre>

To complete the process, you need to log the model and its attachments to the Vectice app:

```python
iteration.log(model)
```

## Add attachments to phase documentation in Vectice app

There are two ways to add attachments to your phase documentation in the Vectice app.&#x20;

### #1 Add attachments from iterations, datasets, or models

The gif below shows how you could add attachments from your assets. This workflow is the same for adding attachments from **iterations**, **datasets**, and **models**.

<figure><img src="../../.gitbook/assets/insert-image.gif" alt=""><figcaption></figcaption></figure>

### #2 Add attachments uploaded from your computer

You can also upload attachments to your phase documentation from your computer. To do so, select **Insert** > **Image** > **Add an Image** in the phase documentatio&#x6E;**,** then select and upload your image from your files.
