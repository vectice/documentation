# Datasets

Datasets reflect the dataset metadata logged to Vectice during model development.

{% hint style="info" %}
**Please note that Vectice does not store your actual datasets.**&#x20;

Vectice documents dataset metadata like origin, version, and artifacts from various sources, while automatically managing dataset versions for lineage tracking.
{% endhint %}

The Vectice API enables you to log all dataset artifacts used during development to the Vectice app, including your **origin**, **cleaned**, and **modeling datasets.**

| Dataset type      | Description                                                                                                             |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Origin datasets   | Origin datasets refer to your datasets containing **raw data**.                                                         |
| Cleaned datasets  | Cleaned datasets refer to your datasets that have been **cleaned and prepared for data modeling** or **data analysis**. |
| Modeling datasets | Modeling datasets combine **training**, **testing**, and **validating** data in a single dataset.                       |

## Things you should know

* Data scientists can capture basic statistics when logging their datasets' artifacts to Vectice. These statistics include the mean, median, variance, quartiles, and more. Learn more by viewing our [Capturing Dataset Statistics](../../../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-datasets.md#capturing-dataset-statistics) section.

## Datasets best practices

* Logged datasets should have the dataset types **Origin**, **Cleaned**, and **Modeling** appended to the end of the corresponding dataset name for easy identification in the Vectice app.
* Create a phase with the **primary objective** of origin datasets registration. This is usually included in the **Data Preparation** phase of a CRISP-DM project.&#x20;
* Project phases that aim to clean and process raw data can have a requirement that ask members to log the **cleaned datasets**. This is typically completed in the **Data Preparation** phase of a CRISP-DM project.
* Mark your **most valuable iterations and assets** in the Vectice app by selecting the **star** next to the corresponding iteration and assets **before** beginning the phase review. This will make it easier for stakeholders and subject matter experts to identify the iterations and assets in review.

### Advanced Dataset guides

* [Dataset resources](dataset-resources.md)
* [Dataset properties](dataset-properties.md)
* [Dataset lineage and versions](dataset-lineage-and-versions.md)

{% hint style="info" %}
Select the **star** next to the **valuable iterations** before completing a phase, even without review. This allows you to identify the **most valuable** **iterations** for that phase.
{% endhint %}

## How to log datasets to Vectice?

Logging datasets is your first step to knowledge capture in Vectice. You can log all datasets used during development, including your **origin datasets** (raw datasets), **cleaned datasets**, and **modeling datasets**.&#x20;

View our [How to log datasets](../../../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-datasets.md) guide for more information on how to log datasets during iterative development.
