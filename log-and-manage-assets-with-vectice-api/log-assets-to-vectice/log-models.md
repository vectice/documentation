# Log models

The Vectice API enables you to log all models used during development to the Vectice app. To log your model's data and supporting artifacts, use the following `Model` method to declare your model.

<pre class="language-python"><code class="lang-python">from vectice import Model

<strong>model = Model(name, library, technique, metrics, predictor, attachments)
</strong></code></pre>

Once your model is declared, log the model's artifacts to vectice:

```python
iteration.log(model)
```

## Example

Below is a full example showcasing the concepts mentioned above.

<pre class="language-python" data-overflow="wrap"><code class="lang-python">import vectice
from vectice import Model, Metric
from sklearn import ...

# Connect to Vectice
connect = vectice.connect(
    api_token = 'your-api-key',        # Paste your api key
    host = 'https://app.vectice.com',  # Paste your host
)

# Retrieve the project phase to begin the model development  
phase = connect.phase("PHA-XXX")

# Initialize iteration
iteration = phase.create_or_get_current_iteration()

# Model artifacts
<strong>model_name = "your-model-name"
</strong>model_library = "sklearn"
model_technique = "clustering"
model_metrics = [Metric("RMSE", 153), Metric("Clusters number", 5)]
model_predictor = my_sklearn_predictor
model_attachments = ["attachment1.png", "attachment2.png" ]

# Declaring your model and its artifacts
model = Model(name=model_name, library=model_library, technique=model_technique, metrics=model_metrics, predictor=model_predictor, attachments=model_attachments)

# Log the model to Vectice
iteration.log(model)
</code></pre>

For an in-depth example, view the code example found in the [Iterative Development](../../glossary/concepts/iterations/iterative-development.md#full-workflow-example) guide.
