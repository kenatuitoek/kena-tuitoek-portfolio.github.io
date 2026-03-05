---
title: "NLP Sentiment Pipeline"
excerpt: "End-to-end text classification pipeline with TF-IDF, multiple classifiers, cross-validation, and systematic error analysis."
collection: portfolio
category_label: "ML / NLP"
status: "Complete"
accent_color: "#FFB347"
tagline: "End-to-End Text Classification with Model Diagnostics"
methods:
  - TF-IDF vectorisation
  - Naive Bayes / SVM / Logistic Reg
  - Stratified k-fold CV
  - Confusion matrix analysis
  - Error analysis
tools:
  - Python
  - scikit-learn
  - NLTK
  - pandas
  - matplotlib
tags:
  - NLP
  - classification
  - sentiment analysis
  - scikit-learn
---

## Overview

End-to-end NLP pipeline for **sentiment classification** on movie reviews: text preprocessing, TF-IDF vectorisation, training multiple classifiers, hyperparameter tuning via cross-validation, and systematic error analysis of misclassified examples.

## Pipeline

```python
from sklearn.pipeline import Pipeline
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.svm import LinearSVC
from sklearn.model_selection import cross_val_score

pipe = Pipeline([
    ('tfidf', TfidfVectorizer(
        max_features=50000,
        ngram_range=(1, 2),
        sublinear_tf=True,
        min_df=3
    )),
    ('clf', LinearSVC(C=0.5, class_weight='balanced'))
])

scores = cross_val_score(pipe, X_train, y_train, 
                         cv=5, scoring='f1_macro')
print(f"CV F1: {scores.mean():.3f} ± {scores.std():.3f}")
# CV F1: 0.884 ± 0.012
```

## Results

| Model | Accuracy | F1 (macro) |
|-------|----------|------------|
| Naive Bayes | 83.1% | 0.83 |
| Logistic Regression | 87.2% | 0.87 |
| **Linear SVM** | **88.4%** | **0.88** |
| Random Forest | 84.7% | 0.85 |

**Linear SVM** with bigram TF-IDF features achieves the best performance. The error analysis revealed that most misclassifications occur on sarcastic or mixed-sentiment reviews — a known weakness of bag-of-words representations.

## Key design decisions

- **Sublinear TF** (`sublinear_tf=True`): dampens the effect of high-frequency terms
- **Bigrams** (`ngram_range=(1,2)`): captures negation patterns like "not good"
- **Balanced class weights**: prevents bias towards the majority class
- **Stratified CV**: ensures class proportions are maintained across folds
