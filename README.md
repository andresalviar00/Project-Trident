# Project Trident

Project Trident is a distributed autonomous maritime fleet simulator built to explore software engineering concepts used in robotics, autonomous systems, mission planning, networking, telemetry, and command-and-control applications.

The project simulates multiple autonomous surface vessels completing civilian maritime missions while navigating around obstacles, communicating with a mission server, reporting telemetry, and responding to failures.

> **Current status:** Early development
> This repository is being built incrementally as part of a project-based autonomous-systems learning roadmap.

---

## Project Goals

The main goals of Project Trident are to:

* Simulate autonomous vessels in a two-dimensional maritime environment.
* Implement waypoint navigation and path-planning algorithms.
* Model vessel behavior using finite-state machines.
* Simulate sensors, communication delays, packet loss, and equipment failures.
* Support communication between multiple vessels.
* Create a backend mission-control service.
* Stream live vessel telemetry to an operator dashboard.
* Test the system under normal and failure conditions.
* Measure mission performance through repeatable experiments.
* Practice professional software development using Git, GitHub, testing, documentation, containers, and continuous integration.

---

## Planned System Architecture

```text
┌────────────────────────────────────────────┐
│         Command-and-Control Dashboard      │
│       React • TypeScript • Live Map        │
└─────────────────────┬──────────────────────┘
                      │ REST API / WebSocket
┌─────────────────────▼──────────────────────┐
│             Mission-Control Server         │
│        Python • FastAPI • PostgreSQL       │
└─────────────────────┬──────────────────────┘
                      │ Telemetry / Commands
┌─────────────────────▼──────────────────────┐
│          Autonomous Vessel Simulator       │
│             Modern C++ • CMake             │
│                                            │
│ Navigation • State Machines • Sensors      │
│ Path Planning • Networking • Logging       │
└─────────────────────┬──────────────────────┘
                      │
             Simulated Environment
```

The initial versions will be smaller than this final architecture. Features will be added gradually and documented through GitHub commits, issues, and milestones.

---

## Planned Features

### Vessel Simulation

* Vessel position, heading, speed, and battery state
* Time-step-based movement
* Waypoint navigation
* Multiple simulated vessels
* Configurable vessel properties
* Mission completion tracking

### Autonomous Navigation

* Finite-state-machine behavior
* A* path planning
* Static obstacle detection
* Dynamic obstacle avoidance
* Route replanning
* Return-to-home behavior
* Emergency-stop behavior

### Simulated Sensors

* GPS position
* Compass heading
* Obstacle detection
* Battery monitoring
* Configurable sensor noise
* Delayed and dropped readings
* Simulated sensor failures

### Fleet Communications

* Vessel identification
* Telemetry messages
* Heartbeat monitoring
* Communication timeouts
* Packet-loss simulation
* Shared obstacle reports
* Stale-message rejection
* Reconnection handling

### Mission Control

* Mission creation
* Vessel assignment
* Waypoint management
* Mission start and abort commands
* Live telemetry streaming
* Alerts and health monitoring
* Mission history
* Mission replay

### Testing and Reliability

* C++ unit tests
* Python unit and API tests
* Integration tests
* Automated mission scenarios
* Failure injection
* Deterministic simulation seeds
* Performance measurements
* Continuous integration

---

## Technology Stack

The planned technology stack includes:

| Area                         | Technology                                |
| ---------------------------- | ----------------------------------------- |
| Autonomous vessel simulation | Modern C++                                |
| Build system                 | CMake                                     |
| Backend API                  | Python and FastAPI                        |
| Database                     | PostgreSQL                                |
| Dashboard                    | React and TypeScript                      |
| Real-time communication      | WebSockets                                |
| Vessel communication         | TCP, UDP, or ROS 2 concepts               |
| Testing                      | GoogleTest, Pytest, and integration tests |
| Containers                   | Docker and Docker Compose                 |
| Continuous integration       | GitHub Actions                            |
| Version control              | Git and GitHub                            |

Technologies may change as the project develops and new requirements are discovered.

---

## Repository Structure

```text
project-trident/
├── autonomy/          # C++ vessel and autonomy software
├── mission-server/    # Python mission-control API
├── dashboard/         # React command-and-control interface
├── simulation/        # Maps, scenarios, and simulation configuration
├── tests/             # Integration and system-level tests
├── docs/              # Architecture and engineering documentation
├── scripts/           # Development and automation scripts
├── .github/           # GitHub Actions and repository templates
├── README.md
└── LICENSE
```

The structure may evolve as the project becomes more complex.

---

## Development Roadmap

### Phase 1: C++ Simulation Foundation

* [ ] Configure the C++ and CMake project
* [ ] Create the initial vessel-state model
* [ ] Implement position, heading, speed, and battery
* [ ] Add simulation time steps
* [ ] Implement waypoint movement
* [ ] Add input validation
* [ ] Add initial unit tests
* [ ] Add structured logging

### Phase 2: Navigation and Autonomy

* [ ] Create the vessel state machine
* [ ] Implement mission and waypoint classes
* [ ] Create a two-dimensional maritime grid
* [ ] Add static obstacles
* [ ] Implement breadth-first search
* [ ] Implement Dijkstra’s algorithm
* [ ] Implement A* path planning
* [ ] Add route replanning
* [ ] Add emergency-stop behavior

### Phase 3: Sensors and Communications

