================================================================================
APPENDIX B — REALISTIC SCALING & PHYSICAL PARAMETERS
STATUS: PHYSICAL CALIBRATION LAYER
================================================================================

I. PURPOSE
--------------------------------------------------------------------------------
This appendix converts the abstract test case (Appendix A) into physically
realistic conditions.

Goal:
- Apply real-world parameter ranges
- Ensure physically meaningful temperatures
- Enable practical implementation

================================================================================
II. SYSTEM CONTEXT
--------------------------------------------------------------------------------

Target system:
- High-density compute node / server module

Typical characteristics:
- Power per node: 50 – 300 W
- Operating temperature: 300 – 360 K
- Forced air or liquid cooling

================================================================================
III. REALISTIC PARAMETERS
--------------------------------------------------------------------------------

Number of nodes:
    N = 5

Heat capacity (effective):

    C_i = 50 – 200 J/K
    (depends on material + thermal mass)

Cooling coefficient:

    h_i = 5 – 20 W/K

Heat input:

    Q_i = [80, 120, 150, 100, 130] W

Environment temperature:

    T_env = 300 K

================================================================================
IV. STEADY-STATE TEMPERATURES
--------------------------------------------------------------------------------

Formula:

    T_i = T_env + Q_i / h_i

Example (h_i = 10 W/K):

    Node 1:
    T_1 = 300 + 80 / 10 = 308 K

    Node 3:
    T_3 = 300 + 150 / 10 = 315 K

Result:
- All temperatures remain within safe operating range

================================================================================
V. DYNAMICS (REALISTIC TIMESCALES)
--------------------------------------------------------------------------------

Decay rate:

    gamma_i = h_i / C_i

Example:

    gamma_i = 10 / 100 = 0.1 s⁻¹

Interpretation:
- characteristic decay time:
    tau = 1 / gamma_i ≈ 10 s

================================================================================
VI. FLUCTUATION SCALE
--------------------------------------------------------------------------------

Variance:

    Var(Psi_i) ~ k_B * T_i / C_i

Estimate:

    Var(Psi_i) ≈ (1.38e-23 * 300) / 100
               ≈ 4.14e-23

Conclusion:
- Pure thermal fluctuations are extremely small

--------------------------------------------------------------------------------

Practical note:

Observed fluctuations in real systems are dominated by:
- workload variation
- power noise
- control system oscillations

================================================================================
VII. EFFECTIVE NOISE MODEL
--------------------------------------------------------------------------------

Replace ideal thermal noise with:

    xi_i(t) = system-level noise

Sources:
- CPU/GPU load variation
- voltage fluctuations
- fan control dynamics

Model:

    xi_i ~ Gaussian(0, sigma_eff²)

Where:

    sigma_eff >> thermal noise

================================================================================
VIII. STABILITY INTERPRETATION
--------------------------------------------------------------------------------

Stable system:

- high h_i → fast damping
- moderate Q_i → controlled temperature

Unstable system:

- low h_i → slow decay
- high Q_i → thermal buildup

Critical ratio:

    gamma_i = h_i / C_i

→ key stability parameter

================================================================================
IX. ENGINEERING IMPLICATIONS
--------------------------------------------------------------------------------

1. Increase cooling (h_i):
   → improves stability

2. Reduce thermal mass (C_i):
   → faster response but higher sensitivity

3. Balance Q_i:
   → prevents hotspot formation

4. Control noise:
   → reduces fluctuation amplitude

================================================================================
X. LINK TO MODULES
--------------------------------------------------------------------------------

Module 1:
- Provides thermal equations

Module 7:
- Provides fluctuation model

Module 7.2:
- Defines coupling

Module 8–9:
- Validate experimentally

================================================================================
XI. CONCLUSION
--------------------------------------------------------------------------------

This appendix shows:

- The model scales to realistic physical systems
- Temperatures remain within operational limits
- Fluctuations are dominated by system-level effects

Result:

→ Framework is physically applicable to real-world systems

================================================================================
END OF APPENDIX B
================================================================================
