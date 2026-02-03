# Vecchia-Inducing Points Full-Scale Approximation (VIF)

In this repository, we provide the complete code for simulated and real-world experiments conducted in the paper "Vecchia-Inducing Points Full-Scale Approximations for Gaussian Processes". 

The  methods for VIF approximations are implemented in the **GPBoost** package, available here: [https://github.com/fabsig/GPBoost](https://github.com/fabsig/GPBoost).

To install the required Python packages, use the following command:
```
pip install -r requirements.txt
```
This will install all dependencies listed in requirements.txt into your environment. Furthermore, install all modules in [https://github.com/katzfuss-group/DKL-GP](https://github.com/katzfuss-group/DKL-GP) to run the DKLGP method used in the real-world data comparison.

## Repository Structure

- **`Simulation`**
  Provides scripts for generating data for the simulation studies and the generated Data used for the experiments and contains scripts to run the simulation experiments. Refer to the `README.md` file in the `Simulation` folder for a detailed description of the various simulations and how to execute them.

- **`Real_World`**  
  Includes scripts and data for the real-world application.

## Quick Start: Running VIF on Your Own Data

This section demonstrates how to apply the VIF methodology to a generic dataset.
The example uses simulated data, but the same workflow applies to real-world data.

```
import numpy as np
import gpboost as gpb
from sklearn.model_selection import train_test_split

# ---------------------------------------------------
# 1. Generate generic spatial data
# ---------------------------------------------------

np.random.seed(1)

n = 3000          # Number of observations
d = 2             # Spatial dimension

# X: spatial coordinates (e.g. longitude / latitude)
X = np.random.uniform(0, 1, size=(n, d))

# y: smooth latent function + Gaussian noise
# (no fixed effects, only GP structure)

y = (
    np.sin(4 * X[:, 0]) +
    np.cos(4 * X[:, 1]) +
    np.random.normal(scale=0.1, size=n)
)

# ---------------------------------------------------
# 2. Train / test split
# ---------------------------------------------------

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=1
)

# ---------------------------------------------------
# 3. Define VIF GP model
# ---------------------------------------------------

num_ind_points = 200      # Inducing points
num_neighbors = 20       # Vecchia neighbors

model_vif = gpb.GPModel(
    gp_coords=X_train,                       # Training coordinates
    cov_function="gaussian_ard",             # Gaussian covariance
    likelihood="gaussian",                   # Gaussian observation model
    num_neighbors=num_neighbors,             # Local conditioning size
    num_ind_points=num_ind_points,           # VIF inducing points
    ind_points_selection="kmeans++",         # Inducing point selection
    matrix_inversion_method="cholesky",      # Dense Cholesky (if likelihood is not Gaussian, use "iterative")
    gp_approx="full_scale_vecchia"           # Use VIF
)

# ---------------------------------------------------
# 4. Fit GP model
# ---------------------------------------------------

model_vif.fit(y=y_train)

# ---------------------------------------------------
# 5. Prediction
# ---------------------------------------------------

pred_mean, pred_var = model_vif.predict(
    gp_coords_pred=X_test,
    predict_var=True
)

print("First 5 predictive means:")
print(pred_mean[:5])

print("\nFirst 5 predictive variances:")
print(pred_var[:5])

```

