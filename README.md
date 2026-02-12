# C++ Simulation Mechanics

This repository contains small, focused C++ projects that explore how real-time simulation systems evolve physical state over fixed timesteps.
The emphasis is on numerical integration, deterministic updates, and patterns commonly used in physics engines and graphics pipelines.

---

## Projects

### Project 1 — Kinematic Mover

**Path:** `Project1_KinematicMover`

A single-body simulation demonstrating deterministic motion under constant force using Semi-Implicit Euler integration.

Focus:

* Fixed timestep update loop
* Force → velocity → position propagation
* Minimal structure used in physics stepping systems

See the project README for mathematical details and implementation notes.

---

### Project 2 — Particle System Simulation

**Path:** `Project2_ParticleSystemSim`

A many-body particle simulation similar to CPU-side updates used for real-time visual effects (sparks, debris, etc.).

Focus:

* Independent particle integration
* Gravity, damping, and collision constraints
* Lifetime management and culling

See the project README for modeling assumptions and equations.

---

## Build Requirements (Windows)

* Visual Studio 2022
* CMake 3.20+
* Use: **x64 Native Tools Command Prompt for VS 2022**

Each project builds independently using its own `CMakeLists.txt`.

---

## Purpose

These examples illustrate how continuous physical laws are approximated numerically in discrete simulation steps—the same core idea underlying real-time physics, robotics simulation, and GPU-driven visualization workflows.

---

## Next Steps (Planned)

* Config-driven simulation runner (headless execution)
* Containerization for reproducible runs
* Cloud deployment using Terraform

---

## Author

Clayton Christudass
