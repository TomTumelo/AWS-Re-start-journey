# 🧠 Fundamentals of Machine Learning & AI

> **Certificate earned:** April 7, 2026 | **Issuer:** AWS / re/Start Program

---

## Overview

This module goes deeper than "Exploring AI" — it breaks down *how* machine learning actually works under the hood. From data preprocessing to model evaluation, this is where theory meets practice using AWS tools and real datasets.

---

## 📚 What I Learned

### The ML Workflow

```
1. Define the Problem
        │
        ▼
2. Collect & Prepare Data
        │
        ▼
3. Choose an Algorithm
        │
        ▼
4. Train the Model
        │
        ▼
5. Evaluate Performance
        │
        ├── Not good enough? ──► Adjust & Retrain
        │
        ▼
6. Deploy to Production
        │
        ▼
7. Monitor & Maintain
```

### Types of Machine Learning

**Supervised Learning** — Learn from labeled data
- Regression: predict continuous values (house prices, stock forecasts)
- Classification: predict categories (fraud/not fraud, disease detection)
- Examples: Linear Regression, Decision Trees, Random Forests, XGBoost, Neural Networks

**Unsupervised Learning** — Find patterns in unlabeled data
- Clustering: group similar data points (K-Means, DBSCAN)
- Dimensionality Reduction: compress data while preserving structure (PCA)
- Anomaly Detection: identify outliers

**Reinforcement Learning** — Learn through trial and reward
- Agent takes actions in an environment
- Receives rewards or penalties
- Goal: maximize cumulative reward
- Examples: game playing (AlphaGo), robotics, recommendation optimization

### Feature Engineering
The art of transforming raw data into useful inputs for ML models.

| Technique | Description |
|---|---|
| **Normalization** | Scale features to 0–1 range |
| **Standardization** | Scale to mean=0, std=1 |
| **One-hot encoding** | Convert categories to binary columns |
| **Binning** | Group continuous values into buckets |
| **Feature selection** | Remove irrelevant/redundant features |
| **Imputation** | Fill in missing values intelligently |

### Data Splits — Why They Matter

```
Full Dataset (100%)
├── Training Set (70–80%)   ─── Model learns from this
├── Validation Set (10–15%) ─── Tune hyperparameters here
└── Test Set (10–15%)       ─── Final, unbiased evaluation (touch ONCE)
```

⚠️ **Never train on test data** — it gives a falsely optimistic accuracy score (data leakage).

### Model Evaluation Metrics

**For Classification:**
- **Accuracy**: % of correct predictions (misleading with imbalanced classes)
- **Precision**: Of predicted positives, how many are real positives?
- **Recall (Sensitivity)**: Of actual positives, how many did we catch?
- **F1 Score**: Harmonic mean of Precision and Recall
- **AUC-ROC**: Overall model discrimination ability

**For Regression:**
- **MAE** (Mean Absolute Error): Average absolute difference
- **RMSE** (Root Mean Squared Error): Penalizes large errors more
- **R²**: How much variance does the model explain? (1.0 = perfect)

### Common ML Pitfalls

| Problem | What it means | Fix |
|---|---|---|
| **Overfitting** | Model memorizes training data, fails on new data | More data, regularization, simpler model |
| **Underfitting** | Model too simple to capture patterns | More complex model, better features |
| **Data Leakage** | Future info contaminates training | Strict train/test separation |
| **Class Imbalance** | Rare class predictions always fail | Oversample, undersample, or use weighted loss |

### Amazon SageMaker

AWS's fully managed ML platform — handles the entire ML lifecycle:

- **SageMaker Studio** — integrated IDE for ML
- **SageMaker Data Wrangler** — visual data preparation
- **SageMaker Autopilot** — AutoML (trains multiple models, picks the best)
- **SageMaker Training Jobs** — scalable model training on managed infrastructure
- **SageMaker Endpoints** — deploy models as REST APIs in one click
- **SageMaker Model Monitor** — detect data drift and performance degradation in production
- **SageMaker Clarify** — detect bias in datasets and models

### Bias & Fairness in ML

A model is only as fair as the data it was trained on. Sources of bias:

- **Historical bias**: If past decisions were biased, training on them perpetuates bias
- **Representation bias**: Underrepresented groups perform worse
- **Measurement bias**: Inconsistent data collection across groups
- **Aggregation bias**: One model applied to groups where sub-group models would be better

**Mitigation tools:** SageMaker Clarify, AWS Audit AI guidelines, diverse dataset curation.

---

## 💡 Key Takeaways

1. **Data quality > algorithm choice** — A simple algorithm on clean data beats a complex model on messy data.
2. **Feature engineering is where the real work happens** — It separates good ML practitioners from great ones.
3. **Always reserve a test set** — And don't touch it until you're done.
4. **Precision vs Recall is a tradeoff** — Choose based on what's worse: false positives or false negatives.
5. **Monitor your models in production** — The world changes, and so does your data distribution.

---

## 🏅 Certificate

> 📄 *Certificate file in this folder*
