# Preserve your code and asset lineage

Vectice captures, tracks, and visualizes the relationships between your data science assets—code, datasets, models, and artifacts—from origin to deployment. This ensures full transparency and traceability for better validation and collaboration.

{% embed url="https://youtu.be/6lG-pEWOVZ0?ref=0" %}

With automatic code capture from your Notebook via the Vectice API, you can preserve both version-controlled and local files. This simplifies model management and saves time by ensuring your code is documented from the start.

## How to preserve code and lineage

1. **Capture Code Automatically**
   * Use the Vectice API to automatically capture code directly from your Notebook.
   * Utilize the `code capture` variable for version-controlled files (e.g., Git or Databricks).
   * For local files, use the `code file capture` variable to track those as well.
2. **Maintain Code Traceability**
   * Your local files and Git repository can coexist in Vectice, ensuring complete traceability of your code.
   * This guarantees that the correct version of your code is always associated with your models.
3. **Document Code and Lineage**
   * While Vectice allows you to update code later within the app, automating the code capture process from the start saves time and effort.
   * Capturing both the source code and input lineage is crucial for documenting your models and building trust in your data science workflows.

## How to Find Your Code and Model Lineage in Vectice

To access your code and model lineage:

1. Go to your project and select the Datasets or Models tab
2. Select the desired asset and its version to view the corresponding lineage
3. Under **Lineage,** you can view the code and assets used for the asset
4. To edit the lineage in-app, select the **Edit Lineage** button and make changes
