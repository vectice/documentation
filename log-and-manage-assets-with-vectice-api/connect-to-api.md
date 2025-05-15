# Connect to API

## Install Vectice

Before installing Vectice, ensure you have the necessary dependencies.

For `Python` , you will need the following:&#x20;

1. `Python 3.8` version or greater.
2. To have `pip` installed.

For `R` , you will need to install and use the `reticulate` library.

{% tabs %}
{% tab title="Python" %}
```python
# Install the latest vectice package
pip install vectice

# Install a specific vectice version
pip install vectice==24.1

# You can chain multiple installations
pip install vectice["s3, gcs"]
```
{% endtab %}

{% tab title="R" %}
```r
# Step 1: Install reticulate if not already installed
install.packages("reticulate")

# Step 2: Install the latest version of Vectice
reticulate::py_install("vectice", pip = TRUE)

# Or install a specific version of Vectice
reticulate::py_install("vectice==<desired_version_number>", pip = TRUE)
```
{% endtab %}
{% endtabs %}

## Create an API key

The Vectice API seamlessly integrates with your favorite notebook or IDE, as well as popular AI tools, platforms, and frameworks. Once connected to the Vectice App using the Vectice API, you can continuously document assets, progress, and learnings.&#x20;

{% hint style="info" %}
Your API key is unique to you and should not be shared with your colleagues.&#x20;
{% endhint %}

**To create an API key:**

1.  Click on the **key icon** in the upper right corner of the Vectice app

    ![](../.gitbook/assets/api-key.png)
2. Select **Create API Key**
3. We recommend you download the key as a `JSON` file to have all of your necessary credentials.

<figure><img src="https://lh7-us.googleusercontent.com/slidesz/AGV_vUccF6DToMTgsxzg8MCgjoEMYhcpkHFFQ5EwbqpRusAldLYiSZ_M7pZDNeSbuImK44Htab4-tBVTDF3Af33NZxXnP2b8xG8XrnWJTtxwPz-7E97Xo6ARIFehcStbuD_9ZW74sx2yD-dUGXQHp-zniHHaXdMXq287=s2048?key=hHxk__FlAKgpd8LAD5j7GQ" alt=""><figcaption></figcaption></figure>

## What's next?

Use your API key to auto-document your work in the [**QuickStart project**](../quickstart/quickstart-auto-document-your-work.md).
