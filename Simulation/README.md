# Simulation Studies

Each script conducts a specific simulation study.
The simulated data is generated using the functions in ```Simulate_Data.ipynb``` and also available in the folder ```Data```.

## Toy Example

Each script includes the variable ```toy```, which activates a simplified "Toy example" mode when set to ```True```. This setting significantly reduces computation time and memory requirements by using a smaller sample size and scaling down other parameters. However, in this Toy mode, some plots may differ from those presented in the manuscript.

## Choice of full-scale approximation parameters

The script ```Model_Parameter.ipynb``` calculates the negative log-likelihood at the data-generating parameters for various numbers of inducing points and Vecchia neighbors for correlation-based and Euclidean-based neighbor search. 

## Preconditioners

The script ```Preconditioners.ipynb``` analyses the performance of the FITC preconditioner for different numbers of inducing points and compares FITC and VIF approximation with diagonal update (VIFDU) preconditioners in terms of runtime and the variance of marginal likelihood estimates.

## Runtime

The script ```Runtime.ipynb``` compares the runtime of VIF, FITC, and pure Vecchia approximations for computing likelihoods and predictive distributions for Gaussian and non-Gaussian data.

## Predictive Distribution

The script ```Predictive_Variance.ipynb``` calculates the predictive mean and variances for different number of sample vectors and compares the accuracy of the predictive variance computations.

## Predictive Accuracy

The script ```Predictive_Accuracy.ipynb``` compares runtime and predictive accuracy of VIF, FITC, and pure Vecchia approximations for different input dimensions and kernels.

## VIFLA Bias

The script ```VIF_Laplace.ipynb``` analyzes the bias of the parameter estimation of the marginal variance for different sample sizes for the VIF-Laplace approximation.

