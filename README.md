# Assignment 2 – Scientific Computing for ODEs and PDEs (Spring 2025)

## Overview

This assignment involves:
- Developing an adaptive Runge-Kutta ODE solver
- Designing, analyzing, and implementing numerical schemes for time-dependent PDEs
- Solving a nonlinear PDE (viscous Burger’s equation)
- Exploring Physics-Informed Neural Networks (PINNs)

> **Deliverables**:  
> - Written report (PDF)  
> - Source code (ZIP)

**Deadline**: Sunday, May 18, 2025, 23:59

---

## Exercise 1: ODE Solver

Implement an adaptive Runge-Kutta solver for ODEs in the form:

y' = f(t, y), y(t₀) = y₀


### Tasks
1. **RK-solver with step control**  
   - Use a local error control criterion:  
     `tol = reps * ||y|| + aeps`

2. **Test Case: Flame Propagation**
   - `y' = y² - y³`, `y₀ = δ`, `t ∈ [0, 2/δ]`
   - Try: δ = 0.02 → 0.0001
   - Relative tolerance: 1e−4
   - Compare with built-in solver
   - Use the Picard–Lindelöf theorem to discuss uniqueness

3. **Step Control via Embedded RK (order 2 & 3)**
   - Use:  
     `E = h * || Σ b̂ⱼ * f(tⱼ, kⱼ) ||`
   - Adjust step size until `E < tol`
   - Measure performance (function calls, steps)

---

## Exercise 2: Parabolic PDE

Solve the heat equation:  
`∂ₜu = ε ∂ₓₓu` on `x ∈ [−1, 1]` with Dirichlet BCs

### Tasks
1. **Discretization (FTCS)**  
   - Forward in time, central in space
   - Use ε = 0.1, test solution in the form:
     `u(x, t) = Σ exp(−εαᵢ²t)[aᵢ cos(αᵢx) + bᵢ sin(αᵢx)]`

2. **Stability Criterion**  
   - Derive condition on h and k (LeVeque §9.3)

3. **Maximum Principle Criterion**  
   - Compare with stability constraint

4. **Convergence Proof**  
   - Use either max principle or Lax-Richtmyer theorem

5. **Code Implementation**  
   - Verify convergence rate

---

## Exercise 3: Hyperbolic PDE

Solve the advection equation:  
`∂ₜu + a ∂ₓu = 0` with periodic BCs

### Tasks
1. **Scheme Selection**
   - Show FTCS is unstable
   - Use FTBS (backward space), prove conditional stability

2. **Code Implementation**
   - Demonstrate convergence of FTBS scheme

3. **Error Analysis**
   - Phase (dispersion) and amplitude (diffusion) errors
   - Predict behavior after 40 wave periods, cr = 0.8
   - Validate prediction via simulation

---

## Exercise 4: Viscous Burger’s Equation

Solve:  
`∂ₜu + ½ ∂ₓ(u²) = ε ∂ₓₓu`

### Tasks
1. **Design Stable Scheme**
   - Combine knowledge from Exercises 2 & 3

2. **Verify with Known Solution**
   - Use: `u(x, t) = -tanh((x + 0.5 − t)/(2ε)) + 1`

3. **Gradient Estimation**
   - New IC: η(x) = −sin(πx), ε = 0.01/π  
   - Estimate `∂ₓu|ₓ=0 ≈ −152.00516` at `t = 1.6037/π`

4. **Efficiency Comparison**
   - Show improved accuracy with fewer points using:
     - Non-uniform grids and/or
     - High-order discretization

5. **Plots and Results**
   - Visualize results and solution profiles

---

## Exercise 5: Physics-Informed Neural Networks (PINNs)

Use a PINN to solve **at least one** of the PDEs above.

### Tasks
1. **Parabolic Case**
   - Visualize solution
   - Tune network architecture
   - Match accuracy of finite difference solution

2. **Hyperbolic Case**
   - Formulate PDE + BC loss
   - Discuss generalization outside training window

3. **Nonlinear Case**
   - Use PINN to solve Burger’s equation
   - Estimate the gradient accurately

4. **Report**
   - Include final plots and details of:
     - Network depth, width
     - Activation functions
     - Training hyperparameters

---

## Notes

- Use plots to verify correctness and convergence
- Annotate your code for readability
- Comment on any assumptions made
