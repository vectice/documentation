# Autolog your assets

You can auto-document all your assets used in your IDE or notebook environment with a single line of code. Start by importing and configuring the `autolog` vectice package:

{% hint style="info" %}
Autolog must be configured at the beginning of your notebook to capture all relevant information.
{% endhint %}

```python
from vectice import autolog

autolog.config(
    api_token = 'your-api-key',       # Paste your api key
    host = 'https://app.vectice.com', # Paste your host
    phase = 'PHA-XXX'                 # Paste your Phase Id
)
```

Develop your model as you normally would. Once you are ready to log your data science work and assets, use the following line of code to log all of your current assets and work to the Vectice app:

```python
autolog.notebook()
```

For more information, view our [Autolog API reference](https://api-docs.vectice.com/reference/vectice/autolog/).
