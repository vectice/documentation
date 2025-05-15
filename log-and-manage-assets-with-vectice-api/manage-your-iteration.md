# Manage your iteration

Once you start logging assets, you can manage them seamlessly through the API or the app to keep your data science projects organized.

## Update iteration status

{% tabs %}
{% tab title="Vectice API" %}
Once you start an iteration in the API, its status automatically changes to "In progress." Once you are complete, you can update your iteration status by marking it complete.&#x20;

{% hint style="info" %}
Once an iteration is complete, you cannot reorganize the assets in the App. To reorganize, change the iteration status back to **In Progress** in the app.
{% endhint %}

{% code fullWidth="true" %}
```python
iteration.complete()
```
{% endcode %}

Full example:

```python
import vectice
from vectice import Model

connect = vectice.connect(api_token="your-api-key") #Paste your API key

# Connect to your project phase using your phase ID
phase = connect.phase("PHA-XXX") #You can fetch the relevant phase ID from your chosen Vectice project in the app.

# Create or get an iteration
iteration = phase.create_or_get_current_iteration()

# Define your model for logging to Vectice
model = Model(metrics, properties, attachments, predictor)

# Log your model to Vectice under the 'Model Used' section.
iteration.log(my_model, section="Model Used")

# Iteration is completed
iteration.complete()
```
{% endtab %}

{% tab title="Vectice Web App" %}
To update an iteration in the Vectice Web App

1. Go to your phase iteration
2. Select the dropdown under **Iteration status**
3. Choose your updated status

<figure><img src="../.gitbook/assets/iter-status.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Create sections

Sections in Vectice function like headers, helping you identify and organize assets. This improves how you access and manage datasets, models, notes, and graphs within your projects.

{% tabs %}
{% tab title="Vectice API" %}
To define a section to organize your assets using the Vectice API...

```python
# import and connect to Vectice
import vectice
from vectice import Model

connect = vectice.connect(api_token="your-api-key") #Paste your API key

# Connect to your project phase using your phase ID
phase = connect.phase("PHA-XXX") #You can fetch the relevant phase ID from your chosen Vectice project in the app.

# Create or get an iteration
iteration = phase.create_or_get_current_iteration()

# Define your model for logging to Vectice
model = Model(metrics, properties, attachments, predictor)

# Define a section by using the 'section' param and assigning a name
# to log your model to Vectice under the 'Model Used' section.
iteration.log(my_model, section="Model Used")
```
{% endtab %}

{% tab title="Vectice Web App" %}
To define a section to organize your assets inside the Vectice Web App...

1. Go to your selected Project and Phase
2. Select the Iteration that has the assets you want to organize
3. Click **Create section**&#x20;
4. Once the section is created, drag and drop your assets to the correct section

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Delete Sections

You can delete sections in the **Web App** by selecting the menu button next to the section name and selecting **Delete Section**. If this section has assets, they will be moved to the default section for unassigned assets.

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

## Move assets across sections in App

{% hint style="info" %}
You can customize sections to fit your unique needs (e.g., organize assets, outline your workflow, etc.).
{% endhint %}

Drag and drop assets between sections to rearrange them as you like.

## Delete assets in a section

{% tabs %}
{% tab title="Vectice API" %}
You can delete assets within a specified section of the iteration using the API:

```python
iteration.delete_assets_in_section(section="Collect Initial Data")
```
{% endtab %}

{% tab title="Vectice Web App" %}
You can delete assets within a specified section of the iteration in the Web App by

1. Go to your phase iteration and identify the section
2. Select one or more of the assets you want to delete
3. Click the **Delete assets**&#x20;
{% endtab %}
{% endtabs %}

## Create Notes&#x20;

Add notes directly to your iteration for more context.

{% tabs %}
{% tab title="Vectice API" %}
To add a note via Vectice API, use the following `log()` method and insert your note.

`iteration.log("This is my note.")`

Full example:

```python
from vectice import Model
my_model = Model(name="my_model")
iteration.log(my_model)
iteration.log("Testing this new linear regression model.")
```
{% endtab %}

{% tab title="Vectice Web App" %}
Inside the Web App, to add a note to your iteration:

1. Go to your phase iteration
2. Select **Create note**

<figure><img src="../.gitbook/assets/create note.png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

## Star your favorite iterations

Star the iterations you want to highlight to make them stand out, making it easier for stakeholders to identify the top iterations.

<figure><img src="../.gitbook/assets/star-iteration.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/star-2.png" alt=""><figcaption></figcaption></figure>

