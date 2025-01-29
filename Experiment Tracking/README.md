# Experiment Tracking - A Complete Guide

## Table of Contents
1. Introduction
2. Why Experiment Tracking Matters
3. What Happens If We Don’t Track Experiments?
4. Traditional Approach vs. Modern Experiment Tracking
5. Introduction to MLflow for Experiment Tracking
6. Setting Up MLflow
7. Logging Experiments in MLflow
8. Comparing Experiments in MLflow
9. Advanced Features: Model Registry and Deployment
10. Best Practices for Experiment Tracking
11. Conclusion

---

## 1. Introduction
Machine learning involves running multiple experiments to find the best model. However, keeping track of these experiments manually can be challenging. This guide explains why experiment tracking is important, the downsides of not doing it, and how modern tools like MLflow simplify the process.

## 2. Why Experiment Tracking Matters
In machine learning, you often tweak parameters, change datasets, or use different models to improve performance. Without proper tracking, you may:
- Lose track of what worked best.
- Waste time rerunning experiments.
- Struggle with reproducibility.
- Fail to collaborate effectively.

**Example:** You train a model with a learning rate of 0.01 and achieve 90% accuracy. Later, you retrain it but forget the learning rate you used, making it difficult to reproduce the result.

## 3. What Happens If We Don’t Track Experiments?
Without experiment tracking, you may face these issues:
- **Inconsistent Results:** Different runs give different outputs, and you don't know why.
- **Time Wasted:** Repeating failed experiments instead of learning from them.
- **Difficult Debugging:** If a model performs poorly, you have no records to check what changed.
- **Hard to Share Work:** In a team, lack of tracking makes collaboration difficult.

## 4. Traditional Approach vs. Modern Experiment Tracking

### **Manual Tracking (Excel, Notepad, etc.)**
A common old-school method is using spreadsheets or text files to log experiments.

#### **Example:**
| Experiment | Model | Learning Rate | Batch Size | Accuracy |
|------------|--------|--------------|------------|---------|
| Exp1      | RandomForest | - | - | 85% |
| Exp2      | CNN   | 0.01 | 32 | 90% |

#### **Problems with this approach:**
- Hard to keep track as experiments grow.
- No automated logging.
- Hard to compare past results.

### **Modern Approach (Using MLflow)**
MLflow automates logging and allows tracking all experiments in a structured way.

## 5. Introduction to MLflow for Experiment Tracking
MLflow is an open-source tool that helps log and manage machine learning experiments.

**Key Features:**
- **Automatic Logging**: Tracks hyperparameters, metrics, and artifacts.
- **Reproducibility**: Stores code versions and environment settings.
- **Comparison Dashboard**: Visualizes different experiments.
- **Model Registry**: Stores and manages trained models.

## 6. Setting Up MLflow
To install MLflow, use:
```bash
pip install mlflow
```
Start MLflow UI:
```bash
mlflow ui
```
This launches a web-based UI at `http://localhost:5000` to track experiments.

## 7. Logging Experiments in MLflow
Here’s an example of logging experiments in MLflow:
```python
import mlflow
import mlflow.sklearn
from sklearn.ensemble import RandomForestClassifier
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split

# Load Data
data = load_iris()
X_train, X_test, y_train, y_test = train_test_split(data.data, data.target, test_size=0.2, random_state=42)

# Start MLflow Experiment
mlflow.start_run()

# Train Model
model = RandomForestClassifier(n_estimators=100)
model.fit(X_train, y_train)

# Log Parameters and Metrics
mlflow.log_param("n_estimators", 100)
mlflow.log_metric("accuracy", model.score(X_test, y_test))

# Log Model
mlflow.sklearn.log_model(model, "random_forest_model")

mlflow.end_run()
```

## 8. Comparing Experiments in MLflow
Once multiple experiments are logged, you can compare them in the MLflow UI.

```python
mlflow.search_runs()
```
This returns a table comparing different runs.

## 9. Advanced Features: Model Registry and Deployment
MLflow allows you to store trained models for deployment.
```python
mlflow.register_model("runs:/<RUN_ID>/random_forest_model", "RandomForestModel")
```
You can then load the model later for inference.

```python
import mlflow.sklearn
model = mlflow.sklearn.load_model("models:/RandomForestModel/1")
predictions = model.predict(X_test)
```

## 10. Best Practices for Experiment Tracking
- **Log Everything:** Hyperparameters, metrics, dataset versions, and code changes.
- **Use Meaningful Experiment Names:** Helps identify results easily.
- **Automate Logging:** Use MLflow’s auto-logging to avoid missing details.
- **Compare Metrics:** Always review past experiments before starting a new one.

## 11. Conclusion
Experiment tracking is crucial for successful ML projects. While manual methods exist, modern tools like MLflow provide structured logging, easy comparisons, and improved reproducibility. By integrating experiment tracking into your workflow, you save time, avoid confusion, and ensure better model performance over time.

