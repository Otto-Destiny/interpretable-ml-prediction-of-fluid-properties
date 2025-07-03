# Predicting PVT Properties from Hydrocarbon Compositional Data

This repository presents a complete, high-precision machine learning framework for predicting three critical PVT properties of reservoir fluids—**bubble point pressure (Pb)**, **solution gas-oil ratio (Rs)**, and **oil formation volume factor (Bo)**—from detailed hydrocarbon compositional data. The modeling pipeline uses sparse polynomial **ElasticNet regression** to uncover interpretable, closed-form predictive equations that capture key nonlinear interactions across C₁ to C₇⁺ components.

## Project Highlights

- **High-Fidelity Prediction**: Achieves $R^2 > 0.99$ for $\log B_o$ and $P_b$, and $R^2 \approx 0.92$ for $R_s$ using carefully tuned regularized regression.
- **Polynomial Feature Engineering**: Applies second-degree interaction terms (e.g. $C_1 \cdot C_7^+$, $(C_7^+)^2$) to capture key nonlinear compositional effects.
- **Correlation-Driven Feature Selection**: Uses Spearman and Pearson correlation to rank and retain the top 10 most informative features per target.
- **Cross-Validated ElasticNet**: Grid search over $\alpha$ and $l_1$-ratio values with 5-fold cross-validation ensures generalization and sparse, physically meaningful coefficients.
- **Equation Extraction**: Final models are expressed as interpretable mathematical equations suitable for field or simulation use.

## Dataset Description

This project uses a **synthetically generated dataset** comprising **529 simulated reservoir fluid samples**. Each sample contains:
- Mole fraction data for 13 compositional variables:  
  $\text{C}_1$ to $\text{C}_7^+$, $\text{N}_2$, $\text{CO}_2$, $\text{iC}_4$, $\text{nC}_4$, $\text{iC}_5$, $\text{nC}_5$
- Molecular weight of C₇⁺ fraction (`MW_C7+`)
- Target PVT properties:  
  - **Bubble Point Pressure** ($P_b$, psia)  
  - **Solution Gas-Oil Ratio** ($R_s$, scf/STB)  
  - **Oil Formation Volume Factor** ($B_o$, bbl/STB)

All PVT outputs are derived from thermodynamic equations of state and calibrated correlations, enabling realistic learning without proprietary data exposure.

## Methodology Overview

1. **Preprocessing**  
   - Dropped irrelevant PVT columns (e.g. dew point)  
   - Normalized compositional features; renamed variables for clarity

2. **Polynomial Feature Expansion**  
   - Created interaction and squared terms up to second-order  
   - Total of 104 engineered features (excluding bias)

3. **Feature Ranking and Selection**  
   - Pearson and Spearman correlation used to rank features for each target  
   - Top 10 features per target retained for modeling

4. **Modeling**  
   - ElasticNet regression fitted using `sklearn.linear_model.ElasticNetCV`  
   - Grid search over $\alpha$ and $l_1$-ratio using 5-fold CV  
   - Metrics: $R^2$, MSE (train/test), residual analysis

5. **Interpretation**  
   - Coefficients extracted and used to form explicit equations for $\log B_o$, $P_b$, and $R_s$  
   - All equations are rendered in LaTeX for clarity

## Example: Final Equation for $R_s$

![Rs_latex_eqn.png](images\Rs_latex_eqn.png)

## Dependencies

* Python ≥ 3.8
* scikit-learn
* pandas, numpy
* matplotlib, seaborn
* Jupyter Notebook
* IPython.display (for LaTeX rendering)


## Author

**Destiny Otto**

_Petroleum Engineering | Machine Learning | Computational Modelling | Subsurface Analytics_

GitHub: [github.com/otto-destiny](https://github.com/otto-destiny)

## License

This work is made available under the [MIT License](LICENSE).

## Future Work

* Incorporate temperature and pressure as model inputs
* Extend to real-field compositional data (with lab-measured PVT)
* Apply symbolic regression to further enhance interpretability
* Compare with deep learning models (MLPs, GPs, etc.)

Bridging compositional analysis with high-precision reservoir property prediction—one equation at a time.
