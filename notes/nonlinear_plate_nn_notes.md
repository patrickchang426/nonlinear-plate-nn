# Neural Network Analysis of Nonlinear Vibrations of a Rectangular Plate

## Reference Paper
Seo Il Chang (1993)  
**Studies in Non-linear Multi-mode Responses of Harmonically Excited Rectangular Plates with Internal Resonances**  
PhD Dissertation, Purdue University

---

# 1. Research Goal

Analyze the **nonlinear vibration response of a rectangular plate** using a **fully connected neural network (FCNN)**.

The neural network will learn the nonlinear mapping between system parameters and vibration responses derived from a **reduced-order model (Galerkin approximation)** of the plate.

Main objective:

> Can a neural network learn the nonlinear frequency-response behavior and modal interactions of a harmonically excited rectangular plate?

---

# 2. Physical Model

The plate dynamics are described using the **von Kármán plate equations**, which account for geometric nonlinearity.

General form: w_tt + D∇⁴w + nonlinear terms = external forcing


Where:

- `w(x,y,t)` : transverse displacement
- `D` : bending stiffness
- nonlinear terms arise from membrane stretching

---

# 3. Model Reduction (Galerkin Method)

The displacement field is expanded in modal functions.


w(x,y,t) = Σ W_mn(t) φ_m(x) ψ_n(y)


For a reduced-order model:


w(x,y,t) ≈ q1(t) φ1(x,y) + q2(t) φ2(x,y)


This converts the PDE into a **set of nonlinear ODEs** for modal coordinates.

Typical form:


q̈1 + ω1² q1 + nonlinear coupling terms = forcing
q̈2 + ω2² q2 + nonlinear coupling terms = forcing


This captures **internal resonance** between vibration modes.

---

# 4. Nonlinear Phenomena in the System

Important dynamical behaviors studied in the paper:

### Internal Resonance
Energy transfer between modes when


ω1 ≈ ω2


or other rational relations.

### Bifurcation
Types observed:

- Saddle-node bifurcation
- Pitchfork bifurcation
- Hopf bifurcation

### Chaos

Possible behaviors include:

- period doubling
- quasi-periodic motion
- chaotic attractors

---

# 5. Neural Network Approach

A **Fully Connected Neural Network (FCNN)** will be used to approximate the nonlinear response.

The NN acts as a **surrogate model** for the reduced-order dynamical system.

---

# 6. Input Variables (NN Features)

Possible inputs:


ω : excitation frequency
F : forcing amplitude
c : damping coefficient
α : nonlinear coupling parameters
β : plate geometry parameters
IC : initial conditions


Example input vector:


x = [ω, F, c, q1(0), q2(0)]


---

# 7. Output Variables (NN Targets)

### Option A — Steady-state response


A1 : amplitude of mode 1
A2 : amplitude of mode 2


### Option B — Time response


q1(t)
q2(t)


### Option C — Regime classification


Periodic
Quasi-periodic
Chaotic


Recommended starting point:

> Predict steady-state modal amplitudes.

---

# 8. Training Data Generation

Training data will be generated using **numerical simulation of the reduced-order model**.

Steps:

1. Implement reduced-order ODE system
2. Perform parameter sweep over:
   - excitation frequency
   - forcing amplitude
   - damping
3. Integrate equations over time
4. Extract steady-state modal amplitudes
5. Store data for training

Example dataset format:


ω , F , c , q1(0) , q2(0) , A1 , A2


---

# 9. Neural Network Architecture

Example FCNN structure:


Input layer : 5
Hidden layer : 128 neurons
Hidden layer : 128 neurons
Hidden layer : 128 neurons
Output layer : 2


Activation function:


tanh


Recommended architecture:


MLP: 5 → 128 → 128 → 128 → 2


---

# 10. Loss Function

Basic regression loss:


L = MSE(A_pred , A_true)


Possible extensions:


L = L_data + λ L_physics


Where:

- `L_data` : prediction error
- `L_physics` : residual of governing ODE

---

# 11. Challenges

### Multi-valued response

Nonlinear systems can have multiple solutions for the same excitation frequency.

Example:

- stable branch
- unstable branch
- jump phenomenon

Possible solutions:

- include initial conditions as inputs
- train separate networks for different branches
- use mixture density networks

---

# 12. Research Roadmap

### Step 1 — Implement reduced-order model

- two-mode Galerkin model
- include nonlinear coupling

---

### Step 2 — Generate simulation dataset

Parameter sweep:


ω
forcing amplitude
damping
initial conditions


---

### Step 3 — Train neural network

Inputs:


ω , F , c , q1(0) , q2(0)


Outputs:


A1 , A2


---

### Step 4 — Evaluate model

Compare with numerical integration:

- frequency response curve
- resonance peak prediction
- modal coupling behavior

---

### Step 5 — Advanced extensions

- Physics-informed neural networks
- Bifurcation prediction
- Chaos detection
- Reduced-order model correction

---

# 13. Possible Research Topics

### 1. Internal resonance prediction using neural networks

Predict onset of modal interaction.

---

### 2. Frequency response surrogate modeling

Replace numerical continuation with neural networks.

---

### 3. Dynamical regime classification

Classify system behavior:


Periodic
Quasi-periodic
Chaotic


---

### 4. Hybrid physics–ML model


ẋ = f_physics(x, μ) + f_NN(x, μ)


The neural network corrects modeling errors.

---

# 14. Recommended First Experiment

Minimal experiment:

1. Implement **two-mode reduced-order ODE**
2. Generate response data via time integration
3. Train FCNN to predict steady-state modal amplitudes
4. Compare predicted and simulated frequency-response curves

---

# End of Research Note
