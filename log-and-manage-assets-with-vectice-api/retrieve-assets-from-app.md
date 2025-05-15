# Retrieve assets from app

Learn how to effortlessly retrieve your assets from the Vectice app using the Vectice API.&#x20;

## Retrieve dataset version metadata from app

After logging your datasets to Vectice, you can retrieve the dataset's metadata using the following code which will return a `Dataset Version Representation`.

A `Dataset Version Representation` shows information about a specific version of a dataset from the Vectice app. It makes it easier to get and read this information through the API.

{% hint style="info" %}
A dataset version ID starts with 'DTV-XXX'. Retrieve the ID in the Vectice App, then use the ID with the following methods to get the dataset version:

`connect.dataset_version(`'DTV-XXX'`)` or `connect.browse(`'DTV-XXX')
{% endhint %}

```python
import vectice
connect = vectice.connect(
    api_token = 'your-api-key',        # Paste your api key
    host = 'https://app.vectice.com',  # Paste your host
)

# Retrieve a specific dataset version metadata
connect.dataset_version('DTV-XXXX')
```

For more information on return values and other associated methods, view the [Dataset Version Representation API documentation](https://api-docs.vectice.com/reference/vectice/representation/datasetversionrepresentation/).&#x20;

## Retrieve model version metadata from app

After logging your models to Vectice, you can retrieve the model's metadata using the following code which will return a `Model Version Representation`.

A `Model Version Representation` shows information about a specific version of a model from the Vectice app. It makes it easier to get and read this information through the API.

{% hint style="info" %}
A model version ID starts with 'MDV-XXX'. Retrieve the ID in the Vectice App, then use the ID with the following methods to get the model version:

`connect.model_version(`'MDV-XXX'`)` or `connect.browse(`'MDV-XXX')
{% endhint %}

```python
import vectice
connect = vectice.connect(
    api_token = 'your-api-key',        # Paste your api key
    host = 'https://app.vectice.com',  # Paste your host
)

# Retrieve a specific model version metadata
connect.model_version('MDV-XXXX')
```

For more information on return values and other associated methods, view the [Model Version Representation API documentation](https://api-docs.vectice.com/reference/vectice/representation/modelversionrepresentation/).&#x20;
