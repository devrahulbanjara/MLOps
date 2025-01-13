# Data Versioning with DVC

## Introduction
Data versioning is a crucial practice in machine learning (ML) projects. Unlike traditional software development, ML involves working with datasets that evolve throughout the development lifecycle. These datasets can be enormous, making it challenging to manage and track them effectively using traditional version control systems like Git.

In this guide, we will explore how **DVC (Data Version Control)** can simplify data versioning and ensure reproducibility in ML projects. By the end, you'll have a thorough understanding of DVC, including a practical, step-by-step tutorial.

---

## Why Do We Need Data Versioning?
When working on ML projects, the pipeline typically looks like this:

1. **Data Ingestion:** Collecting and storing raw data.
2. **Data Preprocessing:** Cleaning and preparing the data for analysis.
3. **Feature Engineering:** Creating meaningful input features for the model.
4. **Feature Selection:** Choosing the most important features.
5. **Model Training:** Training the machine learning model using the prepared data.
6. **Model Evaluation:** Testing the trained model’s performance.

Each step involves data, and that data changes as you process it. For instance:
- Raw data is collected during the ingestion phase.
- Preprocessing modifies the raw data into a cleaned version.
- Feature engineering generates new datasets.

Managing these datasets is a challenge due to their size and complexity. Traditional version control systems like Git are great for tracking code but struggle with large files like datasets and models. This is where **DVC** excels.

---

## What is DVC?
DVC is a version control system tailored for large datasets and machine learning pipelines. Think of it as Git for data, but with specialized tools to manage big files efficiently. DVC integrates seamlessly with Git, enabling you to version control both your code and data.

### Real-Life Analogy
To understand DVC better, consider this example:

Imagine you have a few items: a watch, a phone, a wallet, and a pair of shoes. The first three items are small and can be stored together. However, the shoes are large and need to be stored separately. To keep track:
- You place the watch, phone, and wallet together in one location.
- You write down the location of the shoes on a piece of paper and keep it with the other items.

When you need your belongings, you first retrieve the smaller items and the paper with the shoes’ location. Then, you fetch the shoes using the information on the paper.

In this analogy:
- The small items represent code files.
- The shoes represent a large dataset.
- The piece of paper is similar to a `.dvc` file, which tracks the location of the dataset.

DVC works in a similar way: Git stores the small code files and the `.dvc` file, which contains the location of the dataset.

---

## How to Use DVC
Here is a step-by-step guide to using DVC in a local repository:

### Step 1: Set Up Your Project
1. **Create a Local Repository:**
   Start by creating a new folder for your project and initializing it as a Git repository.
   ```bash
   mkdir my_project
   cd my_project
   git init
   ```
   This creates an empty Git repository in your project folder.

2. **Add a Python Script:**
   Create a file named `code.py` with some code that generates a CSV file. For instance, the script might create a `data.csv` file in a folder named `data/`:
   ```python
   import os
   import pandas as pd

   os.makedirs("data", exist_ok=True)
   df = pd.DataFrame({"A": [1, 2, 3], "B": [4, 5, 6]})
   df.to_csv("data/data.csv", index=False)
   ```

3. **Track Changes with Git:**
   Add and commit the script to your repository:
   ```bash
   git add .
   git commit -m "Initial commit with code and data script"
   ```

### Step 2: Install and Initialize DVC
1. **Install DVC:**
   Use pip to install DVC in your environment:
   ```bash
   pip install dvc
   ```

2. **Initialize DVC in Your Project:**
   Run the following command to initialize DVC in your repository:
   ```bash
   dvc init
   ```
   This creates a `.dvc` folder to store DVC metadata and a `.dvcignore` file to specify files that DVC should ignore.

3. **Commit the Changes:**
   Track the changes made by DVC:
   ```bash
   git add .
   git commit -m "Initialize DVC"
   ```

### Step 3: Add a Remote Storage
1. **Simulate Remote Storage:**
   Create a folder named `S3` to simulate remote storage:
   ```bash
   mkdir S3
   ```

2. **Add the Remote to DVC:**
   Link the simulated remote storage to your project:
   ```bash
   dvc remote add -d myremote S3
   ```
   The `-d` flag sets this remote as the default.

3. **Commit the Changes:**
   Track the changes made to the DVC configuration:
   ```bash
   git add .
   git commit -m "Add remote storage for DVC"
   ```

### Step 4: Track Your Dataset with DVC
1. **Add the Dataset to DVC:**
   Use DVC to track the dataset generated by your script:
   ```bash
   dvc add data/
   ```
   This creates a `.dvc` file for the `data/` folder, storing its metadata and location.

2. **Stop Git from Tracking the Dataset:**
   If Git is already tracking the `data/` folder, you’ll see an error. To resolve this, untrack the folder:
   ```bash
   git rm -r --cached data
   git commit -m "Stop tracking data folder with Git"
   ```

3. **Re-add the Dataset to DVC:**
   Run the `dvc add` command again to ensure the dataset is tracked by DVC:
   ```bash
   dvc add data/
   ```

4. **Push the Dataset to Remote Storage:**
   Commit the changes to DVC and Git, and push the dataset to the remote storage:
   ```bash
   dvc commit
   dvc push
   git add .
   git commit -m "Track dataset with DVC"
   git push
   ```

### Step 5: Update the Dataset and Version It
1. **Modify the Dataset:**
   Add a new row to the dataset by running the script again or manually editing the `data.csv` file.

2. **Check DVC Status:**
   Check which files have changed:
   ```bash
   dvc status
   ```

3. **Commit the Changes:**
   Save the updated dataset:
   ```bash
   dvc commit
   dvc push
   git add .
   git commit -m "Update dataset version"
   git push
   ```

### Step 6: Roll Back to a Previous Version
1. **Checkout an Older Commit:**
   Use Git to move to an earlier version of your code:
   ```bash
   git checkout <commit_hash>
   ```
   The dataset will still reflect the latest version.

2. **Pull the Older Dataset Version:**
   Retrieve the corresponding dataset version:
   ```bash
   dvc pull
   ```

3. **Return to the Latest Version:**
   Move back to the latest version of your code and dataset:
   ```bash
   git checkout main
   dvc pull
   ```

---

## Benefits of Using DVC
- **Reproducibility:** Easily reproduce experiments by versioning datasets and models.
- **Collaboration:** Team members can access the same versions of datasets and pipelines.
- **Efficiency:** Manage large files without overloading your Git repository.

---

## Conclusion
DVC bridges the gap between data management and version control, making it an essential tool for machine learning projects. By following the steps outlined in this guide, you can efficiently manage datasets, ensure reproducibility, and collaborate seamlessly with your team.

