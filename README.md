# Q: Learn Probability Density Functions using Roll-Number-Parameterized Non-Linear Model

## Objective

The objective of this assignment is to **learn and estimate a Probability Density Function (PDF)** for a transformed air‑quality feature using a **roll‑number‑parameterized non‑linear model**.

Given the NO₂ feature (x), it is transformed into (z) using a non‑linear function dependent on the roll number, and the parameters of the following PDF are estimated:

[
\hat{p}(z) = c , e^{-\lambda (z - \mu)^2}
]

---

## Dataset

* **Dataset Name:** India Air Quality Dataset
* **Source:** Kaggle
* **Link:** [https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data](https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data)

### Dataset Details

* Feature used: **NO₂ (`no2`)**
* Total rows: **435,742**
* Valid samples after cleaning: **415,688**

---

## Methodology

### Step 1: Data Cleaning

The NO₂ feature was cleaned using the following steps:

* Converted values to numeric (`errors="coerce"`)
* Removed missing values
* Removed negative values
* Removed extreme outliers using percentile range **[0.5, 99.5]** to improve numerical stability

---

### Step 2: Non‑Linear Transformation (x → z)

The cleaned NO₂ values (x) are transformed into (z) using the roll‑number‑dependent function:

[
z = x + a_r \sin(b_r x)
]

where:

[
a_r = 0.05 (r \bmod 7), \quad b_r = 0.3 ((r \bmod 5) + 1)
]

For **Roll Number: 102303877**

* (r \bmod 7 = 6 \Rightarrow a_r = 0.3)
* (r \bmod 5 = 2 \Rightarrow b_r = 0.9)

---

## Parameter Estimation (Maximum Likelihood Estimation)

Assuming a Gaussian‑shaped density, parameters are estimated using Maximum Likelihood Estimation (MLE):

[
\hat{\mu} = \frac{1}{n} \sum_{i=1}^{n} z_i
]

[
\hat{\sigma}^2 = \frac{1}{n} \sum_{i=1}^{n} (z_i - \hat{\mu})^2
]

[
\hat{\lambda} = \frac{1}{2 \hat{\sigma}^2}
]

[
\hat{c} = \sqrt{\frac{\hat{\lambda}}{\pi}}
]

---

## Results

### Estimated Parameters

| Parameter                    |                 Value |
| ---------------------------- | --------------------: |
| Roll Number                  |             102303877 |
| (a_r)                        |                   0.2 |
| (b_r)                        |    0.8999999999999999 |
| Estimated Mean ((\mu))       |    25.804091267939096 |
| Estimated Lambda ((\lambda)) | 0.0014593812811427918 |
| Estimated (c)                |   0.02155308538236038 |

The estimated parameters are saved as a CSV file at:

```
outputs/estimated_params.csv
```

---

## Visualization

A histogram of the transformed variable (z) is plotted with the fitted PDF overlaid to visually verify the estimation.

![PDF Fit Plot](outputs/fit_plot.png)

---

## Notes

* This repository is created as part of a **Data Science assignment**.
* The implementation focuses on clarity and correctness rather than optimization.
* The project is suitable for beginners learning **PDF estimation, data cleaning, and MLE**.
