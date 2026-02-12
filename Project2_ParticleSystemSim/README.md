# Particle System Simulation

Simple many-body update similar to CPU particle passes in real-time graphics.

## State per particle

* position
* velocity
* lifetime

## Forces

Gravity:
v ← v + g Δt

Damping:
v ← v · d

Ground constraint:
if y < 0 → clamp and reflect velocity with loss.

Lifetime:
lifetime -= Δt (particle removed when ≤ 0)

## Update order

Emit → Integrate → Apply constraints → Age → Cull

## Notes

* Particles are independent; no pairwise solving.
* Designed to mirror data produced before GPU submission.
