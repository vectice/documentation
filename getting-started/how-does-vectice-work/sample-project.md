---
description: Understand how a Project is setup inside Vectice
---

# 2️⃣ Sample Project

To learn Vectice, we will do a sample project.

Imagine that you are a data scientist working at a large real estate company. You’ve been asked to find “that old house project,” another data scientist Albert worked on last year. Your business partner tells you that the new Census Bureau housing dataset is out, so we should retrain the model with it and improve the model. You’ve also been asked to check the data the model is trained on because nobody remembers. Your team wants you to document your work so they can understand it better next time.

From your personal Workspace, let’s open the “**Predicting house prices in King County, Washington**” project.

### **Project Overview**

In the Project Overview, you can immediately understand what the project is about, the progress of its milestones through the stages that are well documented, and on the right some details like the recent activity and the contributors that help find the right people to ask questions if you have any.

→ Click on the “Improved Modeling with decision tree” stage to view the documentation already produced by a colleague.

![](<../../.gitbook/assets/1 (1)>)

### **Project Stages**

Stages help data science teams and managers visually organize the project, enforce best practices, bring consistency, and capture knowledge. Since they're configurable, you can easily replicate your existing workflows or create new ones.

Here, we see the different stages of the project, and we can observe what work was done. For example, we see that Albert documented that he worked on two models: a Baseline model and an advanced model using a decision tree for better results.

With stages, you can:

* **Document** your work for yourself and others.
* Indicate **status** to communicate progress.
* **Reorganize** your stages using drag-and-drop to reflect the non-linear nature of data science work.
* View document **history**, see the changes done over time, and even restore to an earlier version.
* Mention and notify your teammates using the built-in **@mention** capabilities.

![](../../.gitbook/assets/2)

### **Datasets**

Datasets reflect the datasets used for analysis, cleaning, model training, and validation. You can register datasets from various source systems in the catalog along with their metadata. You can see the datasets in your Project on the Datasets tab.

![](<../../.gitbook/assets/3 (1)>)

### **Models**

Models represent the machine learning models created and trained during the modeling process, their hyper-parameters, and the metrics from the train-test process. You can have multiple versions for a model depending on the algorithms you use or even different hyperparameters.

<figure><img src="../../.gitbook/assets/4 (1)" alt=""><figcaption></figcaption></figure>

### **Runs**

Runs are just code executions captured in Vectice, which are essential to reproduce work for existing projects. Each run can have one or more input assets, code references, and output assets. Visit the Runs tab on the Project to see all the runs you have logged with Vectice.

![](<../../.gitbook/assets/5 (1)>)

Vectice has native integration with Git; thus, you can easily declare the code you’re using through the Vectice logging library. Click the code section on the run to view the commit on Github.

### **Navigation**

You can learn more about this project by going through the various stages that are well-documented. Click the widgets present inside the documentation to see the different project assets.

Use the breadcrumbs at the top to navigate through the various Workspaces, Projects, and assets like Datasets and Models.

![](../../.gitbook/assets/6)

### **Next Step**

Now that you’ve figured out how to navigate the Vectice web interface, it’s time for us to get started on the API interface.
