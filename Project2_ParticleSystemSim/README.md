\# Particle System Simulation



\## Purpose



This project scales the integration approach from a single body to many independent particles, similar to systems used in real-time graphics and visual effects.



Each particle evolves under simple forces and constraints and is removed after a finite lifetime.



---



\## Particle Model



Each particle maintains:



\* Position x(t)

\* Velocity v(t)

\* Remaining lifetime



Particles are simulated independently, allowing efficient batch updates.



---



\## Forces Applied



\### Gravity



A constant downward acceleration:



g = (0, −9.8)



Velocity integration:



vₙ₊₁ = vₙ + g Δt



---



\### Damping



Velocity is scaled each frame:



v ← v · d



This approximates drag and prevents unbounded motion.



---



\### Ground Constraint



If a particle penetrates the ground plane:



y < 0 → clamp to y = 0



Velocity reflects with energy loss:



v\_y ← −e v\_y



---



\### Lifetime Decay



Particles age each timestep:



lifetime ← lifetime − Δt



Particles are removed once lifetime ≤ 0.



---



\## Update Pipeline



Emit → Integrate → Apply Forces → Resolve Constraints → Age → Cull



This mirrors CPU-side particle simulation performed before sending data to GPU render buffers.



---



\## Mathematical Interpretation



Each particle numerically solves:



d²x/dt² = g − k v



Using discrete stepping:



vₙ₊₁ = (vₙ + g Δt) d

xₙ₊₁ = xₙ + vₙ₊₁ Δt



This produces damped ballistic trajectories typical of particle effects.



---



\## What This Represents



A simplified version of the update stage used in graphics engines, where thousands of lightweight bodies are advanced every frame prior to rendering.



