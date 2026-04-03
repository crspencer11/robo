# C++ Robot Simulator + Physics Engine

## Overview

A lightweight 2D robotics simulation engine built in modern C++.

This project focuses on:

* Real-time simulation loops
* Basic physics (movement + collisions)
* Multi-agent systems
* Performance and scalability

The goal is to demonstrate robotics-relevant systems skills without heavy frameworks.

---

## Core Features

* Time-stepped simulation loop
* Robot kinematics (position, velocity)
* Collision detection (robot–robot, robot–world)
* Collision resolution
* Multi-robot support

---

## Tech Stack

* C++17+
* CMake
* (Optional) Eigen (linear algebra)
* (Optional) SDL/OpenGL (visualization)

---

## Project Structure (Target)

```
robot_sim/
├── src/
│  ├── core/    # simulation loop, world
│  ├── physics/ # collision detection/resolution
│  ├── models/  # robot definitions
│  ├── utils/   # math helpers (Vec2, etc)
├── include/
├── tests/
├── CMakeLists.txt
├── README.md
```

---

## Core Concepts

### Simulation Loop

```
while (running) {
    update(dt);
    handle_collisions();
}
```

### Robot Model

Each robot has:

* position (x, y)
* velocity (vx, vy)
* radius (for collisions)

---

## Roadmap

### 1. Basic Simulation (MVP)

Goal: single moving robot

Tasks:

* [ ] Implement `Vec2` struct
* [ ] Create `Robot` struct/class
* [ ] Implement update loop (position += velocity * dt)
* [ ] Add boundary constraints (walls)

Deliverable:

* One robot moving and bouncing in a box

---

### 2. Collision System

Goal: detect and resolve collisions

Tasks:

* [ ] Circle–wall collision detection
* [ ] Circle–circle collision detection
* [ ] Basic collision response (velocity reflection)

Deliverable:

* Robots do not overlap and respond to impacts

---

### 3. Multi-Robot Support

Goal: scale to N robots

Tasks:

* [ ] Store robots in container (vector)
* [ ] Iterate and update all robots
* [ ] Handle pairwise collisions

Deliverable:

* Multiple robots interacting in same world

---

### 4. Performance Optimization (Important)

Goal: avoid O(n^2) bottleneck

Tasks:

* [ ] Implement spatial grid OR quadtree
* [ ] Partition world into cells
* [ ] Only check nearby collisions

Deliverable:

* Scalable simulation (100+ robots)

---

### 5. Event / Messaging Layer (Optional but High Value)

Goal: simulate robotics middleware

Tasks:

* [ ] Implement simple pub/sub system
* [ ] Robots publish state
* [ ] Systems subscribe to updates

Deliverable:

* Decoupled architecture similar to real robotics systems

---

### 6. Path Planning (Optional Extension)

Goal: intelligent movement

Tasks:

* [ ] Implement A* on grid
* [ ] Assign targets to robots
* [ ] Follow planned path

Deliverable:

* Goal-directed robot behavior

---

### 7. Control Systems (Optional Extension)

Goal: realistic motion control

Tasks:

* [ ] Implement PID controller
* [ ] Smooth movement toward targets

Deliverable:

* Stable, realistic motion

---

## How to Build

```
mkdir build && cd build
cmake ..
make
./robot_sim
```

---

## Design Notes

* Keep modules loosely coupled (physics, entities, simulation)
* Prefer simple, testable components
* Optimize only after correctness

---

## Future Improvements

* Visualization layer
* Logging + replay system
* Multi-threaded simulation
* Integration with robotics frameworks (optional)

---

## What This Demonstrates

* Real-time systems design
* Physics simulation fundamentals
* Performance optimization
* Scalable architecture

---

## Notes (For Development)

* Start simple; get end-to-end working early
* Add complexity incrementally
* Validate each stage before moving on
* Prioritize clean ar
