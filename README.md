These are the codes for the paper 'Thornton, Li and Xie(2023) - The New England Journal of Statistics in Data Science Volume 1, 270–282' implementing its numerical examples. They compare the frequentist performance (coverage, confidence interval width) of standard Regression-Adjusted ABC (`ISregABC`) with the paper's new Regression-Adjusted ACDC method (`regACC`).

### Cauchy Model
* **`Cauchy_example_paper.R`**: The main script for a univariate Cauchy model. It runs experiments to compare `ISregABC` and `regACC`.
* **`Cauchy_example_functions.R`**: Contains helper functions for the univariate Cauchy example, including simulating datasets, calculating summaries (like median and MAD), and defining the data-dependent proposal distribution (`simulate_from_r2`) from subgroups.

### Cauchy Regression Model
* **`Cauchy_regression_example_paper.R`**: The main script for a linear regression model with Cauchy errors. It compares `ISregABC` and `regACC` for estimating the regression coefficients.
* **`Cauchy_regression_example_functions.R`**: Helper functions for the Cauchy regression example.
    * **Summaries:** Uses the Least Squares Estimator (LSE) as the summary statistic (`cal_summaries`).
    * **Proposals:** Implements an "oracle" proposal (`simulate_from_orcl`) and the paper's data-driven "minibatch" proposal (`simulate_from_propsl`).

### Ricker Model
This is a complex state-space model example that demonstrates the full ACDC workflow.

* **`Ricker_example_initial_calculation.R`**: A **pre-processing script** that must be run first. It implements the "minibatch scheme" to build the `r_n` proposal distribution. It does this by:
    1.  Simulating many "observed" datasets.
    2.  For each dataset, fitting a synthetic likelihood (`synlik`) model to *subgroups* of the data using MCMC (`smcmc`) to get rough parameter estimates.
    3.  Saving these rough estimates (e.g., in `Ricker_SubgroupEst_...RData`), which are then loaded by the main analysis script.

* **`Ricker_example.R`**: The main analysis script. It **loads** the pre-calculated estimates. It then runs the full experiment to compare six different ABC and ACDC methods (e.g., `ISABC`, `ISregABC`, `rejACC`, `regACC`) and analyzes their coverage and confidence region volumes.

* **`Ricker_example_functions.R`**: Helper functions for the Ricker model, primarily wrappers for the `synlik` package.
    * `point_estimate`: A wrapper for `synlik::smcmc` to get the initial parameter estimates for the minibatch scheme.
    * `simulate_pseudo_summaries`: A wrapper for `synlik::simulate` to generate new data.
    * `ABC_ACC_results_summary`: A comprehensive function to calculate all posterior summaries, confidence/credible intervals, and coverage rates.

---
