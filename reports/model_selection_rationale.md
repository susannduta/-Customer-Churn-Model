# Group Written Reflection: Customer Churn Model

## 1. Model selection and justification

The selected model was **Logistic regression**, using parameters
`{'model__C': 1}`. It achieved a mean five-fold cross-validation
F1-score of **0.4701**, with a fold standard deviation of
**0.0527**.

It was selected because it achieved the strongest mean F1-score among
the evaluated candidate models. Its performance across the folds was
reasonably consistent, as indicated by the standard deviation. The
model also offers relatively straightforward interpretation compared
with a more complex decision tree.

## 2. False negatives and subgroup performance

False negatives represent customers who actually churned but were
predicted to stay. For the provider, this means potentially losing
customers without identifying them as being at risk in advance,
resulting in missed opportunities for retention interventions.

The development out-of-fold evaluation recorded **566 false negatives**.

The subgroup with the lowest recall was **Established**:
- Sample size: **2268 customers**
- Actual churners: **649**
- Recall: **0.216**

For comparison, **New** had a recall of
**0.782**, with
261 actual churners among
452 customers.

This difference should be interpreted cautiously because subgroup
sizes and the numbers of actual churners differ. It does not, by
itself, establish systematic bias.

## 3. Permutation importance

The highest permutation importance was recorded for
**tenure_months**, with a mean importance of
**0.079**.

This indicates that shuffling this feature caused the largest average
decrease in validation F1-score. However, permutation importance does
not establish causation. It measures the feature's contribution to
the model's predictive performance, not whether changing the feature
would cause customer churn. Correlations with other features can also
affect the importance estimates.

## 4. Final-test performance and generalization

The final-test F1-score was **0.4486**, compared with a mean
cross-validation F1-score of **0.4701**. The difference was
**-0.0215**.

The final test accuracy was **0.700**, precision was
**0.585**, and recall was **0.364**.

The test F1-score is relatively close to the cross-validation F1-score, suggesting reasonably consistent generalization. However, the absolute predictive performance remains limited.

The model nevertheless missed **145 actual churners** in the final
test set, so its ability to identify customers at risk remains a
significant limitation.

## 5. Dataset limitations and deployment considerations

Two limitations of the synthetic dataset are:

1. **Limited real-world representativeness:** Synthetic customer
   records may not fully reproduce the complexity, variability, and
   behavioural patterns found in actual telecommunications customer
   data. Model performance on this dataset may therefore not
   transfer directly to real customers.

2. **Potentially simplified relationships:** Relationships between
   customer characteristics and churn may have been generated using
   simplified assumptions. Real customer churn can be influenced by
   additional factors, changing behaviours, and interactions that
   are not represented in the dataset.

Before deploying a real churn model, I would validate it using
historical, real customer data from the provider, ensuring that the
data is representative, leakage-free, and evaluated on a separate
time-based test period. I would also monitor predictive performance
and subgroup recall after deployment.

---

**Final model:** Logistic regression

**Development CV F1:** 0.4701

**Final-test F1:** 0.4486
