# physics-simulation-infrastructure

Small C++ projects exploring fixed-timestep simulation and how those workloads can be packaged and executed in a reproducible environment.

The repository is split into two parts:

* `Project*` directories → simulation code
* `infra/` → containerization and infrastructure for running simulations as jobs

---

## Projects

### Project1_KinematicMover

Single rigid body advanced under constant force using a semi-implicit Euler step.

Focus:

* Deterministic update loop
* Force → velocity → position integration
* Minimal math + state separation

### Project2_ParticleSystemSim

Independent particle updates similar to CPU-side work done before GPU particle rendering.

Focus:

* Many-body stepping
* Gravity, damping, ground constraint
* Lifetime culling

Each project builds independently with CMake.

---

## Build (Windows)

Requirements:

* Visual Studio 2022
* CMake ≥ 3.20

Use the "x64 Native Tools Command Prompt for VS 2022".

Example:

cmake -S Project1_KinematicMover -B Project1_KinematicMover/build -G "Visual Studio 17 2022"
cmake --build Project1_KinematicMover/build

---

## Infrastructure (in progress)

`infra/` will contain:

* Docker image definitions for simulation runners
* Terraform configuration for provisioning compute to execute them
* Helper scripts for local and remote execution

---

## Intent

The goal is to treat simulation code as a workload that can be executed locally or scheduled remotely, not just as a standalone application.
