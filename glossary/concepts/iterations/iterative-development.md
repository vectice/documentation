---
description: >-
  This guide will show data scientist how to sync their iterative development to
  Vectice.
---

# Iterative development

In iterative development, a model is built and tested in repeated cycles. Each cycle tunes and tests the model's hyperparameters until a fully functional algorithm is ready.&#x20;

We'll guide you through this process using Vectice.

## Step 1: Install and configure

Install and import any packages you need for your model development, including the `vectice` library. If you have not installed the `vectice` library, view the [Install Vectice Library ](../../../log-and-manage-assets-with-vectice-api/api-cheatsheets/vectice-python-api-cheatsheet.md#install-vectice)guide for more details.&#x20;

Once you installed and imported `vectice` into your script, connect to the Vectice API.&#x20;

```python
import vectice

connect = vectice.connect(api_token="your-api-key") #Paste your API key
```

Now that you have connected to the Vectice API and linked your script to a project, we can start an iteration.&#x20;

## Step 2: Retrieve a phase

To start an iteration, you must retrieve a phase. To retrieve a phase, connect using your phase ID.

```python
# Connect to your phase using your phase ID
phase = connect.phase("PHA-XXX") #Paste your own phase ID
```

## Step 3: Initialize iteration

After retrieving a phase, we want to begin an iteration. We will initialize an iteration with the `create_or_get_current_iteration()` method, as shown below.

```python
iteration = phase.create_or_get_current_iteration()
```

_Current iteration_ is your last updated iteration. However, if the current iteration is not writable or no iterations exist, we will create an iteration or list writable iterations. If you have multiple "In progress" iterations from the past, to not make assumptions, we will display a list of writable iterations that you can select using the  `{phase}.iteration("iteration name or ID")` method.

{% hint style="info" %}
You can create several editable iterations in different phases, but each user can have only one active iteration session at a time.
{% endhint %}

## Step 4: Log your assets

You can log your assets during model development, testing, and validation using simple code lines to share your progress and work artifacts.

To log your assets, use the iteration's log method as follows:

```python
#Log an asset
iteration.log(asset)

#Log a note
iteration.log("this is a note")
```

This variable `asset` could be your datasets, models and code used while iterating. For more information on how to log specific assets, view the user guides linked below:

* [How to log datasets to Vectice](../../../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-datasets.md)
* [How to log models to Vectice](../../../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-models.md)
* [How to log code to Vectice](../../../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-code.md)

You can also use `sections` to organize your assets:&#x20;

```python
iteration.log(asset, section="your-section-title")
```

The following are a few capabilities that you can utilize to add visibility into your model development.

### **Version Control**

Vectice allows you to track versions of datasets, models, and code used in development. For datasets and models, it includes version IDs, descriptions, lineage, properties, resources, attachments, algorithms, metrics, status, and dataset types.&#x20;

You can find these asset versions and details in the Vectice app under the Datasets and Models sections of the Project.

{% hint style="success" %}
All assets are automatically versioned, making it simple to track a project's progress and compare results across different iterations.
{% endhint %}

## Step 5: Complete an iteration

Once you finish an iteration, use this code to mark it as complete in Vectice in real time.&#x20;

```python
iteration.complete()
```

{% hint style="success" %}
This signals that a phase or task is finished, helping track progress and letting others know it's ready for review or the next steps.
{% endhint %}

You may revisit the details of the iteration for a retrospective. If satisfied, you can summarize your outcomes or start another iteration.&#x20;

## Example

<pre class="language-python" data-overflow="wrap"><code class="lang-python">import numpy as np
import pandas as pd
import vectice
from vectice import FileResource, Dataset, Model, Metric
from sklearn import datasets

# Connect to Vectice
connect = vectice.connect(api_token="your-api-key")

# Retrieve the project phase  
phase = connection.phase("PHA-XXX")

# Initialize iteration
<strong>iteration = phase.create_or_get_current_iteration()
</strong>
# Prepare origin dataset
iris = datasets.load_iris()
data = pd.DataFrame(data=np.c_[iris['data'], iris['target']],
                      columns=iris['feature_names'] + ['target'])
data.to_csv("origin_iris.csv")

# Use FileResource to wrap your local origin dataset
origin_resource = FileResource(paths="origin_iris.csv")
<strong>origin_dataset = Dataset.origin(name="Iris Origin", resource=origin_resource)
</strong>
# Prepare model artifacts
model_name = "your-model-name"
model_metrics = [Metric("RMSE", 153), Metric("Clusters number", 5)]

# Declaring your model artifacts
model = Model(name=model_name, metrics=model_metrics)

# Log the origin dataset and model to Vectice
iteration.log(origin_dataset)
iteration.log(model, section="Model Experiment #1")

# Completes and closes the current iteration
iteration.complete()
</code></pre>

{% hint style="info" %}
The above is just an example of how to perform various actions. The best practice is to have one file (or notebook) per phase of the Project.&#x20;
{% endhint %}

View the [Python API Reference Docs ](https://api-docs.vectice.com/)for more information on how to use Vectice API.
