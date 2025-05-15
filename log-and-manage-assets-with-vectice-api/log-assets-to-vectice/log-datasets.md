---
description: Learn how to log your datasets to Vectice.
---

# Log datasets

{% hint style="info" %}
Make sure to complete the [prerequisites](../connect-to-api.md#prerequisites-to-register-assets) before getting started with logging datasets to Vectice. To learn more, view our [Getting Started with Vectice API guide](../connect-to-api.md).
{% endhint %}

The Vectice API enables you to log all datasets used during development to the Vectice app. This includes **origin datasets**, **cleaned datasets**, and **modeling datasets.**

| Dataset type      | Description                                                                                                             |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Origin datasets   | Origin datasets refer to your datasets containing **raw data**.                                                         |
| Cleaned datasets  | Cleaned datasets refer to your datasets that have been **cleaned and prepared for data modeling** or **data analysis**. |
| Modeling datasets | Modeling datasets combine **training**, **testing**, and **validation** data in a single dataset.                       |

## Dataset logging

Now that you know more about the different dataset types and available [resources](../../glossary/concepts/datasets/dataset-resources.md), we will walk you through logging your dataset metadata.&#x20;

Each dataset's metadata is logged at the iteration level. Use the static methods for each dataset type (i.e., `origin()`, `clean()`, and `modeling()` to log your datasets to Vectice.&#x20;

### Log origin dataset

To log the columnar data of your origin dataset, [use any resource](../../glossary/concepts/datasets/dataset-resources.md) to log it to your current iteration. For this example, we will use `FileResource()` to log a local origin dataset:

{% code overflow="wrap" %}
```python
from vectice import FileResource

# Log your origin dataset's supporting artifacts to your current iteration
origin_dataset = Dataset.origin(name="Iris Origin", resource=FileResource(paths="raw_iris.csv"))

iteration.log(origin_dataset) 
```
{% endcode %}

### Log cleaned dataset

To log the columnar data of your cleaned dataset, use any resource to log it to your current iteration. For this example, we will use `FileResource()` to log a local clean dataset:

{% code overflow="wrap" %}
```python
from vectice import FileResource

# Log your clean dataset's supporting artifacts to your current iteration
clean_dataset = Dataset.clean(name="Iris Cleaned", resource=FileResource(paths="iris_cleaned.csv"))
                                
iteration.log(clean_dataset)
```
{% endcode %}

### Log modeling dataset

To log the columnar data of your modeling datasets used for **training**, **testing**, and **validation**, use any resource to log it to your current iteration. We will use `FileResource()` to log this example dataset:

{% hint style="info" %}
Training and testing resources are **required** to log a modeling dataset. Validation resources are **optional**.
{% endhint %}

```python
from vectice import FileResource

training_resource = FileResource(paths="iris_training.csv")
testing_resource = FileResource(paths="iris_testing.csv")
validation_resource = FileResource(paths="iris_validation.csv") #optional

# Log your modeling dataset's supporting artifacts to your current iteration
modeling_dataset = Dataset.modeling(
    name="Modeling Dataset",
    training_resource=training_resource,
    testing_resource=testing_resource,
    validation_resource=validation_resource)
    
iteration.log(modeling_dataset)
```

### **Full code example**

This example will demonstrate the full workflow of how to log your modeling datasets' supporting artifacts to Vectice.

```python
from vectice import FileResource

# Connect to Vectice 
connect = vectice.connect(
    api_token = 'your-api-key',        # Paste your api key
    host = 'https://app.vectice.com',  # Paste your host
)

# Select your project phase
phase = connect.phase("PHA-xxxx") #Paste your own phase ID

# Create an iteration
iteration = phase.create_or_get_current_iteration()

# Wrap your datasets used for training, testing, and validation
training_resource = FileResource(paths="iris_training.csv")
testing_resource = FileResource(paths="iris_testing.csv")
validation_resource = FileResource(paths="iris_validation.csv")

# Log your modeling datasets
modeling_data = Dataset.modeling(
    name="Modeling Dataset",
    training_resource=training_resource,
    testing_resource=testing_resource,
    validation_resource=validation_resource)

iteration.log(modeling_data)

# Complete the iteration
iteration.complete()
```

Once your wrapped dataset is logged inside of Vectice, you can view datasets supporting artifacts by clicking on the **Datasets** tab in the Vectice app.

## Best practices

* When logging datasets, append the dataset type (**Origin**, **Cleaned**, and **Modeling**) to the end of the corresponding dataset name for easy identification when logged in the Vectice app.
* Before cleaning or transforming your datasets, log your **origin** **dataset** to Vectice. This way, you can always refer back to it if needed.
* As you iterate through different modeling approaches, log multiple versions of your modeling dataset. This will help you to keep track of the changes you have made and to compare the results of different approaches.
* Document your work thoroughly, including your data sources, cleaning and modeling processes, and any assumptions or decisions you make. This will help you to communicate your work to others and to ensure that your analysis is transparent and reproducible. Document key milestones via:
  * The Vectice app in your Phase documentation
  * The Vectice API by adding an iteration note&#x20;
* Mark your **most valuable iterations and assets** in the Vectice app by selecting the **star** next to the corresponding iteration and assets **before** beginning the phase review. This will make it easier for stakeholders and subject matter experts to identify the iterations and assets in review.
