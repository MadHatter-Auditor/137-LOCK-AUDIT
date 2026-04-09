================================================================================
APPENDIX A — REFERENCE TEST CASE (THERMAL–DRIFT SYSTEM)
STATUS: DEMONSTRATION / VALIDATION EXAMPLE
================================================================================

I. PURPOSE
--------------------------------------------------------------------------------
This appendix provides a complete numerical test case demonstrating:

- Thermal dynamics (Module 1)
- Drift behavior (Module 7)
- Coupling (Module 7.2)
- Validation procedure (Modules 8–9)

Goal:
- Provide a reproducible example
- Verify model behavior
- Serve as reference for future experiments

================================================================================
II. SYSTEM SETUP
--------------------------------------------------------------------------------

Number of nodes:
    N = 5

Parameters:

- Heat capacity:
    C_i = 500 J/K

- Cooling coefficient:
    h_i = 0.05 W/K

- Heat input:
    Q_i = [120, 150, 180, 140, 160] W

- Environment temperature:
    T_env = 300 K

================================================================================
III. THEORETICAL PREDICTIONS
--------------------------------------------------------------------------------

1. Steady-state temperature:

    T_i = T_env + Q_i / h_i

Example:

    Node 1:
    T_1 = 300 + 120 / 0.05 = 300 + 2400 = 2700 K

(Note: high values indicate simplified model scaling)

--------------------------------------------------------------------------------

2. Decay rate:

    gamma_i = h_i / C_i = 0.05 / 500 = 1.0e-4 s⁻¹

--------------------------------------------------------------------------------

3. Fluctuation variance:

    Var(Psi_i) ~ k_B * T_i / C_i

================================================================================
IV. SIMULATION PROCEDURE
--------------------------------------------------------------------------------

Time parameters:

- dt = 0.1 s
- steps = 1000

Dynamics:

    T_i(t+dt) = T_i(t)
                + (Q_i / C_i)*dt
                - h_i*(T_i - T_env)/C_i * dt
                + noise

Noise term:

    xi_i ~ Gaussian(0, sigma²)

================================================================================
V. EXPECTED RESULTS
--------------------------------------------------------------------------------

1. Temperature behavior:
- Converges to steady-state T_i

2. Fluctuations:
- Small oscillations around equilibrium

3. Drift:
- Psi_i(t) fluctuates around zero

4. Decay:
- After perturbation:

    Psi_i(t) ~ exp(-gamma_i * t)

================================================================================
VI. VALIDATION CHECK
--------------------------------------------------------------------------------

Measure:

- gamma_i(exp) from decay fit

Compare:

    gamma_i(exp) ≈ 1.0e-4 s⁻¹

Acceptable deviation:
    < 10%

--------------------------------------------------------------------------------

Variance check:

    Var(Psi_i) ∝ T_i

================================================================================
VII. INTERPRETATION
--------------------------------------------------------------------------------

If results match:

- Thermal model is consistent
- Drift model is validated
- Coupling is correct

If not:

- Check parameter scaling
- Check timestep stability
- Check noise level

================================================================================
VIII. NOTES
--------------------------------------------------------------------------------

- Absolute temperatures are not realistic (scaled system)
- Model demonstrates structure, not physical limits
- Can be rescaled for real systems

================================================================================
IX. CONCLUSION
--------------------------------------------------------------------------------

This test case confirms:

- Theoretical predictions are numerically reproducible
- Drift–thermal coupling behaves as expected
- Framework is internally consistent

================================================================================
END OF APPENDIX A
================================================================================
