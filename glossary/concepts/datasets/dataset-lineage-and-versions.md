# Dataset lineage and versions

## Dataset lineage

To keep track of your derived datasets lineage, use the `derived_from` parameter to list the datasets (or dataset IDs) from which your dataset is derived.

```python
from vectice import Dataset, FileResource

origin_dataset = Dataset.origin(
    name="my origin dataset",
    resource=FileResource(paths="origin.csv"),
)

clean_dataset = Dataset.clean(
    name="my clean dataset",
    resource=FileResource(paths="clean_dataset.csv"),
    derived_from= [origin_dataset]
)
```

## Dataset versions

**Dataset versions** are datasets with the same name as another dataset that you have already logged in Vectice. Logging datasets with the same name automatically increment the versions, maintaining the dataset's history.

<figure><img src="../../../.gitbook/assets/ds-versions.png" alt=""><figcaption></figcaption></figure>
