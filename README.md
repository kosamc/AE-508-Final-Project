# Optimal Interplanetary Trajectory Design

This project focuses on optimizing fuel-efficient trajectories for Earth-to-Mars and Earth-to-Jupiter transfers using **Modified Equinoctial Elements (MEE)** and **polar coordinates** with **indirect optimal control methods**. The code implements Hamiltonian-based optimization, Pareto front analysis, and validation via symbolic and numerical techniques.

## Key Features

### 1. **Dynamics and Optimization**
- **Equations of Motion**: Derived in both MEE (`EOM_MEE_Minfuel.m`) and polar coordinates (`Dynamics` functions).
- **Optimal Control**:  
  - Minimizes fuel consumption using **Pontryagin's Maximum Principle**.
  - Implements **bang-bang control** via switch functions \( S = \|P\| - 1 \), where \( P \) is the primer vector.
  - Throttle parameterized as \( \delta = 0.5(1 + \tanh(S/\rho)) \).

### 2. **Coordinate Systems**
- **MEE Coordinates**:  
  - Used in `Jupiter_3D_to_MEE.m` for 3D trajectory optimization.
  - State vector: \( \mathbf{x} = [p, f, g, h, k, L, m]^T \).
- **Polar Coordinates**:  
  - Simplified 2D dynamics in `Mars_Polar_Transfer.m` and `Jupiter_Polar_Transfer.m`.
  - State vector: \( \mathbf{x} = [r, \theta, u, v, m]^T \).

### 3. **Numerical Methods**
- **Boundary Value Problem (BVP)**:  
  Solved via `fsolve` for costate initialization and `ode45` for trajectory propagation.
- **Pareto Front Analysis**:  
  Trade-off between time-of-flight (TOF) and fuel consumption (e.g., `Jupiter_3D_to_MEE.m`):
  ```latex
  J = 0.5 \cdot (\text{TOF} + \text{Fuel})
