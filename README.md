# ROS 2 Multi-Robot Coordination System

## Overview

This project simulates a distributed multi-robot system using ROS 2, focusing on real-time communication, coordination, and task scheduling.

The goal is to demonstrate systems-level thinking applied to robotics software, including:

* Pub/sub messaging
* Distributed coordination
* Real-time constraints
* Fault tolerance and observability

---

## Architecture

### High-Level Design

* Multiple robot nodes publish state
* A central coordinator assigns tasks
* Communication happens via ROS 2 topics

Core components:

* `robot_node` (C++): publishes state, consumes tasks
* `coordinator_node` (C++): aggregates state, assigns tasks
* `simulation` (Gazebo): environment + physics

---

## Tech Stack

* ROS 2 (Humble or Iron)
* C++17
* Python (optional tooling)
* Gazebo (simulation)

---

## Repository Structure (Target)

```
ros2_multi_robot/
├── src/
│   ├── robot_msgs/          # Custom message definitions
│   ├── robot_node/          # Robot implementation
│   ├── coordinator_node/    # Task scheduler
│   └── simulation/          # Gazebo world + configs
├── launch/
│   ├── multi_robot.launch.py
├── config/
│   ├── params.yaml
├── docs/
│   ├── architecture.md
│   ├── design_decisions.md
├── README.md
```

---

## Roadmap (Execution Plan)

This section doubles as a checklist for building the system.

---

### 1. ROS 2 Fundamentals

Goal: Understand core ROS 2 abstractions

Tasks:

* [ ] Install ROS 2 (Humble or Iron)
* [ ] Complete basic tutorials (nodes, topics)
* [ ] Write a minimal publisher node (C++)
* [ ] Write a minimal subscriber node (C++)
* [ ] Understand:

  * [ ] Topics
  * [ ] Nodes
  * [ ] QoS policies

Deliverable:

* Simple pub/sub working locally

---

### 2. Custom Message Definitions

Goal: Define structured communication between components

Tasks:

* [ ] Create `robot_msgs` package
* [ ] Define:

```
RobotState.msg
float64 x
float64 y
float64 vx
float64 vy
string robot_id
```

```
RobotTask.msg
string robot_id
float64 target_x
float64 target_y
```

* [ ] Build and verify message generation

Deliverable:

* Custom messages usable across nodes

---

### 3. Single Robot Node

Goal: Simulate one robot publishing state

Tasks:

* [ ] Implement `robot_node` in C++
* [ ] Publish `RobotState` at fixed frequency
* [ ] Add configurable robot_id
* [ ] Add basic motion logic (e.g., linear movement)

Deliverable:

* One robot publishing valid state messages

---

### 4. Simulation Integration (Gazebo)

Goal: Visualize robot in a simulated environment

Tasks:

* [ ] Install Gazebo
* [ ] Create simple world file
* [ ] Spawn robot model
* [ ] Connect simulation state to ROS topics

Deliverable:

* Robot visible and moving in simulation

---

### 5. Multi-Robot System

Goal: Scale from 1 → N robots

Tasks:

* [ ] Launch multiple robot instances
* [ ] Implement namespacing OR shared topic strategy
* [ ] Ensure unique robot IDs
* [ ] Validate concurrent publishing

Design decision (document this):

* Namespaced topics vs shared topic

Deliverable:

* Multiple robots publishing simultaneously

---

### 6. Coordinator Node (Core Logic)

Goal: Central system for task assignment

Tasks:

* [ ] Implement `coordinator_node`
* [ ] Subscribe to all robot states
* [ ] Maintain in-memory state store
* [ ] Publish `RobotTask` messages

Basic logic:

* Assign random or fixed targets
* Reassign when target reached

Deliverable:

* End-to-end loop: state → task → robot movement

---

### 7. Coordination & Collision Avoidance

Goal: Introduce multi-agent reasoning

Tasks:

* [ ] Detect proximity between robots
* [ ] Implement simple avoidance logic
* [ ] Adjust velocity or reassign tasks

Deliverable:

* Robots avoid collisions in simulation

---

### 8. Observability (High Impact)

Goal: Make system debuggable and measurable

Tasks:

* [ ] Add structured logging
* [ ] Measure:

  * [ ] message latency
  * [ ] publish frequency
* [ ] Visualize in RViz

Deliverable:

* Ability to inspect system behavior in real time

---

### 9. Performance & Failure Handling (Optional)

Goal: Simulate real-world constraints

Tasks:

* [ ] Introduce artificial delays
* [ ] Handle dropped messages
* [ ] Detect stale robot state
* [ ] Tune QoS settings

Deliverable:

* System behaves reasonably under degraded conditions

---

## How to Run (Target)

```
colcon build
source install/setup.bash
ros2 launch multi_robot.launch.py
```

---

## Design Considerations

### Centralized vs Decentralized

* Current system uses centralized coordinator
* Tradeoffs:

  * Simpler logic
  * Single point of failure

### Scaling

* Bottlenecks:

  * Coordinator CPU
  * Network throughput

### Reliability

* ROS QoS tuning required for:

  * reliability
  * latency

---

## Future Improvements

* Decentralized coordination
* Advanced planning (A*, RRT)
* Sensor fusion
* Real robot deployment (Raspberry Pi / TurtleBot)

---

## Why This Project Matters

This project demonstrates:

* Real-time distributed systems
* Robotics middleware usage
* C++ systems programming
* Multi-agent coordination

It is designed to align with robotics SWE roles, autonomy platforms, and infrastructure teams.

---

## Notes (For Myself)

* Focus on correctness over realism initially
* Prioritize end-to-end system early
* Iterate on complexity after working baseline
* Document every design decision for interview discussion