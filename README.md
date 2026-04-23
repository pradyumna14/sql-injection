# SQL Injection Detection using Machine Learning

## Overview

SQL Injection (SQLi) is a critical vulnerability in database-driven systems where malicious inputs alter the intended structure of SQL queries, enabling unauthorized access or data manipulation. Traditional detection mechanisms rely on rule-based or signature-based approaches, which often fail to generalize to unseen or obfuscated attack patterns.

This work presents a machine learning-based approach for detecting SQL injection attacks by modeling SQL queries as textual data and performing binary classification into malicious and benign categories.

---

## Mathematical Formulation

Let a SQL query be represented as a sequence of tokens:

q = (w1, w2, ..., wn)

Using Bag-of-Words, each query is converted into a vector:

x ∈ R^d

where d is the vocabulary size.

### Logistic Regression

The probability of a query being malicious is:

P(y = 1 | x) = sigmoid(wᵀx + b)

where:
- sigmoid(z) = 1 / (1 + e^(-z))
- w = weight vector
- b = bias

Loss function used:

Binary Cross Entropy:
Loss = - [ y log(ŷ) + (1 - y) log(1 - ŷ) ]

---

## Existing Approaches

SQL injection detection methods include:

- Rule-based filtering
- Signature-based detection
- Static query validation

Machine learning models used:

- Logistic Regression
- Support Vector Machines
- Naive Bayes
- Decision Trees

Deep learning approaches:

- LSTM / GRU
- CNN for text
- Transformer-based models

---

## Proposed Model

This work implements:

1. Logistic Regression (baseline)
2. Feed-Forward Neural Network (dense layers)

The neural network computes:

f(x) = sigmoid( W2 · activation(W1 · x + b1) + b2 )

where:
- W1, W2 = weight matrices
- activation = non-linear function (e.g., ReLU)

---

## Methodology

### Data Processing

- Input: labeled SQL queries
- Text preprocessing and normalization
- Vectorization using CountVectorizer

### Feature Representation

- Bag-of-Words encoding
- Captures frequency of SQL tokens

### Model Training

- Logistic Regression for baseline
- Feed-Forward Neural Network trained using backpropagation

### Evaluation Metrics

- Accuracy
- Precision
- Recall
- F1-score

---

## Results

- Logistic Regression Accuracy: ~94.3%
- Neural Network Accuracy: ~95.9%

The neural network slightly outperforms logistic regression by capturing non-linear relationships.

---

## Underlying Logic

Malicious SQL queries contain distinguishable token patterns such as:

- ' OR 1=1 --
- UNION SELECT

These patterns are captured through vectorization. The models learn associations between these patterns and the output labels.

---

## Linear Algebra and Calculus

### Linear Algebra

- Queries are represented as vectors
- Matrix multiplication used in models:
  
  z = W · x + b

### Calculus

- Gradient descent used for optimization
- Backpropagation computes gradients of loss with respect to weights
- Parameters updated iteratively to minimize loss

---

## Conclusion

Machine learning models can effectively detect SQL injection attacks using textual patterns in queries. Both linear and neural approaches achieve strong performance, with neural networks providing improved accuracy.
