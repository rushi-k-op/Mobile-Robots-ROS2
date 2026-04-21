# Autonomous Mapping and Navigation with TurtleBot3

### What is this?
This is a project where I set up a TurtleBot3 to map out an unknown 3D environment and then autonomously drive itself to different waypoints while dodging obstacles. Built this using ROS 2 (Humble) and simulated the whole thing in Gazebo.

### Demo
![TurtleBot3 Navigation Demo](docs/images/demo_navigation.gif)

### What this project is about:
- **SLAM (Simultaneous Localization and Mapping):** used the `turtlebot3_cartographer` package to build a 2D occupancy grid map of a custom Gazebo world.
- **Autonomous Navigation:** Once had a good map, fed it into the ROS 2 Nav2 stack. 
- **Path Planning:** Using RViz2, one can click anywhere on the map to set a goal. The robot calculates the shortest path and drives there.

### The Tech Stack
- **Robot:** TurtleBot3 (Waffle model)
- **Framework:** ROS 2 Humble
- **Simulation & Visualization:** Gazebo and RViz2
- **Core Packages:** Nav2, Cartographer
