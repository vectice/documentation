# Log custom metadata in a table format

A Vectice `Table` wraps a pandas dataframe into a table format, which you can then log to a Vectice iteration. This enables you to log custom metadata to Vectice in a tabular format.&#x20;

{% hint style="warning" %}
You should not use `Table` to store important or sensitive information. `Table` is for storing low sensitive information that may support your documentation efforts.
{% endhint %}

For example, if you wish to log a few rows of additional low sensitive information not captured in the dataset, you can utilize `Table` to log and document them into Vectice. See below for a code example:

```python
import pandas as pd
from vectice import Table

table_dict = {
    "inputs": ["What is Vectice?", "Describe a dog to me"],
    "outputs": ["Vectice is an auto-documentation platform", "A dog is an animal with four legs"],
    "toxicity": [0.0, 0.0],
}

prompt_data_input_output = pd.DataFrame(table_dict)

table = Table(prompt_data_input_output, name="prompt_data")
iteration.log(table)
```

{% hint style="info" %}
`Table()`has a maximum capacity of 100 rows and 20 columns.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2024-04-02 at 1.56.15 PM.png" alt=""><figcaption></figcaption></figure>
