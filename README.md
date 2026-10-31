# Machine Learning — TP2: Standardized PCA

**Student:** Kaddour Abdelmalek Islam  
 

---

## Project Overview
This repository contains the complete implementation and analysis for **Practical Session 2: Python for Standardized PCA**.

The objective is to implement **Principal Component Analysis (PCA)** from scratch using NumPy and Pandas, and compare the mathematical and numerical results against the predefined implementation from `scikit-learn` (`sklearn.decomposition.PCA`).

---

## Repository Structure
```text
machine-learning-tp2/
├── TP2_Solutions.ipynb       # Jupyter Notebook with full code, outputs, and plots
└── README.md                # Project overview, findings, and analysis notes
```

---

## Key Results & Discussion Notes

### 1. Standardization & Correlation
- Variables are standardized ($Z = \frac{X - \mu}{\sigma}$) using population standard deviation ($ddof=0$) to ensure consistency with Scikit-Learn's `StandardScaler`.
- The correlation matrix shows very high correlations across subjects (e.g., Mathematics and Algorithms $r = 0.991$, Mathematics and Programming $r = 0.945$). This strong multicollinearity indicates high redundancy, making PCA suitable for reducing dimensionality from 4 to 2 components.

### 2. Eigenvalues & Explained Variance
The eigen-decomposition of the $4 \times 4$ correlation matrix yields:
- $\lambda_1 = 3.7397$ ($93.49\%$ of total variance)
- $\lambda_2 = 0.2402$ ($6.01\%$ of total variance)
- $\lambda_3 = 0.0191$ ($0.48\%$ of total variance)
- $\lambda_4 = 0.0009$ ($0.02\%$ of total variance)

The first two principal components capture **99.50%** of the total variance, retaining practically all the information with only $0.50\%$ loss.

### 3. Comparison: Scratch vs Scikit-Learn
- **Coordinates:** The projected 2D coordinates obtained from scratch ($Z \times W$) and `sklearn.decomposition.PCA` match down to floating-point precision ($|\text{diff}| < 10^{-15}$).
- **Variance Ratio:** Both implementations produce the exact same explained variance ratios ($93.49\%$ and $6.01\%$).
- **Eigenvector Sign Indeterminacy:** In PCA, if $v$ is an eigenvector ($R v = \lambda v$), then $-v$ is also a valid eigenvector ($R (-v) = \lambda (-v)$). While both directions represent the exact same geometric axis, different solvers may flip the sign. Both implementations here yield identical vector orientations.

### 4. Interpretation of Principal Components
- **PC1 (Overall Performance):** All subjects have positive, uniform loadings ($\approx 0.48$ to $0.52$). High values correspond to top-performing students across all disciplines (e.g., S4 at $+2.88$), while negative values reflect weaker grades (e.g., S3 at $-2.95$).
- **PC2 (Discipline Specialization):** PC2 contrasts theoretical/statistical ability (loading $+0.78$ on Statistics) with practical computer science skills (loading $-0.59$ on Programming, $-0.19$ on Algorithms). S6 exhibits the highest positive coordinate on PC2 ($+0.79$) due to relatively higher grades in Statistics (15) compared to Programming (13).

---

