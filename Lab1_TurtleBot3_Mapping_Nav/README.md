# Autonomous Mapping and Navigation with TurtleBot3

## What is this?

A project demonstrating how a TurtleBot3 can map an unknown 3D environment and then autonomously navigate to different waypoints while dodging obstacles. Built using ROS 2 (Humble) and simulated entirely in Gazebo.

---

## Demo

![TurtleBot3 Navigation Demo](docs/images/demo_navigation.gif)

---

## What this project is about

- **SLAM (Simultaneous Localization and Mapping):** The `turtlebot3_cartographer` package builds a 2D occupancy grid map of the Gazebo world by driving the robot through the environment with keyboard teleoperation.
- **Autonomous Navigation:** Once a complete map is generated, it is fed into the ROS 2 Nav2 stack for autonomous path planning.
- **Path Planning:** Using RViz2, a goal position can be set anywhere on the map. The robot calculates the shortest collision-free path and drives there — even reacting to unexpected obstacles on the way.

---

## The Tech Stack

| Component | Tool |
|---|---|
| Robot | TurtleBot3 (Waffle model) |
| Framework | ROS 2 Humble |
| Simulation | Gazebo |
| Visualization | RViz2 |
| SLAM | Cartographer |
| Navigation | Nav2 |

---

## How to Reproduce

> Make sure TurtleBot3 packages and Nav2 are installed before running.

**Step 1 — Launch the Gazebo simulation:**
```bash
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

**Step 2 — Start keyboard teleoperation (new terminal):**
```bash
ros2 run turtlebot3_teleop teleop_keyboard
```

**Step 3 — Run SLAM with Cartographer (new terminal):**
```bash
ros2 launch turtlebot3_cartographer cartographer.launch.py
```
Drive the robot around until the full environment is mapped in RViz2.

**Step 4 — Save the generated map (new terminal):**
```bash
ros2 run nav2_map_server map_saver_cli -f ~/map_world
```
The saved map files are also available in the [`maps/`](maps/) folder of this repo.

**Step 5 — Launch autonomous navigation:**
```bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=true map:=$HOME/map_world.yaml
```

**Step 6 — Set initial pose and navigation goal in RViz2:**
- Use **2D Pose Estimate** to tell the robot where it is on the map
- Use **2D Nav Goal** to set a destination — the robot will plan and drive there autonomously

---

## Key Takeaways

- SLAM builds a probabilistic occupancy grid map incrementally as the robot explores — unknown areas stay grey until the laser scanner reaches them.
- The Nav2 stack separates concerns cleanly: the global planner finds the optimal path, while the local planner handles real-time obstacle avoidance.
- The initial pose estimate is critical — without it, the robot's localization drifts and navigation fails completely.
- Coordinate frames in RViz2 are fundamental: the fixed frame (`map`) vs target frame distinction directly affects how sensor data is visualized.

---

## Output Files

The map generated during this lab is saved in the [`maps/`](maps/) folder:
- `map_world.pgm` — the occupancy grid image
- `map_world.yaml` — map metadata (resolution, origin, thresholds)
