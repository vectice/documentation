# Auto-document Models and Datasets with AskAI Prompts

**AskAI** empowers data scientists to generate clear, tailored documentation for iterations, models, or datasets with ease. Whether using the “Ask Me Anything” feature for custom prompts or documenting directly from your assets using Macros, AskAI ensures all key details are documented seamlessly—so you can focus on your work, not the paperwork.

{% embed url="https://youtu.be/4BzJPtITQD8?ref=0" %}

## AskAI Prompts

Below, we have crafted some basic prompts to get you started auto-documenting with AskAI.&#x20;

{% hint style="info" %}
To generate documentation based on your assets and phases, use AskAI's "Ask me anything" feature and use the `/`character to select the desired assets or phrases.
{% endhint %}

### Summarize model

The following AI prompt will summarize your model's technique, performance metrics and insert attachments.

{% code overflow="wrap" %}
```
Generate a summary of the model {{ MDV-163 }}. Explain the metrics and insert attachments related to performance.
```
{% endcode %}

**Prompt output:**

<figure><img src="../.gitbook/assets/askai2.gif" alt=""><figcaption></figcaption></figure>

### Compare models

The following AI prompt will generate a detailed comparison of multiple models, highlighting differences in technique, training data, and results.

{% code overflow="wrap" %}
```
Compare the following models {{ MDV-162 }} and {{ MDV-163 }}. Focus on differences in their techniques, training data, and performance outcomes.
```
{% endcode %}

**Prompt output:**

<figure><img src="../.gitbook/assets/askai11.png" alt=""><figcaption></figcaption></figure>

### Extract feature engineering from Datasets <a href="#h-1665" id="h-1665"></a>

Prompt to derive the feature engineering that happened between 2 datasets. The LLM will look at the distribution of the columns and all of the metadata and infer the feature engineering.

{% code overflow="wrap" %}
```
Explain what feature engineering and transformations that happened between those 2 datasets {{ DTV-358 }} and {{ DTV-370 }}. 
```
{% endcode %}

**Prompt output:**

<figure><img src="../.gitbook/assets/askai3.png" alt=""><figcaption></figcaption></figure>

### Extract feature engineering from Datasets with enriched iteration

Alternatively, you can provide more information to your Prompt to derive more based on iteration.

{% code overflow="wrap" %}
```
Explain what feature engineering and transformations that happened between those 2 datasets {{ DTV-358 }} and {{ DTV-370 }}. Based on this iteration {{ ITR-223 }}, go deeper in the feature engineering process and provide extensive detail about what happened. 
```
{% endcode %}

**Prompt output:**

<figure><img src="../.gitbook/assets/askai4.png" alt=""><figcaption></figcaption></figure>

## Advanced use cases: Analyze tables and CSV inside prompt

The following prompt allows you to pass a table or CSV file directly into the prompt, enabling AskAI to analyze and summarize the data seamlessly. This option is ideal for generating insights, summaries, or comparisons based on structured data.

{% hint style="info" %}
Use the "**/"** or "**."** character to effortlessly autocomplete prompts while typing, ensuring smooth and accurate asset integration.
{% endhint %}

<figure><img src="../.gitbook/assets/2025-01-22_13-05-34 (1).gif" alt=""><figcaption></figcaption></figure>

**Prompt output:**

<figure><img src="../.gitbook/assets/askai13.png" alt=""><figcaption></figcaption></figure>

## Macro Prompts

Alternatively, prompts can be found and inserted within macros. These prompts tend to be more intricate and often contain detailed expectations for the output, which are crucial for generating comprehensive documentation. Below are a few examples.

{% hint style="info" %}
You can customize and modify predefined Macro Prompts to align them with your specific needs and requirements.
{% endhint %}

### **Prompt 1** <a href="#h-1887" id="h-1887"></a>

This is the prompt inside the macro '**Model overview'**. These prompts are more complex and give you a predefined structure and tone of voice. Here, the prompt is just a standalone:

<figure><img src="../.gitbook/assets/askai5.png" alt=""><figcaption></figcaption></figure>

Once you run this macro, the results will look something like this:

<figure><img src="../.gitbook/assets/askai6.png" alt=""><figcaption></figcaption></figure>

### **Prompt 2** <a href="#h-1968" id="h-1968"></a>

This is the prompt inside the macro **'Model improvements'.** It combines the macrostructure and a prompt to allow you to analyze the differences between models more thoroughly.

<figure><img src="../.gitbook/assets/askai7.png" alt=""><figcaption></figcaption></figure>

Here are the results of running this Macro prompt:

<figure><img src="../.gitbook/assets/askai8.png" alt=""><figcaption></figcaption></figure>

### **Prompt 3** <a href="#h-2037" id="h-2037"></a>

This is the prompt inside the macro **'Model alternatives'**. As before, the advanced prompt can manage multiple model inputs.

<figure><img src="../.gitbook/assets/askai12.png" alt=""><figcaption></figcaption></figure>

The result of running this macro prompt:

<figure><img src="../.gitbook/assets/askai10.png" alt=""><figcaption></figcaption></figure>

Overall, AskAI combines ease of use with powerful prompts that you can customize, ensuring you can capture and communicate the value of your projects with minimal effort.
