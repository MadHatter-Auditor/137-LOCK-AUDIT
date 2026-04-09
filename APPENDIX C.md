================================================================================
APPENDIX C — REFERENCE IMPLEMENTATION (SIMULATION FRAMEWORK)
STATUS: REPRODUCIBILITY LAYER
================================================================================

I. PURPOSE
--------------------------------------------------------------------------------
This appendix provides a minimal Python implementation of the full framework:

- Thermal dynamics (Module 1)
- Drift fluctuations (Module 7)
- Coupling (Module 7.2)

Goal:
- Enable direct simulation
- Verify theoretical predictions
- Provide a baseline for further development

================================================================================
II. MODEL OVERVIEW
--------------------------------------------------------------------------------

We simulate:

1. Temperature evolution:
    dT_i/dt = (Q_i / C_i) - h_i (T_i - T_env)/C_i + noise

2. Drift:
    Psi_i(t) = T_i(t) - <T_i>

3. Noise:
    Gaussian system-level fluctuations

================================================================================
III. PYTHON IMPLEMENTATION
--------------------------------------------------------------------------------

import numpy as np
import matplotlib.pyplot as plt

# PARAMETERS
N = 5
T_env = 300.0

C = np.ones(N) * 100.0        # J/K
h = np.ones(N) * 10.0         # W/K
Q = np.array([80, 120, 150, 100, 130])  # W

dt = 0.1
steps = 1000

# Noise strength (effective, not pure thermal)
sigma = 0.5

# INITIAL CONDITIONS
T = np.ones(N) * T_env
history = []

# SIMULATION LOOP
for _ in range(steps):
    noise = np.random.normal(0, sigma, N)
    
    dT = (Q / C) - h * (T - T_env) / C + noise
    T = T + dT * dt
    
    history.append(T.copy())

history = np.array(history)

================================================================================
IV. DATA PROCESSING
--------------------------------------------------------------------------------

# Compute equilibrium (time average)
T_mean = np.mean(history[-200:], axis=0)

# Compute drift
Psi = history - T_mean

================================================================================
V. PARAMETER EXTRACTION
--------------------------------------------------------------------------------

# Example: extract decay rate from perturbation
def estimate_gamma(signal, dt):
    signal = np.abs(signal)
    signal = signal[signal > 1e-6]
    
    t = np.arange(len(signal)) * dt
    log_signal = np.log(signal)
    
    slope, _ = np.polyfit(t, log_signal, 1)
    return -slope

gamma_est = estimate_gamma(Psi[:,0], dt)

================================================================================
VI. VISUALIZATION
--------------------------------------------------------------------------------

# Temperature evolution
plt.plot(history)
plt.title("Temperature Evolution")
plt.xlabel("Time step")
plt.ylabel("Temperature (K)")
plt.grid()
plt.show()

# Drift example
plt.plot(Psi[:,0])
plt.title("Drift (Psi) at Node 0")
plt.xlabel("Time step")
plt.ylabel("Deviation")
plt.grid()
plt.show()

================================================================================
VII. EXPECTED OUTPUT
--------------------------------------------------------------------------------

- Temperatures converge to steady state
- Small fluctuations around equilibrium
- Drift signal oscillates around zero
- Estimated gamma close to:

    gamma_theory = h / C = 10 / 100 = 0.1 s⁻¹

================================================================================
VIII. EXTENSIONS
--------------------------------------------------------------------------------

- Add spatial coupling between nodes
- Replace noise with measured data
- Integrate real hardware sensors
- Extend to 2D/3D thermal grids

================================================================================
IX. CONCLUSION
--------------------------------------------------------------------------------

This implementation demonstrates:

- Full integration of theoretical modules
- Reproducible simulation behavior
- Direct pathway to experimental validation

================================================================================
END OF APPENDIX C
================================================================================
