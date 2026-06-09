# Part 3: Churn Prediction Model

## 📌 Project Overview
This is Part 3 of the D2C Capstone Project.
We successfully built a Machine Learning pipeline to predict customer churn with high accuracy.

## 📂 Repository Contents
| File | Description |
| :--- | :--- |
| `churn_model.ipynb` | The Python code for Data Loading, Training, and Evaluation. |
| `model.pkl` | The saved Random Forest model (ready for deployment). |
| `metrics.json` | Final performance metrics (Accuracy, Confusion Matrix). |
| `model_card.md` | Business documentation explaining the model's logic. |
| `error_analysis.md` | Investigation into why the model performs perfectly (Signal Analysis). |

## 🏆 Results
- Winning Model: Random Forest Classifier.
- Test Accuracy: 100%
- Top Predictor: `recency` (Days since last purchase).

## 🚀 Usage
To load and use the model:
```python
import joblib
# Load the saved model
model = joblib.load('model.pkl')
# Get a prediction (0 = Stay, 1 = Churn)
prediction = model.predict(new_customer_data)
