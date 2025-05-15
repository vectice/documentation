# Log MLFLow runs

Vectice provides an easy way to retrieve already saved information from your MLflow runs and document them into Vectice.

To log model information from `MLFlow` use the following lines of code:

```python
# Use the following model wrapper to retrieve your MLFlow run artifacts
model = Model.mlflow(run_id='your_run_id', client=mlflow, url='https://your_url.com')

# Log MLFlow artifacts in Vectice
iteration.log(model)
```

<table><thead><tr><th width="184.5">Parameter</th><th width="421">Description</th><th>Default</th></tr></thead><tbody><tr><td><code>run_id</code></td><td>A unique identifier for the MLflow experiment run.</td><td><em>required</em></td></tr><tr><td><code>client</code></td><td>The MLflow client object used for interacting with MLflow. This parameter is mandatory to ensure compatibility and avoid issues with specific configurations.</td><td><em>required</em></td></tr><tr><td><code>url</code></td><td>The URL to the<code>MLFlow</code> UI to access the run information.</td><td><em>optional</em></td></tr><tr><td><code>derived_from</code></td><td>List of datasets (or version ids) to link as lineage.</td><td><em>optional</em></td></tr></tbody></table>

You can access your MLFlow run artifacts in Vectice where you will see the model version metrics, properties, and a link to the MLFlow UI of your run.

Find this information by navigating to **Models** **>** **Select model name > Select version**.&#x20;

<figure><img src="../../.gitbook/assets/Screen Shot 2023-08-03 at 1.17.13 PM.png" alt=""><figcaption><p>MLFlow Model Version Metrics and Properties in the Vectice App</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/MLflow-blur.png" alt=""><figcaption><p>MLFlow UI URL Accessible in the Vectice App</p></figcaption></figure>
