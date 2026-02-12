# Kinematic Mover

Minimal example of fixed-timestep motion integration.

## Model

Newton's law:

F = m a

With m = 1:

a = F

Discrete update (semi-implicit Euler):

vₙ₊₁ = vₙ + a Δt
xₙ₊₁ = xₙ + vₙ₊₁ Δt

Δt is fixed at 0.016 s.

## Step

Each update:

1. Accumulate force
2. Update velocity
3. Update position
4. Clear force

## Notes

* Deterministic (no frame-time dependence)
* Matches the structure used inside real-time physics stepping
* Intended as a baseline integrator, not a full solver
