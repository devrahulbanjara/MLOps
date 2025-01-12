# Data Versioning with DVC

## Why Do We Need Data Versioning?

When we work on machine learning (ML) projects, the process isn’t just about writing code. The pipeline typically looks like this:

1. **Data Ingestion:** Collecting and storing raw data.
2. **Data Preprocessing:** Cleaning and preparing the data for analysis.
3. **Feature Engineering:** Creating meaningful input features for the model.
4. **Feature Selection:** Choosing the most important features.
5. **Model Training:** Training the machine learning model using the prepared data.
6. **Model Evaluation:** Testing the trained model’s performance.

Each step involves data, and that data changes as you process it. For example:
- You start with raw data (data ingestion).
- After cleaning it (data preprocessing), it’s no longer raw.
- Feature engineering creates entirely new datasets.

These datasets are large, sometimes several gigabytes or more. Unlike code, which is a few kilobytes, storing and managing these large files is a challenge. Version control systems like Git are great for code but struggle with large files like datasets and models. This is where **DVC (Data Version Control)** comes in.

---

## What is DVC?

DVC is a version control system designed specifically for handling large datasets and machine learning pipelines. Think of it as Git for data, but with special tools to manage big files efficiently.

### Real-Life Example

Imagine you’re working on a project to predict house prices. The pipeline looks like this:
1. Raw data (`raw_data.csv`) is collected.
2. Preprocessed data (`preprocessed_data.csv`) is created.
3. A model (`house_price_model.pkl`) is trained.

Without DVC:
- You manually manage files, often forgetting which version of the dataset corresponds to which model.
- Your team spends hours figuring out why someone’s model doesn’t work with the new dataset.

With DVC:
- Each stage of your pipeline is versioned.
- You can switch between different dataset and model versions instantly.
- Everyone on the team has access to the same versions of data and models.

---

## Why Do We Need DVC?

### Problems Without DVC:
1. **Data Overwrites and Loss:**
   - Without proper versioning, it’s easy to overwrite your data accidentally or lose important versions of your datasets or models.
   - Example: You might clean your data but accidentally overwrite the original file. Later, you realize you need the raw data again but can’t retrieve it.

2. **No Traceability:**
   - Without DVC, there’s no easy way to know which version of your dataset or model was used to achieve a specific result.
   - Example: If a model performs exceptionally well, you might struggle to reproduce the results because you don’t know which version of the dataset or features was used.

3. **Storage Issues:**
   - Git stores all versions of files, and with large datasets, this quickly becomes impractical due to storage limitations.
   - Example: A single dataset could be 10GB, and every modification would duplicate that size in Git.

4. **Collaboration Problems:**
   - Sharing large files via email or cloud storage can be tedious and prone to errors.
   - Example: Team members working on different versions of the same dataset might create confusion.

---

### Benefits With DVC:
1. **Efficient Storage:**
   - DVC stores only the changes (not the entire file) and uses remote storage (like AWS S3, Google Drive, or even your local drive) to save large files.

2. **Reproducibility:**
   - DVC tracks which dataset and model versions were used at every stage of the ML pipeline. This makes it easy to reproduce results.

3. **Collaboration:**
   - DVC allows teams to share datasets and models without manually uploading and downloading files. It integrates seamlessly with Git.

4. **Traceability:**
   - You can easily switch between different versions of your data and models, just like you do with code in Git.

5. **Pipeline Automation:**
   - DVC can automate the entire ML pipeline, tracking dependencies between stages and ensuring consistency.

---

## How DVC Works (with Examples)

### Step 1: Install DVC
Install DVC in your environment:
```bash
pip install dvc
```

### Step 2: Initialize DVC
Inside your project directory, initialize DVC:
```bash
dvc init
```
This sets up DVC in your repository.

### Step 3: Add a Dataset
Suppose you have a dataset `data.csv` that you want to version. Add it to DVC:
```bash
dvc add data.csv
```
This does two things:
1. Tracks `data.csv` in DVC (instead of Git).
2. Creates a small `.dvc` file (e.g., `data.csv.dvc`) that points to your dataset.

Commit this `.dvc` file to Git:
```bash
git add data.csv.dvc .gitignore
```

### Step 4: Set Up Remote Storage
Set up a remote storage location for your data (e.g., Google Drive, AWS S3, or your local drive):
```bash
dvc remote add -d myremote <remote-storage-url>
```
Push your data to the remote storage:
```bash
dvc push
```

### Step 5: Reproducing Pipelines
Suppose you preprocess the data and generate a new file `cleaned_data.csv`. Add this to DVC as well:
```bash
dvc add cleaned_data.csv
```
Now, if another team member wants to reproduce your results, they can:
1. Clone the repository.
2. Pull the required data:
   ```bash
   dvc pull
   ```
3. Use the same data and models you used.

---

## Advanced DVC Features

### Managing ML Pipelines
DVC allows you to define and track your entire ML pipeline using `dvc.yaml` files. For example, your pipeline might look like this:

```yaml
stages:
  preprocess:
    cmd: python preprocess.py raw_data.csv cleaned_data.csv
    deps:
      - raw_data.csv
      - preprocess.py
    outs:
      - cleaned_data.csv

  train:
    cmd: python train.py cleaned_data.csv model.pkl
    deps:
      - cleaned_data.csv
      - train.py
    outs:
      - model.pkl
```
Run the pipeline with:
```bash
dvc repro
```
This ensures each stage runs in the correct order and only reruns stages when necessary (e.g., if the input data changes).

### Experiment Tracking
DVC can track multiple experiments:
```bash
dvc exp run
```
You can compare experiments, switch between them, and reproduce results easily.

### Metrics Tracking
Add metrics to track model performance:
```bash
dvc metrics add metrics.json
```
View metrics across experiments:
```bash
dvc metrics show
```

### Data and Model Sharing
Share data and models using remotes. Other team members can pull the exact same versions:
```bash
dvc push  # To upload
```
```bash
dvc pull  # To download
```

---

## Summary
DVC solves a critical problem in ML projects: managing and versioning large datasets and models. By integrating with Git, it ensures reproducibility, collaboration, and efficient storage.

With DVC, you can:
- Track your data and models seamlessly.
- Reproduce results with confidence.
- Collaborate with your team effortlessly.
- Automate and manage complex ML pipelines.

To get started, follow the steps above and explore advanced features like pipelines, experiment tracking, and metrics to bring your ML projects to the next level!

