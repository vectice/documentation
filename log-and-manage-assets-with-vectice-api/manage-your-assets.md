# Manage your assets

Efficiently manage your AI project assets to ensure your data is organized, accessible, and up-to-date.

## Update model status via API

You can update your model status to`PRODUCTION`, `EXPERIMENTAL`, `RETIRED`, or `STAGING`.&#x20;

{% hint style="info" %}
You will receive an error message if you use a status outside the options mentioned above.
{% endhint %}

{% tabs %}
{% tab title="Vectice API" %}
To update a model status using the Vectice API...

```python
import vectice

# Connect to Vectice
connect = vectice.connect(
    api_token = 'your-api-key',        # Paste your api key
    host = 'https://app.vectice.com',  # Paste your host
)

# Retrieve your model version using the model version ID
mdv = connect.browse('MDV-XXX')

# Update your model status
mdv.update(status="PRODUCTION")
```
{% endtab %}

{% tab title="Vectice Web App " %}
To update a model status in the Vectice Web App...

1. Go to your project and select **Models**&#x20;
2. Choose the model that needs a status update
3. Select a model version
4. Update the **Model version status**

<figure><img src="../.gitbook/assets/Screenshot 2024-06-11 at 10.05.53 AM.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}