* [ ] Simulate GPS and compass readings
* [ ] Add configurable sensor noise
* [ ] Add delayed and dropped sensor readings
* [ ] Create a telemetry-message format
* [ ] Build a telemetry receiver
* [ ] Implement vessel heartbeats
* [ ] Detect communication loss
* [ ] Support multiple vessels
* [ ] Add shared obstacle reports

### Phase 4: Mission-Control Server

* [ ] Create the FastAPI project
* [ ] Add vessel endpoints
* [ ] Add mission endpoints
* [ ] Add input validation
* [ ] Add PostgreSQL persistence
* [ ] Store telemetry and mission events
* [ ] Add WebSocket telemetry streaming
* [ ] Add API and integration tests

### Phase 5: Operator Dashboard

* [ ] Create the React and TypeScript application
* [ ] Display the fleet
* [ ] Display live vessel positions
* [ ] Display planned routes
* [ ] Show battery and mission status
* [ ] Display system alerts
* [ ] Create missions through the interface
* [ ] Add mission-history and replay views

### Phase 6: Reliability and Deployment

* [ ] Add failure-injection scenarios
* [ ] Add randomized mission tests
* [ ] Add Dockerfiles
* [ ] Configure Docker Compose
* [ ] Configure GitHub Actions
* [ ] Add health checks and metrics
* [ ] Create a complete demonstration scenario
* [ ] Publish performance results

---

## Initial Vessel States

The autonomy system is planned to support states such as:

```text
IDLE
PLANNING
NAVIGATING
AVOIDING_OBSTACLE
RETURNING_HOME
LOW_BATTERY
COMMUNICATION_LOST
EMERGENCY_STOP
MISSION_COMPLETE
```

Transitions between these states will be explicit, testable, and documented.

Example:

```text
NAVIGATING + battery below safe threshold
→ RETURNING_HOME
```

Safety-related conditions will take priority over normal mission progress.

---

## Example Telemetry Message

A vessel may eventually send telemetry in a format similar to:

```json
{
  "vessel_id": "TRIDENT-01",
  "timestamp": 0,
  "position": {
    "x": 125.4,
    "y": 82.1
  },
  "heading": 145.0,
  "speed": 4.8,
  "battery": 76.5,
  "state": "NAVIGATING"
}
```

The final message format will be versioned and documented in the repository.

---

## Planned Performance Metrics

Project Trident will measure:

* Mission success rate
* Collision count
* Mission-completion time
* Distance traveled
* Number of route replans
* Communication messages transmitted
* Communication-loss duration
* Telemetry latency
* Battery consumption
* Simulation-step processing time

These measurements will support controlled experiments involving communication range, packet loss, sensor noise, fleet size, and obstacle density.

---

## Testing Philosophy

The project will use several testing levels:

1. **Unit tests** for individual classes and functions.
2. **Integration tests** for communication between components.
3. **Scenario tests** for complete autonomous missions.
4. **Failure tests** for network loss, sensor failure, and invalid data.
5. **Randomized tests** for unexpected combinations of environmental conditions.
6. **Regression tests** to prevent previously fixed bugs from returning.

A random seed will be recorded whenever possible so that failed simulations can be reproduced.

---

## Current Progress

### Completed

* [x] Defined the initial project idea
* [x] Selected the main project goals
* [x] Created the initial system architecture
* [x] Created the development roadmap
* [x] Initialized the GitHub repository
* [x] Added the initial README

### Currently Working On

* [ ] Creating the initial C++ project
* [ ] Configuring CMake
* [ ] Implementing the first `VesselState` model
* [ ] Writing the first unit tests

---

## Running the Project

The project is not yet ready for a complete release.

Initial build and execution instructions will be added after the first C++ simulation milestone is complete.

The expected C++ workflow will eventually resemble:

```bash
cmake -S . -B build
cmake --build build
./build/project_trident
```

Exact commands may change as the repository structure develops.

---

## Documentation

Engineering documentation will be maintained in the `docs/` directory.

Planned documents include:

* `architecture.md`
* `requirements.md`
* `state-machine.md`
* `network-protocol.md`
* `testing-strategy.md`
* `failure-analysis.md`
* `performance-results.md`
* `security-considerations.md`

---

## Project Background

This project expands on previous experience modifying a decentralized swarm-robotics simulation.

That project involved:

* C++ development
* Autonomous-agent behavior
* Range-limited robot communication
* Distributed information sharing
* Simulation configuration
* Repeatable experiments
* Performance comparisons
* Debugging and technical presentation

Project Trident applies similar distributed-autonomy ideas to a simulated maritime environment while adding navigation, networking, mission control, telemetry, testing, and deployment.

---

## Learning Objectives

Through this project, I intend to strengthen my knowledge of:

* Modern C++
* Python backend development
* Data structures and algorithms
* Linux development
* Computer networking
* Autonomous-system architecture
* Robotics communication patterns
* Multithreading and concurrency
* API design
* Databases
* Testing and debugging
* Docker and continuous integration
* Technical documentation
* Engineering communication

---

## Safety and Scope

Project Trident is an educational software simulation.

It is designed around civilian maritime scenarios such as environmental surveying, navigation research, fleet coordination, and search operations. It does not control real vessels and does not implement weapons or targeting systems.

---

## License

A license has not yet been selected.

Before publishing reusable code, an appropriate open-source license will be added to this repository.

---

## Author

**Andres Alviar**

Computer Science graduate developing skills in autonomous systems, distributed software, simulation, networking, and software integration.

** alexander manrique jr** 

cd grad may2026
---

## Project Status

**Actively under development**

Progress, design decisions, experiments, failures, and lessons learned will be documented throughout the repository.
