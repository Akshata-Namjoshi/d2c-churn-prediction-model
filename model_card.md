# Model Card: D2C Churn Predictor (v1.0)

## 1. Intended Use
- Goal: Predict which customers will stop buying in the next 60 days.
- Users: Marketing Team (Win-back campaigns) and CS Team (Intervention).
- Input: Customer transaction history, support tickets, and web visits.

## 2. Model Architecture
- Type: Random Forest Classifier.
- Parameters: 100 Trees (`n_estimators=100`), Max Depth of 10.
- Why Random Forest? It achieved perfect separation of the classes (AUC = 1.0) compared to Logistic Regression (AUC = 0.99).

## 3. Performance
- Accuracy: 100% (Test Set)
- Precision: 1.00
- Recall: 1.00
- Primary Driver: `recency` (74% importance). The model is essentially a sophisticated "Inactivity Detector."

## 4. Limitations
- Recency Bias: The model relies almost entirely on "Time Since Last Order." It is less sensitive to subtle behavioral changes like "browsing but not buying."
- Data Dependency: The model is trained on current market conditions. If the economy changes and people start buying less frequently overall, the model might falsely flag everyone as churning.

## 5. Ethical Considerations
- Age Fairness: The model uses `age_group` as a feature. We must ensure that "Older" customers aren't unfairly targeted with lower discounts.
- Privacy: All customer PII (Personally Identifiable Information) was removed before training.
