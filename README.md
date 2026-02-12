# physics-simulation-infrastructure

C++ simulation examples paired with infrastructure for running them as reproducible workloads.

This repository is less about graphics or UI and more about how simulation code is structured, built, and eventually deployed.

---

## About The Repository

The code explores fixed-timestep numerical simulation and how those executables can be treated as batch jobs instead of standalone apps.

Two simulation examples are included today, with infrastructure support being added alongside them.

---

## Projects

### Project1_KinematicMover

Single-body motion integrated under constant force.

Used to isolate the core update step found in real-time physics systems.

### Project2_ParticleSystemSim

Many independent particles advanced under gravity, damping, and a ground constraint.

Represents the CPU simulation stage typically run before rendering particle effects.

---

## Getting Started

Requirements:

* Visual Studio 2022
* CMake 3.20+

Use the Visual Studio Native Tools prompt.

Build example:

cmake -S Project1_KinematicMover -B Project1_KinematicMover/build -G "Visual Studio 17 2022"
cmake --build Project1_KinematicMover/build

Each project can be built independently the same way.

---

## Usage

Run the executables directly from their build directories.
They produce console output showing state evolution over time.

No rendering is included. These are compute-only simulations.

---

## Infrastructure

The `infra/` directory is being developed to support:

* Containerizing simulation runners
* Provisioning compute resources with Terraform
* Executing simulations as repeatable jobs

---

## Roadmap

Next additions:

* Project3_SimRunner (config-driven batch simulation)
* Docker packaging
* Terraform deployment for remote execution

---

## Notes

The goal is to bridge the gap between writing simulation code and operating it as part of a reproducible compute pipeline.
