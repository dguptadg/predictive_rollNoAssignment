# Probability Density Function Estimation with Roll-Number-Based Nonlinear Mapping

## Project Description

This project demonstrates the estimation of a **Probability Density Function (PDF)** for air-quality data using a **custom nonlinear transformation** derived from a student roll number. The work applies data preprocessing, nonlinear feature mapping, and **Maximum Likelihood Estimation (MLE)** to learn a Gaussian-shaped density.

The NO₂ pollutant concentration values are transformed and modeled probabilistically to understand their distribution after transformation.

---

## Dataset

- **Name:** India Air Quality Dataset  
- **Source:** Kaggle  
- **Link:** https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data  

### Dataset Summary

- Feature selected: **NO₂ (`no2`)**
- Total rows: **435,742**
- Rows used after cleaning: **415,688**

---

## Data Cleaning Procedure

The dataset was filtered using the following steps:

- Removed entries with missing NO₂ values
- Discarded negative NO₂ measurements

Only valid and physically meaningful values were retained for analysis.

---

## Nonlinear Transformation (x → z)

Each cleaned NO₂ value \( x \) is transformed into a new variable \( z \) using a sinusoidal nonlinear mapping:

$$
z = x + a_r \sin(b_r x)
$$


The parameters \( a_r \) and \( b_r \) depend on the roll number \( r \):

$$
a_r = 0.05 \times (r \bmod 7)
$$

$$
b_r = 0.3 \times ((r \bmod 5) + 1)
$$

### Roll Number Details

- **Roll Number:** 102303877

Computed values:

- \( a_r = 0.2 \)
- \( b_r = 0.9 \)

---

## Probability Density Model

The transformed variable \( z \) is assumed to follow a Gaussian-shaped probability density function of the form:

$$
\hat{p}(z) = c \, e^{-\lambda (z - \mu)^2}
$$


The parameters \( \mu \), \( \lambda \), and \( c \) are estimated from data.

---

## Parameter Estimation (MLE)

The parameters are estimated using **Maximum Likelihood Estimation (MLE)**.

### Mean

$$
\hat{\mu} = \frac{1}{n} \sum_{i=1}^{n} z_i
$$

### Variance

$$
\hat{\sigma}^2 = \frac{1}{n} \sum_{i=1}^{n} (z_i - \hat{\mu})^2
$$

### Lambda

$$
\hat{\lambda} = \frac{1}{2\hat{\sigma}^2}
$$

### Normalization Constant

$$
\hat{c} = \sqrt{\frac{\hat{\lambda}}{\pi}}
$$


---

##  Estimated Parameters

| Parameter | Value |
|---------|------:|
| Roll Number | 102303877 |
| \( a_r \) | 0.2 |
| \( b_r \) | 0.9 |
| Estimated Mean \( \mu \) | 25.8041 |
| Estimated \( \lambda \) | 0.001459 |
| Estimated \( c \) | 0.02155 |

---

##  Visualization

A histogram of the transformed variable \( z \) is plotted along with the fitted PDF to visually assess the quality of the estimation.

<p align="center">
  <img src="https://github.com/user-attachments/assets/f1ea5bed-7b00-4183-8a81-04be1b17169e" width="700">
</p>

---

##  Notes

- This repository was created as part of a **Data Science academic assignment**
- The emphasis is on **conceptual understanding and mathematical correctness**
- The project is intended for learners exploring:
  - Probability density functions
  - Nonlinear transformations
  - Maximum Likelihood Estimation
  - Real-world data preprocessing

---

