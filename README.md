# Molecular Dynamics Simulation of Argon

A Python-based molecular dynamics (MD) engine simulating Argon atoms interacting via the Lennard-Jones potential. This project explores the time evolution of a multi-particle system, implementing MD concepts such as periodic boundary conditions, lattice initialization, and symplectic integration.

## Physical Model

The simulation models **Argon** atoms as classical point particles governed by Newtonian mechanics.

* **Interactions**: Particles interact via the **Lennard-Jones (LJ) Potential**:
    $$U_{LJ}(r) = 4\epsilon \left[ \left(\frac{\sigma}{r}\right)^{12} - \left(\frac{\sigma}{r}\right)^{6} \right]$$
    Where $\sigma$ represents the finite distance at which the inter-particle potential is zero, and $\epsilon$ is the depth of the potential well.
* **Ensemble**: Microcanonical (NVE) - Total energy is conserved (approximately, depending on the integrator).
* **Units**: The simulation utilizes **dimensionless units** internally to ensure numerical stability, scaling by $\sigma$ (length), $\epsilon$ (energy), and $m$ (mass).

## Features

* **Initialization**:
    * **Positions**: Atoms are initialized either on a Face-Centered Cubic (FCC) lattice to simulate solid-phase structures or at random positions to simulate gaseous phases. In both cases, atomic overlaps are forbidden.
    * **Velocities**: Initialized according to the Maxwell-Boltzmann distribution at a specified temperature.
* **Boundary Conditions**: Implements **Periodic Boundary Conditions (PBC)** using the **Minimum Image Convention** to simulate an infinite bulk system.
* **Integrators**:
    * **Euler Method**: Simple first-order integrator (included for educational comparison).
    * **Velocity-Verlet**: Symplectic second-order integrator, preferred for energy conservation in long runs.
* **Analysis**:
    * Tracking of Kinetic ($K$), Potential ($U$), and Total ($E$) energies.
    * Calculation and error analysis of observables, such as the pressure and the heat capacity.

## File Structure

* `MD_functions.py`: Contains the core class `molecular_motion` and helper functions for force calculation, time integration, and lattice generation.
* `MD_simulation.ipynb`: The main executable notebook. It sets up parameters, runs the simulation loops, and visualizes results.
* `images/`: Contains relevant images concerning physical concepts and/or the simulation.

## Configuration & Parameters

Key simulation parameters defined in `MD_simulation.ipynb`:

| Parameter | Description | Default (Argon) |
| :--- | :--- | :--- |
| `N` | Number of atoms | (Derived from lattice) |
| `temp` | Initial Temperature | Kelvin |
| `Dt` | Time step size | User defined (recommended values 1e-3-1e-2) (dimensionless) |
| `tsteps` | Number of time steps | User defined |
| `sigma` | LJ zero-potential distance | 3.405e-10 m |
| `epsilon` | LJ well depth | 1.65e-21 J |

## Usage

1.  **Install Dependencies**:
    ```bash
    pip install numpy scipy matplotlib pandas tqdm
    ```

2.  **Run the Simulation**:
    Open `MD_simulation.ipynb` in Jupyter Lab or Notebook.
    ```bash
    jupyter notebook MD_simulation.ipynb
    ```

3.  **Workflow**:
    * Run the initialization cells to generate the FCC lattice.
    * Select the integrator (Velocity-Verlet recommended).
    * Generate and plot the time evolution of the system of atoms in real space.
    * Observe the energy plots to verify conservation (fluctuations around a mean value are expected).

## Methodology Details

### Dimensionless Units
To avoid numerical errors with extremely small SI values, variables are normalized:
* **Position**: $\tilde{x} = x / \sigma$
* **Time**: $\tilde{t} = t \sqrt{\epsilon / m\sigma^2}$
* **Energy**: $\tilde{E} = E / \epsilon$

## Additional information

The initial development of this project was part of the course **Computational Physics (AP3082)** of the MSc Applied Physics at TU Delft, which took part in March 2025. Further developments in the code have been/are being done independently.

## Authors

* **Ashley Ang**
* **Stefanos Vasileiadis**

## License

This project is open source and available under the **MIT License**.
