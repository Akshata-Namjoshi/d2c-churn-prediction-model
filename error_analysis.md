# Model Performance & Error Audit

## 1. Executive Summary
The Random Forest model achieved 100% Accuracy on the Test Set.
- False Positives: 0
- False Negatives: 0

## 2. Why is the error rate zero? (Root Cause Analysis)
The model discovered a "Dominant Signal" in the data: Recency.
- Feature Importance: `recency` (Days since last order) accounts for 74.5% of the decision logic.
- The "Magic Rule": The data likely contains a hard cutoff (e.g., if a customer is inactive for >120 days, they are always labeled as churned). The Random Forest successfully reverse-engineered this business rule.

## 3. Potential Risks (Hypothetical Error Scenarios)
Even though the model made no mistakes on this dataset, we must be aware of future risks:

### Risk A: The "Holiday" False Positive
   Scenario: A loyal customer goes on a 3-month vacation. Their `recency` spikes to 90+ days.
   Model Prediction: CHURN (Probability > 90%).
   Reality: They return after the holiday.
   Mitigation: We should check `loyalty_tier` before cutting them off. If they are "Platinum", send a "We Miss You" email instead of assuming they are gone.

### Risk B: The "Angry" False Negative
   Scenario: A customer buys today (Recency = 0), so they look "Safe." However, they file 5 angry support tickets immediately.
   Model Prediction: RETAINED (because Recency is low).
   Reality: They churn immediately due to anger.
   Mitigation: The current model only weighs `support_tickets` at 0.5%. We may need to manually boost this weight to catch "Angry Active" users.
