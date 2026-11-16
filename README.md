

# RoboDuo Fleet OS

**A smart fleet orchestrator for autonomous warehouses.**

RoboDuo Fleet OS is a browser-based digital twin that shows how a small fleet of autonomous mobile robots (AMRs) can coordinate in a warehouse. Instead of following fixed guide paths, the robots re-plan their routes whenever something changes on the floor, such as a spill, a group of workers, an urgent order or a blocked aisle.

## The Problem

Traditional AMR fleets stall for three reasons:
- **Rigid guide paths:** robots freeze when an unexpected obstacle appears.
- **No context awareness:** a chemical spill and a worker group look like the same wall.
- **Corridor deadlocks:** two robots meeting head-on in a narrow aisle block each other.

## Our Approach

The system uses a three-layer hybrid design:

1. **Event classification:** turns events (spill, worker crowd, urgent medical order, manual obstacle) into hazards and priorities that change what the fleet does.
2. **Grid graph router:** the warehouse is an 18 × 12 grid of 50 px tiles. Breadth-first search finds the shortest open route for each robot, and every new event triggers a fresh re-plan.
3. **Proximity safety shield:** every frame, the distance between the two robots is checked. Under 85 px, AMR-01's current and next cells are reserved and AMR-02 plans a detour around them.

Every decision is written to a **Cognitive Audit Log** in plain English, so each route change can be explained.

## Features

- Two robots with different roles: AMR-01 (Heavy Hauler) and AMR-02 (Agile Unit)
- Live scenarios: chemical spill, urgent medical order (Priority-1 preemption), crowded worker zone
- Click anywhere on the map to drop or clear an obstacle and watch the robots reroute
- Live fleet telemetry with status colours (Active, Rerouting, Priority-1, Yielding)
- Real-time audit log explaining every routing decision

## Performance

Measured by running the simulation logic headlessly:
- Average path calculation: about 0.08 ms
- Full re-plan for both robots: about 0.09 ms

## How to Run

No installation needed. Download or clone this repository and open `index.html` in any modern browser.

## Tech Stack

HTML, CSS and vanilla JavaScript with the Canvas API. No external libraries.

## Documentation

The full presentation is in the repository: `RoboDuo_Fleet_OS_Presentation.pptx`

## Known Limitations and Next Steps

- Only AMR-02 yields during head-on conflicts, so brief contact can still occur.
- Event detection is simulated with buttons; a vision model could feed the same entry points.
- Planned: time-aware coordination between both robots and cost-aware planning (A* / D* Lite).

## Team RoboDuo
- Fardin Rasul Khan: [simulation and ppt design]
- Fahid Hussain: [path finding logic and backend]
