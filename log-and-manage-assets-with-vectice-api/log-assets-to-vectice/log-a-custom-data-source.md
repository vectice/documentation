---
description: Learn how to wrap datasets from a custom data source.
---

# Log a custom data source

To wrap data from any data source, create a custom resource class and inherit from the Vectice base`Resource` class. Then create a `_build_metadata()` and `_fetch_data()` method to collect metadata from your custom data sources.

## Custom resource example code

Below is a pre-built custom resource code example you could use to build your own data resource:

```python
from vectice import Resource, DatasetSourceOrigin, FilesMetadata

class MyCustomResource(Resource):
    _source_name = "Data source name"
    
    def __init__(
                self,
                paths: str | list[str],
            ):
                super().__init__(paths=paths)

    def _build_metadata(self) -> FilesMetadata:  # 
        files = ...  # fetch file list from your custom storage, retrieve them from self._paths
        total_size = ...  # compute total file size
        return FilesMetadata(
            size=total_size,
            origin=self._source_name,
            files=files,
            usage=self.usage,
        )

    def _fetch_data(self) -> dict[str, bytes]:
        files_data = {}
        for file in self.metadata.files:
            file_contents = ...  # fetch file contents from your custom storage
            files_data[file.name] = file_contents
        return files_data
```

From this point, you can use your custom resource class to wrap data from any data source (i.e., Redshift, RDS, Snowflake, etc).&#x20;

To learn how to log your dataset from your custom data source, view our [How to log datasets](log-datasets.md) guide.

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption><p>Filter Datasets by Data Source in the UI</p></figcaption></figure>
