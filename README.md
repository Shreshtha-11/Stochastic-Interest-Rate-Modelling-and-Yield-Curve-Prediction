# Stochastic Interest Rate Modelling and Prediction

## Project Overview
This repository contains a comprehensive implementation, calibration, and extension of the **Cox-Ingersoll-Ross (CIR)** stochastic short-rate model using historical yield curve data. The project is specifically designed to evaluate the predictive power of short-rate models when subjected to real-world market dynamics and macroeconomic regime shifts.

The primary objective is an **Out-of-Sample Prediction Challenge**: Reconstructing the entire yield curve (maturities ranging from 6 Months to 30 Years) for any given day in the testing period by ingesting **only the 3-Month yield** as a proxy for the instantaneous short rate ($r_t$).

## Core Features
1. **Robust Data Engineering**: Implements a specialized Spike-Reversal Filter and handles market holiday gaps via business-day reindexing, ensuring data integrity and strictly preventing data leakage.
2. **CIR Calibration**: Features multiple calibration methodologies, including:
   - Discretized Ordinary Least Squares (OLS)
   - Exact Maximum Likelihood Estimation (MLE)
   - Risk-Neutral Measure ($\mathbb{Q}$) adjustments
3. **Advanced Extensions**:
   - **Shifted CIR++**: Augments the base model with deterministic shifts, applying validation shrinkage to prevent overfitting during sudden regime changes (e.g., transitioning from an upward-sloping to an inverted yield curve).
   - **Additive Two-Factor CIR**: Decomposes the short rate into independent, positive "level" and "slope" factors to capture complex term structure variations.
4. **Predictive Performance**: The optimized Risk-Neutral MLE model achieves an outstanding aggregate out-of-sample $R^2$ of **~0.947**, comfortably surpassing the project's 0.85 evaluation benchmark.

## Repository Structure
- `Stochastic_Interest_Rate_Modelling.ipynb`: The singular, comprehensive Jupyter Notebook containing all data preprocessing, mathematical derivations, calibration algorithms, yield predictions, and presentation-grade visualizations.
- `train_data.csv`: Historical daily yields (9 tenors) used for parameter calibration (2016–2024).
- `test_data_3M.csv`: Held-out 3-Month yield proxy used as the sole input for out-of-sample predictions (2024–2026).
- `test_data.csv`: Held-out ground truth data used strictly for $R^2$ validation scoring.

## How to Run
The project is encapsulated entirely within `Stochastic_Interest_Rate_Modelling.ipynb`. Ensure your environment has the required scientific libraries (`pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `scikit-learn`).

Execute the notebook sequentially from top to bottom. It will automatically load the data, process outliers, calibrate the models, and generate the final out-of-sample evaluation metrics and visual dashboards.
