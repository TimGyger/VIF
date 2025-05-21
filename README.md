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


