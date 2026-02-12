# C++ Simulation Mechanics

**Deterministic Integration and Real-Time Particle Dynamics**

This repository contains two focused simulation projects implemented in modern C++ that demonstrate how continuous physical systems are approximated numerically in real-time environments such as game engines, robotics simulators, and GPU-driven visualization pipelines.

Rather than solving equations analytically, real-time systems advance state incrementally using numerical integration over small, fixed timesteps. These projects illustrate that process from first principles and scale it from a single rigid body to a many-particle system typical of graphics simulations.

---

# Project 1 — Kinematic Mover

**Location:** `Project1_KinematicMover`

## Objective

To model deterministic motion of a body subjected to a constant force using a fixed timestep integrator.
This demonstrates the foundational update loop used in physics engines and simulation frameworks.

---

## Physical Model

We begin with **Newton’s Second Law of Motion**:

```
F = m a
```

Where:

* `F` = applied force
* `m` = mass
* `a` = acceleration

To simplify the system and isolate integration behavior, we assume:

```
m = 1
```

So the equation reduces to:

```
a = F
```

This means applied force directly determines acceleration.

---

## From Continuous Physics to Discrete Simulation

Physics describes motion using derivatives:

```
a(t) = dv/dt
v(t) = dx/dt
```

A computer cannot evaluate derivatives continuously, so we integrate them numerically over a timestep Δt.

---

## Semi-Implicit Euler Integration

We approximate the integral of acceleration over a small time interval:

```
v(t + Δt) = v(t) + a(t) · Δt
```

Then update position using the *new* velocity:

```
x(t + Δt) = x(t) + v(t + Δt) · Δt
```

This is known as **Semi-Implicit Euler Integration**, chosen because it is:

* Stable for real-time stepping
* Computationally inexpensive (O(1) per body)
* Widely used in real-time physics (PhysX, Bullet, Box2D)

---

## Behavior Under Constant Force

If a constant force is applied:

```
a = constant
```

Then analytically:

```
v(t) = a t
x(t) = (1/2) a t²
```

The simulation reconstructs this quadratic trajectory numerically, frame by frame.

---

## Simulation Loop Structure

Each fixed update performs:

```
Accumulate Forces
→ Integrate Velocity
→ Integrate Position
→ Clear Forces
```

This deterministic stepping ensures identical results across runs, which is essential for reproducibility in simulation and robotics.

---

## What This Project Demonstrates

* Fixed 60 Hz timestep integration
* Deterministic state propagation
* Numerical approximation of continuous motion
* Clean separation of:

  * Math layer (`Vector2`)
  * Physical state (`KinematicBody`)
  * Simulation driver (`main.cpp`)

This mirrors the architecture of real simulation subsystems.

---

# Project 2 — Particle System Simulation (Game Graphics Style)

**Location:** `Project2_ParticleSystemSim`

## Objective

To extend the same integration principles to a many-body system representing particles used in real-time visual effects such as sparks, smoke, and debris.

Unlike rigid body simulation, particles are independent and short-lived, making them ideal for massively parallel evaluation.

---

## Particle State Representation

Each particle maintains:

```
position  → x(t)
velocity  → v(t)
lifetime  → remaining simulation time
```

Particles are stored in a contiguous array, enabling efficient iteration — the same structure used before uploading simulation data to GPU buffers.

---

## Forces Applied

### Gravity

A constant downward acceleration:

```
g = (0, −9.8 m/s²)
```

Velocity update:

```
v(t + Δt) = v(t) + g Δt
```

---

### Damping (Air Resistance Approximation)

To simulate drag, velocity is scaled each frame:

```
v ← v · d
```

Where:

```
0 < d < 1
```

This models exponential decay:

```
v(t) ≈ v₀ e^(−kt)
```

---

### Ground Collision Constraint

If a particle penetrates the ground plane:

```
y < 0
```

We project it back:

```
y = 0
```

And invert velocity with energy loss:

```
v_y ← −e v_y
```

Where:

```
0 < e < 1
```

This mimics inelastic collision response.

---

### Lifetime Decay

Particles exist for finite duration:

```
lifetime ← lifetime − Δt
```

Particles are culled when:

```
lifetime ≤ 0
```

This prevents unbounded growth and mirrors GPU particle lifecycles.

---

## Frame Update Pipeline

Each simulation step executes:

```
Emit New Particles
→ Integrate Motion (Euler Step)
→ Apply Forces (Gravity + Damping)
→ Resolve Constraints (Ground Collision)
→ Age Particles
→ Remove Expired Particles
```

This is structurally identical to CPU-side update stages in real-time rendering engines before issuing draw calls.

---

## Mathematical Interpretation

Each particle independently solves:

```
d²x/dt² = g − kv
```

Numerically approximated as:

```
v_{n+1} = (v_n + g Δt) d
x_{n+1} = x_n + v_{n+1} Δt
```

This produces damped ballistic motion — the classic trajectory used in particle VFX.

---

## What This Project Demonstrates

* Many-body simulation scaling from a shared integrator
* Time-based lifecycle management
* Constraint-based correction instead of analytic collision solving
* CPU-side physics preparation for graphics pipelines
* Real-time simulation structure used in:

  * Game engines
  * Visualization tools
  * GPU particle systems

---

# Build Instructions (Windows + Visual Studio 2022)

Open:

```
x64 Native Tools Command Prompt for VS 2022
```

---

## Build Project 1

```
cmake -S Project1_KinematicMover -B Project1_KinematicMover/build -G "Visual Studio 17 2022"
cmake --build Project1_KinematicMover/build
Project1_KinematicMover/build/Debug/KinematicMover.exe
```

---

## Build Project 2

```
cmake -S Project2_ParticleSystemSim -B Project2_ParticleSystemSim/build -G "Visual Studio 17 2022"
cmake --build Project2_ParticleSystemSim/build
Project2_ParticleSystemSim/build/Debug/ParticleSystemSim.exe
```

---

# Why These Projects Matter

Real-time systems cannot solve physics analytically for complex scenes.
Instead, they evolve state incrementally:

```
state(t + Δt) ≈ state(t) + derivative · Δt
```

This repository demonstrates that core principle at two scales:

| Scale                            | Example                      |
| -------------------------------- | ---------------------------- |
| Single-body deterministic motion | Rigid body stepping          |
| Many-body stochastic motion      | Graphics particle simulation |

Together they illustrate how simulation engines bridge continuous mathematics and discrete computation.

---

# Author

Clayton Christudass
Exploration of numerical simulation, real-time physics integration, and graphics-oriented computation pipelines.
