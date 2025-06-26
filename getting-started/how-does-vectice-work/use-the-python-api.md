---
description: Work on a sample project inside Vectice
---

# 3️⃣ Use the Python API

Vectice provides a Python API to integrate with your code so that you can log all your project milestones within Vectice from the environment of your choice.

To visit the API documentation, click [here](../../api-docs.md).

### Install Vectice <a href="#qitiz43tthph" id="qitiz43tthph"></a>

Before we get started, we need to install vectice. For this tutorial, we will use the GitHub flavor of Vectice. We are using pip to install Vectice.

```python

pip install vectice[github]

```

To learn how to install the Python API, click [here](../install-vectice-library.md).

### Log In <a href="#l0qtldumtq9e" id="l0qtldumtq9e"></a>

Now that we’ve installed the library, let’s log in to Vectice. You need the following:

* **API Endpoint**: This is usually the same as the one you use for the web UI.
* **API Token**: You can generate your API token from the Vectice UI from your profile page, which is accessible from the top-right corner of the web UI.
* **Project Id**: The project you want to use. You can find it from the Project Settings page in the Web UI.

```python

#Import the required packages
from vectice import Vectice
from vectice import Experiment
import os

os.environ['VECTICE_API_ENDPOINT']= "app.vectice.com"
os.environ['VECTICE_API_TOKEN'] = "API TOKEN"
Project_id = Project ID

# Initialize the Project
project = Vectice(project = Project_id )

```

### Create Your First Experiment <a href="#lduqp31555om" id="lduqp31555om"></a>

Now that you’ve logged in let’s create your first experiment. An experiment in Vectice groups multiple runs of any type like Modeling. They represent the metadata that you log to Vectice for a given job.

Each execution of an experiment is called a run, beginning when you start a tracked experiment with experiment.start() and ending when you stop the experiment with experiment.complete().

Every run has one or more inputs and outputs. The inputs can be code, dataset, and model versions, and the outputs can be dataset and model versions.

By default, every artifact used before experiment.start() is considered as an input of the run, and every artifact added between experiment.start() and experiment.complete() is considered as an output. However, you can still declare your run's inputs when starting it.

```python
# Import the job type enum
from vectice.api.json import JobType

experiment = Experiment(job = "Modeling", 
                                project = Project_id, 
                                job_type = JobType.TRAINING,
                                auto_code = True)

```

{% hint style="info" %}
Setting the <mark style="color:red;">`auto_code=True`</mark> lets you automatically log the code version into the Run if you are using Jupyter notebook and have a .git folder configured where you have your notebook. You may use the <mark style="color:red;">`experiment.add_code_version`</mark> method if you wish to do this manually.
{% endhint %}

### Create a New Dataset <a href="#id-3up2ziolpy41" id="id-3up2ziolpy41"></a>

The sample project already has all the required datasets. However, you may create a new dataset by importing data into Vectice from GCS, S3, or BigQuery. Let’s take an example of how to register a dataset from GCS.

For this, you need

* **Account key**: This Google Cloud Service account key is used to authenticate your access to Google Cloud Storage. You will be able to download this as a JSON file.
* **URI**: The URI of the folder/file you intend to use. This is the URI you get when you select the file/folder in Google Cloud Storage.

```python

import os

os.environ["GOOGLE_APPLICATION_CREDENTIALS"] = "readerKey.json"
uri = "vectice_tutorial/kc_house_data_cleaned.csv"
input_ds = experiment.vectice.create_gcs_dataset(uri=uri, name = "Cleaned data")

```

{% hint style="success" %}
Vectice API will use the credentials to connect to GCS to retrieve the data and then register the dataset along with the associated metadata. The credentials are **NOT** stored inside Vectice.
{% endhint %}

Once you log this, you will be able to see a new dataset in the Datasets tab of the Project. Click on it and see the details of this dataset.

### Create a Model Version <a href="#eknt21e9lz75" id="eknt21e9lz75"></a>

We already have a model registered a model in the Project. Now, let’s add a new version to it. Here we assume that you have already built a Random Forest model and have the errors calculated.

```python

experiment.start(inputs = [input_ds], run_properties = {"Technique": "RF"})

RMSE = 96000
experiment.add_model_version(model = "Regressor",
                                algorithm = "Random Forest",
                                metrics = {"RMSE": RMSE},
                                hyper_parameters = {"tree_depth": 6})

```

After this run, you can see that a new model version has been added. To the existing model Regressor. If you do not have a model of the said name, Vectice will create a new one for you.

### Complete Your Experiment <a href="#q0zh8nnt0xhz" id="q0zh8nnt0xhz"></a>

Vectice lets you document your work from the API without leaving your notebook.

{% hint style="info" %}
You can either add documentation manually or use the <mark style="color:red;">`document_run()`</mark> method to automatically add documentation about your run to your project’s documentation.
{% endhint %}

```python

experiment.document_run(name = "Remodeling")
experiment.complete()

```

This will automatically log every artifact you created after starting the run into the mentioned project stage.

### Document Your Conclusions <a href="#w6jev8s0pqpk" id="w6jev8s0pqpk"></a>

Let’s skip ahead and assume that you’ve completed the modeling work and reached some conclusions based on the experiments. The next step is to document them - you can do it right from your notebook.

First, let’s get to the stage where we want to provide updates.

```python

stage = experiment.vectice.get_stage(stage = "Remodeling")

```

Next, we add our conclusion to the stage. Anything we add gets appended to the existing content; you do not have to worry about erasing or losing existing work.

{% code overflow="wrap" %}
```python

stage.add_block(text = "Conclusion")
stage.add_block(text = "We successfully captured our input dataset and output model version and documented them.")

```
{% endcode %}

And finally, let’s move the stage to completed status to let others know that your work is complete.

```

from vectice.api.json import StageStatus
experiment.vectice.update_stage(stage="Remodeling", status=StageStatus.Completed)

```

Now you may use the web UI to check these changes and see how they have been documented!&#x20;

:tada:Congratulations, you've successfully completed the tutorial!&#x20;
