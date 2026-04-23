# SQL Injection Detection using Machine Learning

## Overview

SQL Injection (SQLi) is a major security vulnerability where malicious SQL queries manipulate database operations. This project implements a machine learning-based binary classification system to distinguish between **malicious** and **benign** SQL queries.

The approach models SQL queries as text data and applies **Bag-of-Words feature extraction**, followed by:

- Logistic Regression (baseline)
- Feed-Forward Neural Network (improved model)

---

## Mathematical Formulation

Let a SQL query be represented as a sequence of tokens:

$$
q = (w_1, w_2, \dots, w_n)
$$

Using **Bag-of-Words (CountVectorizer)**, the query is transformed into a feature vector:

$$
x \in \mathbb{R}^d
$$

where:
- $d$ = vocabulary size  
- $x_i$ = frequency of token $i$

---

### Logistic Regression (Baseline Model)

The probability of a query being malicious is:

$$
P(y = 1 \mid x) = \sigma(w^T x + b)
$$

where:

$$
\sigma(z) = \frac{1}{1 + e^{-z}}
$$

- $w \in \mathbb{R}^d$: weight vector  
- $b$: bias  

**Loss Function (Binary Cross-Entropy):**

$$
\mathcal{L} = - \left[ y \log(\hat{y}) + (1 - y)\log(1 - \hat{y}) \right]
$$

---

### Feed-Forward Neural Network

The neural network used consists of multiple dense layers:

$$
z_1 = \text{ReLU}(W_1 x + b_1)
$$

$$
z_2 = \text{ReLU}(W_2 z_1 + b_2)
$$

$$
z_3 = \text{ReLU}(W_3 z_2 + b_3)
$$

$$
\hat{y} = \sigma(W_4 z_3 + b_4)
$$

Additional components:
- Batch Normalization  
- Dropout (0.5)  

---

## Methodology

### Data Processing
- Input: labeled SQL queries (malicious / benign)
- No heavy manual preprocessing
- Vectorization using CountVectorizer:
  - `min_df = 2`
  - `max_df = 0.7`
  - English stopwords removed

---

### Feature Representation
- Bag-of-Words encoding
- Captures token frequency patterns in SQL queries

---

### Model Training
- Logistic Regression trained as baseline
- Neural Network trained using:
  - Binary Cross-Entropy Loss
  - Backpropagation
  - Gradient-based optimization

---

### Evaluation Metrics
- Accuracy  
- Precision  
- Recall  
- F1-score  

---

## Results

- **Logistic Regression Accuracy:** 94.3%  
- **Neural Network Accuracy:** 95.86%  
- **Precision:** 98.63%  
- **Recall:** 89.84%  
- **F1-score:** 94.03%  

The neural network performs slightly better due to its ability to model non-linear relationships.

---

## Underlying Logic

Malicious SQL queries contain identifiable patterns such as:

- `' OR 1=1 --`
- `UNION SELECT`

These patterns are captured as token frequency features, allowing the models to learn associations between specific token combinations and malicious behavior.

---

## Linear Algebra and Calculus Used

### Linear Algebra

Queries are represented as vectors:

$$
z = W x + b
$$

Neural networks involve stacked matrix multiplications.

---

### Calculus

Optimization is performed using gradient descent.

Gradients are computed as:

$$
\frac{\partial \mathcal{L}}{\partial W}
$$

Parameters are updated iteratively to minimize the loss.

---

## Conclusion

A Bag-of-Words representation combined with Logistic Regression and a Feed-Forward Neural Network is effective for SQL injection detection. The neural network provides improved accuracy by capturing non-linear relationships in token patterns.
