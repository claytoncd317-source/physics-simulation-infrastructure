\# Kinematic Mover



\## Purpose



This project demonstrates how continuous motion governed by Newtonian mechanics is approximated numerically using a fixed-timestep integrator.



It models a single body subjected to a constant force and advances its state deterministically over time.



---



\## Physical Basis



Newton’s Second Law:



F = m a



Assuming unit mass (m = 1):



a = F



Acceleration defines how velocity changes:



a = dv/dt



Velocity defines how position changes:



v = dx/dt



Because simulations cannot evaluate derivatives continuously, we integrate them numerically over discrete timesteps.



---



\## Integration Scheme — Semi-Implicit Euler



Velocity update:



vₙ₊₁ = vₙ + a Δt



Position update:



xₙ₊₁ = xₙ + vₙ₊₁ Δt



This method is preferred in real-time systems because it is stable, fast, and deterministic.



---



\## Simulation Loop



Each timestep performs:



1\. Accumulate applied forces

2\. Integrate velocity from acceleration

3\. Integrate position from velocity

4\. Reset forces for next step



A fixed timestep (Δt = 0.016 s) ensures reproducible results independent of frame rate.



---



\## Code Structure



\* `Vector2` — minimal math abstraction

\* `KinematicBody` — stores state and performs integration

\* `main.cpp` — deterministic stepping loop



---



\## What This Represents



This is the foundational update pattern used inside physics engines and simulation frameworks, where state evolves incrementally rather than being solved analytically.



