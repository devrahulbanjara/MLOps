# Experiment Tracking - A Complete Guide

## Table of Contents
1. Introduction
2. Why Experiment Tracking Matters
3. What Happens If We Don’t Track Experiments?
4. Traditional Approach vs. Modern Experiment Tracking
5. Introduction to MLflow for Experiment Tracking
6. Setting Up MLflow (Localhost and Remote Server)
7. Logging Experiments in MLflow (Manual vs. Auto-Logging)
8. Comparing Experiments in MLflow
9. Hyperparameter Tuning with MLflow
10. Advanced Features: Model Registry and Deployment
11. Limitations of MLflow
12. Best Practices for Experiment Tracking
13. Conclusion

---

## 1. Introduction
Machine learning involves running multiple experiments to find the best model. However, keeping track of these experiments manually can be challenging. Each experiment might have different hyperparameters, datasets, and configurations. Without a proper tracking system, it becomes difficult to understand what worked and what didn't.

This guide is designed for absolute beginners. We will explain everything from why tracking is essential to how MLflow, a powerful experiment tracking tool, makes it easy. We will cover step-by-step instructions, detailed explanations of each feature, and practical examples.

## 2. Why Experiment Tracking Matters
Experiment tracking is essential in machine learning because:
- **Prevents Repetitive Work:** Without tracking, you may waste time rerunning experiments you have already conducted.
- **Ensures Reproducibility:** You can recreate past results with the same settings.
- **Improves Collaboration:** Teams can share experiment details without confusion.
- **Helps Compare Models:** You can evaluate different models easily.

**Example:**
Imagine training a model with a learning rate of 0.01 and getting 90% accuracy. Later, you tweak the model but forget the original setting. Without tracking, you lose valuable insights.

## 3. What Happens If We Don’t Track Experiments?
If you do not track your experiments, you may face several challenges:
- **Inconsistent Results:** You may get different results each time and not know why.
- **Time Wasted:** You might repeat unsuccessful experiments instead of learning from them.
- **Difficult Debugging:** When a model fails, you won’t have previous records to analyze.
- **Poor Collaboration:** Your teammates won’t understand what changes you made to the model.

## 4. Traditional Approach vs. Modern Experiment Tracking

### **Manual Tracking (Using Excel, Notepad, etc.)**
Traditionally, many data scientists used spreadsheets to record experiments. 

#### **Example of a Spreadsheet:**
| Experiment | Model | Learning Rate | Batch Size | Accuracy |
|------------|--------|--------------|------------|---------|
| Exp1      | RandomForest | - | - | 85% |
| Exp2      | CNN   | 0.01 | 32 | 90% |

#### **Problems with this approach:**
- **Difficult to manage** when there are hundreds of experiments.
- **No automation**, meaning everything has to be entered manually.
- **Difficult to compare** past results effectively.

### **Modern Approach (Using MLflow)**
MLflow is an automated experiment tracking tool that stores details in a structured way.

## 5. Introduction to MLflow for Experiment Tracking
MLflow is an open-source platform for managing machine learning experiments. It helps in:
- **Logging experiments automatically.**
- **Storing hyperparameters, metrics, and model versions.**
- **Comparing different experiments in a user-friendly dashboard.**

## 6. Setting Up MLflow (Localhost and Remote Server)

### **Setting Up MLflow Locally**
To install MLflow, open your terminal and run:
```bash
pip install mlflow
```
To start the MLflow UI, run:
```bash
mlflow ui
```
This will launch a web-based interface at `http://localhost:5000`, where you can see your experiment logs.

### **Remote Tracking using DagsHub**
DagsHub allows remote tracking of MLflow experiments.
1. Create a repository on [DagsHub](https://dagshub.com/).
2. Obtain the remote tracking URL.
3. Set the remote tracking URI in your MLflow script:
```python
import mlflow
mlflow.set_tracking_uri("https://dagshub.com/<user>/<repo>.mlflow")
```

## 7. Logging Experiments in MLflow (Manual vs. Auto-Logging)

### **Manual Logging**
```python
import mlflow
import mlflow.sklearn
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split

data = load_iris()
X_train, X_test, y_train, y_test = train_test_split(data.data, data.target, test_size=0.2, random_state=42)

mlflow.start_run()
model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)

mlflow.log_param("n_estimators", 100)
mlflow.log_metric("accuracy", model.score(X_test, y_test))
mlflow.sklearn.log_model(model, "random_forest_model")
mlflow.end_run()
```

### **Auto-Logging**
```python
import mlflow.sklearn
mlflow.sklearn.autolog()
```
This will automatically log parameters, metrics, and the model without manually specifying them.

## 8. Comparing Experiments in MLflow
Once multiple experiments are logged, you can compare them in the MLflow UI.
```python
mlflow.search_runs()
```

## 9. Hyperparameter Tuning with MLflow
MLflow helps visualize and compare different hyperparameters without using external libraries like Optuna. You can:
- **Manually run multiple experiments** with different hyperparameter values.
- **Log and compare results** in the MLflow UI.
- **Plot graphs** to analyze trends.

Example:
```python
for n_estimators in [10, 50, 100, 200]:
    mlflow.start_run()
    model = RandomForestClassifier(n_estimators=n_estimators)
    model.fit(X_train, y_train)
    accuracy = model.score(X_test, y_test)
    mlflow.log_param("n_estimators", n_estimators)
    mlflow.log_metric("accuracy", accuracy)
    mlflow.end_run()
```
This allows you to compare performance using MLflow's UI and identify the best hyperparameter values using common sense.

## 10. Advanced Features: Model Registry and Deployment
MLflow allows storing and deploying trained models.
```python
mlflow.register_model("runs:/<RUN_ID>/random_forest_model", "RandomForestModel")
```

## 11. Limitations of MLflow
- **Storage Overhead:** Large logs require more space.
- **Security Risks:** Remote tracking may expose data.

## 12. Best Practices for Experiment Tracking
- **Log all hyperparameters and metrics.**
- **Use meaningful experiment names.**
- **Automate logging when possible.**

## 13. Conclusion
MLflow simplifies experiment tracking, making ML workflows efficient. By using MLflow, you ensure reproducibility, easy comparison, and better collaboration in your ML projects.

