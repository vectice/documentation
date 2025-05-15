# Streamline documentation with Macros

**Macros** offer an easy way to keep your documentation uniform and accessible, helping everyone stay on the same page. Macros use internal metadata to fill your reports with specific project information. You can create your own macros, and Vectice provides predefined macros.&#x20;

**Benefits of Macros**:

* Save time on routine documentation tasks
* Ensure consistency across projects and teams
* Reduce errors by pre-configuring fields and prompts

## 🧩 Available Pre-defined Macros

{% hint style="info" %}
You can easily create and customize your macros directly from the admin menu, customizing them to suit your specific needs.
{% endhint %}

Here are the main macros available in Vectice, each designed to meet different documentation needs:

### Asset Documentation Macros

Quickly document new assets with standardized fields for name, type, and description, ensuring all asset entries are clear and uniform.

{% hint style="info" %}
_<mark style="color:orange;">**Example Usage:**</mark>_ When a new data source is added to a project, use the "Data overview" macro to instantly capture a general summary of the new data.
{% endhint %}

#### Model Version Macros

<table><thead><tr><th width="260">Macro</th><th>Description</th><th data-hidden>Requirement</th></tr></thead><tbody><tr><td>Model version properties</td><td>Displays all properties of your model version.</td><td></td></tr><tr><td>Model feature importance</td><td>Displays a graph showing the importance of each feature in your model.</td><td></td></tr><tr><td>Model version summary</td><td>Provides a summary of your model's version.</td><td></td></tr><tr><td>Model version description</td><td>Displays the description of your model version.</td><td></td></tr><tr><td>Model version performance</td><td>Displays the performance metrics of your model.</td><td></td></tr><tr><td>Model version feature importance</td><td>Displays the graph showing the importance of each feature in your model version.</td><td></td></tr><tr><td>Model version comparison</td><td>Compares a model with the baseline or prior production model.</td><td></td></tr><tr><td>Model version alternative</td><td>Displays a summary table of the different model alternatives tested.</td><td></td></tr></tbody></table>

#### Dataset Version Macros

<table><thead><tr><th width="248">Macro </th><th>Description</th><th data-hidden>Requirement</th></tr></thead><tbody><tr><td>Dataset version overview</td><td>Provides a general summary of your dataset.</td><td></td></tr><tr><td>Dataset version columns description</td><td>Displays a table of your dataset's columns with key statistics.</td><td></td></tr><tr><td>Dataset version comparison</td><td>Compares a new dataset to a reference dataset.</td><td></td></tr><tr><td>Dataset version lineage comparison</td><td>Compares the evolution of a dataset to its input dataset within the lineage.</td><td></td></tr></tbody></table>

## General Macros

Use the general macro to capture key project details like objectives, timelines, team members, and phase-specific updates. It simplifies onboarding, keeps stakeholders informed, and ensures consistent, relevant updates throughout the project.

{% hint style="info" %}
_<mark style="color:orange;">**Example Usage:**</mark>_ At the start of the project documentation, use the Project Information Macro to set up the project’s essential information, ensuring everyone has a clear understanding of the project’s scope and goals.\

{% endhint %}

<table><thead><tr><th width="225">Macro</th><th>Description</th><th data-hidden>Requirement</th></tr></thead><tbody><tr><td>Project info</td><td>Inserts your project's details and description.</td><td></td></tr><tr><td>Project structure</td><td>Displays an overview of your project's structure.</td><td></td></tr><tr><td>Project title</td><td>Displays the title of your project.</td><td></td></tr><tr><td>Insert phase content</td><td>Inserts information from your project's phase documentation.</td><td></td></tr><tr><td>Project stakeholders</td><td>Displays your project and model stakeholders.</td><td></td></tr></tbody></table>

## Additional or Specific Macros

These macros offer specialized functionality for enhanced documentation.

<table><thead><tr><th width="245">Macro</th><th>Description</th><th data-hidden>Reqirements</th></tr></thead><tbody><tr><td>Model Development Document Header</td><td>Adds a structured header table to the model development document for organized reporting.</td><td></td></tr></tbody></table>

## Macro requirements

{% hint style="info" %}
**Note:** Some macros have requirements to work properly. For example, the "Insert phase content" macro requires content in the selected phase to display information.
{% endhint %}

Here are a few examples of macro requirements and tips to ensure you have the necessary information for proper macro use:

### Insert phase content

This Macro will insert specific phase documentation into your report.  To use this Macro, phase documentation is required. You can find the phase documentation within the `Documentation` tab of your phase.

<figure><img src="../.gitbook/assets/phase-documentation-loc.png" alt=""><figcaption></figcaption></figure>

### Project info

This Macro requires a project description. To add a description, go to your project settings and add a description.&#x20;

<figure><img src="../.gitbook/assets/proj-description-ss.png" alt=""><figcaption></figcaption></figure>

### Model intent&#x20;

To use this Macro, the Model of interest must include a description. You can add a Model description by selecting the **Models** tab, selecting your model, and then adding a description.

<figure><img src="../.gitbook/assets/model-des-ss.png" alt=""><figcaption></figcaption></figure>

### Model version summary

To use this Macro, the Model version must have properly updated information. To update your model page with the right info, select the **Models** tab, select a version, and edit the model page where needed.&#x20;

<figure><img src="../.gitbook/assets/model-edits-ss.png" alt=""><figcaption></figcaption></figure>

### Model properties

To use this Macro, the Model version must have properties logged to Vectice either through the API or within the Vectice app. Refer to our guide "[How to log models](../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-models.md)" for adding properties via the API.

### Model version description

To use this Macro, the Model version must have a description. To add a description, select the Models tab, choose your model, select a model version, and then add a description.

<figure><img src="../.gitbook/assets/mv-descr.png" alt=""><figcaption></figcaption></figure>

### Model performance

To use this Macro, the Model version must have metrics logged to Vectice either through the API or within the Vectice app. Refer to our guide "[How to log models](../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-models.md)" for adding metrics via the API.

### Model feature importance&#x20;

To use this Macro, the Model requires an upload of the feature importance graph to the Vectice app, or log it from the API. To add attachments via API, view our [Log attachments and notes](../log-and-manage-assets-with-vectice-api/log-assets-to-vectice/log-attachments-and-notes.md) guide.

{% hint style="info" %}
The API requires you to name the logged graph `feature_importance.png`.
{% endhint %}

To add a graph in the Vectice app, select the Models tab, pick your model and its version, and beside "Attachments" select the **Add** button.

<figure><img src="../.gitbook/assets/add-attmnts-model.png" alt=""><figcaption></figcaption></figure>
