# C++ Simulation Mechanics

This repository contains two focused C++ simulation projects demonstrating core techniques used in real-time physics and graphics systems.

The goal is to show how continuous physical behavior is approximated numerically using fixed-timestep integration—the same pattern used in game engines, robotics simulators, and visualization pipelines.

---

## Project 1 — Kinematic Mover

**Location:** `Project1_KinematicMover`

### Purpose

Demonstrates deterministic motion of a single body under constant force using **Semi-Implicit Euler Integration**.

### Mathematical Model

We begin with Newton’s Second Law:

F = ma

Assuming unit mass:

a = F

Velocity is integrated from acceleration:

v(t + Δt) = v(t) + a · Δt

Position is integrated from velocity:

x(t + Δt) = x(t) + v(t + Δt) · Δt

This produces uniformly accelerated motion and illustrates how simulation steps evolve system state over time.

### What It Shows

* Fixed 60 Hz timestep loop
* Numerical integration of motion
* Separation of math, state, and simulation logic
* Deterministic, reproducible results

---

## Project 2 — Particle System Simulation (Game Graphics Style)

**Location:** `Project2_ParticleSystemSim`

### Purpose

Implements a multi-particle physics system similar to those used for real-time visual effects such as sparks, debris, or smoke.

Each particle is simulated independently using the same integration method but scaled across many bodies.

### Simulation Pipeline

Each frame performs:

Emit → Integrate → Apply Forces → Handle Collision → Age → Cull Dead

### Physics Modeled

* Gravity acceleration
* Velocity damping (air resistance)
* Ground-plane collision with energy loss
* Finite particle lifetime

This mirrors the CPU-side update used before particle data is uploaded to the GPU for rendering.

### What It Shows

* Many-body time integration
* Lifetime management and culling
* Data-oriented simulation loop
* Real-time graphics–style update structure

---

## Build Instructions (Windows + Visual Studio 2022)

Open:

**x64 Native Tools Command Prompt for VS 2022**

---

### Build Project 1

cmake -S Project1_KinematicMover -B Project1_KinematicMover/build -G "Visual Studio 17 2022"
cmake --build Project1_KinematicMover/build
Project1_KinematicMover/build/Debug/KinematicMover.exe

---

### Build Project 2

cmake -S Project2_ParticleSystemSim
