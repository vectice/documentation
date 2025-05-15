# Log assets using Vectice IDs

Each asset within Vectice has a unique ID. These identifiers are permanent and unique inside the Vectice organization. That way, you can identify resources from the Vectice API and simplify collaboration amongst teammates by providing the IDs of assets.&#x20;

{% hint style="info" %}
Each asset has a three-letter prefix followed by an incrementing number. For example, **WSP-213**.
{% endhint %}

## Vectice IDs prefix

| Prefix  | Asset           |
| ------- | --------------- |
| **WSP** | Workspace       |
| **PRJ** | Project         |
| **PHA** | Phase           |
| **ITR** | Iteration       |
| **MDL** | Model           |
| **MDV** | Model version   |
| **DST** | Datasets        |
| **DSV** | Dataset version |

## Where can I find the Vectice IDs?

Vectice IDs can be found in the details sections of the Vectice app. They are also shown in the projects, phases, and asset pages list as well as inside each phase (Phase and Iteration IDs).

<figure><img src="../../.gitbook/assets/projectid (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/phaseid-in-docs.png" alt=""><figcaption></figcaption></figure>

## How can I access Vectice IDs via the API?

To find Vectice IDS **via the Vectice API**, use the list functions. You can then access workspaces, projects, phases, and assets from your working environment.&#x20;

```python
# Find Workspace IDs to select a specific Workspace
connect = vectice.connect(api_token="your-api-key") #Paste your API key
connect.list_workspaces()

# Find Project IDs inside of Workspace to retrieve a specific project
workspace = connect.workspace("WSP-123")
workspace.list_projects()

# Find Phase IDs to retrieve a specific phase
project = workspace.project("PRJ-1228")
project.list_phases()

# Find Iteration IDs to retrieve a specific iteration
phase = project.phase("PHA-120")
phase.list_iterations()
```

To find asset IDs for Dataset and Model, you must retrieve the IDs from the Vectice app.

## How to use Vectice IDs?

You can use Vectice IDs to:

* Retrieve workspaces, projects, phases, iterations, and assets in your working environment using the Vectice Python API
* Document phase updates and summaries with ease by identifying specific items using their Vectice ID
* Collaborate and communicate by sharing the Vectice ID you are referring to with your colleagues and stakeholders
