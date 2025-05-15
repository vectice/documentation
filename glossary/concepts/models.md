---
description: Learn more about Models within Vectice.
---

# Models

Models reflect the model metadata logged to Vectice during model development. All models are versioned and tagged with their deployment environment within Vectice.&#x20;

## Model artifacts in Vectice

Below is a list of artifacts you can find in the Vectice app after data scientists log the models artifacts from their iterative development.

| Artifacts              | Description                                                                                                                                                                                                                                                                                                                                                                                                                        |
| ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Model snapshot         | Highlights the number of model versions grouped by model status.                                                                                                                                                                                                                                                                                                                                                                   |
| Model Status           | The model status states whether the model is in **Production**, **Staging,** or **Experimentation** mod&#x65;**.**                                                                                                                                                                                                                                                                                                                 |
| Model creation details | Creation details show when the model was created and who it was created by.                                                                                                                                                                                                                                                                                                                                                        |
| Model type             | Classifies the model by model type. For example, **clustering**, **classification**, or **regression**.                                                                                                                                                                                                                                                                                                                            |
| Technique              | The technique highlights the exact modeling algorithm used for the model. (i.e., Linear Regression)                                                                                                                                                                                                                                                                                                                                |
| Model lineage          | The model lineage can showcase the dataset used for the model, the code captured from `git` and the model version output.                                                                                                                                                                                                                                                                                                          |
| Model metrics          | The model metrics captures metrics used to evaluate model performance. (i.e., MAE and RSME values)                                                                                                                                                                                                                                                                                                                                 |
| Versions               | Models with the same name as another model you already logged in Vectice. As you log models with the same name, the versions are incremented, maintaining the model's history.                                                                                                                                                                                                                                                     |
| Attachments            | <p>Attachments showcase files that were logged with the model. For example, this could be notebooks, images, or excel sheets of data analysis, model results, etc.<br><br><strong>All file types are supported for model attachments and can be downloaded from the Vectice app.</strong> </p><p></p><p>However, the <strong>supported previews types</strong> in the Vectice app are PNG, JPEG, CSV, Notebook, and TXT files.</p> |

## Models best practices

* Project phases that aim to **train**, **test**, or **validate** **models** should have iteration sections to log the models accordingly. This is typically completed in the **Modeling** phase of a CRISP-DM project.
* Mark your **most valuable iterations and assets** in the Vectice app by selecting the **star** next to the corresponding iteration and assets **before** beginning the phase review. This will make it easier for stakeholders and subject matter experts to identify the iterations and assets in review.

{% hint style="info" %}
Select the **star** next to the **valuable iterations** before completing a phase, even without review. This allows you to identify the **most valuable** **iterations** for that phase.
{% endhint %}

## How to log models to Vectice?

View our [How to log models](../../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-models.md) guide for more information on logging models during iterative development.
