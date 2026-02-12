\# C++ Kinematic Simulation



\## Overview



This project demonstrates a deterministic kinematic motion model implemented in modern C++ using a fixed timestep update loop and numerical integration.



It simulates how an object's position evolves over time under a constant applied force, following Newtonian mechanics. The implementation mirrors the core update structure used in real-time physics engines, robotics simulators, and interactive simulation environments.



---



\## Mathematical Model



We begin with Newton’s Second Law:



F = ma



For simplicity, mass is assumed to be 1:



a = F



Velocity is the time integral of acceleration:



v(t + Δt) = v(t) + a · Δt



Position is the time integral of velocity:



x(t + Δt) = x(t) + v(t + Δt) · Δt



This stepping method is known as \*\*Semi-Implicit Euler Integration\*\*, a widely used numerical integrator in real-time simulation because of its stability and computational efficiency.



---



\## What the Simulation Shows



A constant force is applied along the X-axis each timestep.

This produces:



\* Linearly increasing velocity

\* Quadratically increasing position over time

\* Deterministic motion under a fixed 60 Hz timestep



The program outputs the evolving state, demonstrating numerical integration of motion.



---



\## Project Structure



```

Project1\_KinematicMover/

│

├── include/          # Public interfaces (Vector2, KinematicBody)

├── src/              # Implementations

├── main.cpp          # Simulation driver loop

└── CMakeLists.txt    # Build configuration

```



The code separates math, state, and simulation stepping to reflect real-world engine organization.



---



\## Build Instructions (Windows + Visual Studio 2022)



Open:



x64 Native Tools Command Prompt for VS 2022



Then run:



cmake -S Project1\_KinematicMover -B Project1\_KinematicMover/build -G "Visual Studio 17 2022"

cmake --build Project1\_KinematicMover/build

Project1\_KinematicMover/build/Debug/KinematicMover.exe



---



\## Example Output



```

Time: 0.016  Position: (0.00768, 0)

Time: 0.032  Position: (0.01536, 0)

Time: 0.048  Position: (0.0256, 0)

```



The increasing spacing between positions reflects constant acceleration.



---



\## Purpose



This repository focuses on the mathematical and architectural foundations of simulation rather than rendering or UI. It demonstrates how continuous physical laws are approximated numerically to evolve state over discrete timesteps.



---



\## Author



Clayton Christudass



