---
description: Setup your environment to work with Vectice
---

# 📥 Install Vectice Library

With Vectice, Data Scientists can capture the key milestones of the initiative they're working on without leaving their favorite notebook. To facilitate this, Vectice provides a Python API library. The Vectice Python API is available through [PyPI](https://pypi.org/project/vectice/).&#x20;

Before we install Vectice, let's make sure that you have the necessary dependencies:&#x20;

1. You have Python 3.7.1+&#x20;
2. You have pip installed.

Depending on your operating system open a terminal or command line and run this command:

```python
pip install vectice
```

{% hint style="info" %}
**Note**\
The above line installs the latest version of Vectice published in PyPI.&#x20;

To install a specific version, specify the version number like this: <mark style="color:red;">`pip install vectice==version number`</mark>. You can find all the Vectice versions [`here`](https://pypi.org/project/vectice/#history).
{% endhint %}

### Extras

Some integrations require extras to be installed with the Vectice Python API. For example, using Gitlab would require <mark style="color:red;">`pip install vectice[gitlab]`</mark>. It’s possible to chain multiple extras by using the following notation.

```python
pip install vectice "[gitlab, github]".
```

The supported options are:&#x20;

* `mlflow` : \[”mlflow”]
* `git` : \[”GitPython”]
* `github` : \[”PyGithub”]
* `bitbucket` : \[”atlassian-python-api”]
* `gitlab` : \[”python-gitlab”]
* `pandas` : \[”pandas”]
* `jupyter` : \[”jupyter\_core”, “ipykernel”, “traitlets”]
* `collab` : \[”oauth2client”, “GitPython >= 3.1.14”]
* `bigquery` : \[”google-cloud”, “google-cloud-bigquery”]

Now that we have installed Vectice, let's start capturing the key milestones for a sample Project.&#x20;
