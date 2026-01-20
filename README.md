# Project Report: Non-Linear Modeling of Air Quality Data

## 1. Project Abstract
This assignment explores the statistical modeling of environmental data. The objective is to apply a user-specific non-linear transformation to Nitrogen Dioxide ($NO_2$) levels from the India Air Quality dataset and subsequently learn the parameters of a Gaussian-based Probability Density Function (PDF) that best fits the transformed data.

## 2. Implementation Details

### A. Dataset & Feature Selection
* **Dataset:** India Air Quality Data (Kaggle).
* **Target Feature:** $NO_2$ (Nitrogen Dioxide).
* **Preprocessing:** The data was cleaned to remove missing values and parse non-numeric entries.

### B. Non-Linear Transformation
The raw feature $x$ was mapped to a new feature space $z$ using a sinusoidal transformation function parameterized by the University Roll Number ($r$).

* **University Roll Number ($r$):** `102303993`
* **Derived Constants:**
  * $a_r = 0.05 \times (r \pmod 7) \rightarrow 0.05$
  * $b_r = 0.3 \times ((r \pmod 5) + 1) \rightarrow 1.2$
* **Transformation Equation:**
  $$z = x + 0.05 \cdot \sin(1.2 \cdot x)$$

### C. Probability Density Function (PDF) Estimation
The goal was to learn the parameters for the following density model:
$$\hat{p}(z) = c \cdot e^{-\lambda(z - \mu)^2}$$

This equation is structurally identical to the Gaussian Normal Distribution:
$$f(z) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{1}{2\sigma^2}(z - \mu)^2}$$

By equating terms, the model parameters were estimated using statistical moments (Mean and Variance) of the transformed variable $z$:
1. **$\mu$ (Mean):** Direct arithmetic mean of $z$.
2. **$\lambda$ (Precision Factor):** Calculated as $\frac{1}{2\sigma^2}$.
3. **$c$ (Normalization Constant):** Calculated as $\frac{1}{\sigma\sqrt{2\pi}}$.

## 3. Computational Results

Based on the analysis of **419,509 valid data points**, the learned parameters for the model are:

| Model Parameter | Symbol | Estimated Value |
| :--- | :---: | :--- |
| **Center (Mean)** | $\mu$ | `25.808528` |
| **Width Factor** | $\lambda$ | `0.001460` |
| **Peak Density** | $c$ | `0.02155982` |

## 4. Conclusion
The non-linear transformation successfully modified the feature space, and the Gaussian parameters were derived using the Method of Moments. The resulting curve represents the probability density of the transformed air quality index for my roll number - 102303993.
