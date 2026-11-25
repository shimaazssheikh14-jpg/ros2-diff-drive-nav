# ROS 2 Differential Drive Robot Simulation, Mapping and Navigation

## Project Overview

This project implements a differential drive mobile robot using ROS 2 and Gazebo.

The robot is simulated in a virtual environment and is capable of:

- Differential drive robot simulation
- Sensor-based environment perception
- Mapping using SLAM Toolbox
- Robot localization using AMCL
- Autonomous point-to-point navigation using Nav2
- Visualization and navigation through RViz2

The project demonstrates the integration of simulation, mapping, localization, and autonomous navigation in ROS 2.

## Technologies Used

- ROS 2 Humble
- Ubuntu 22.04
- Gazebo
- RViz2
- SLAM Toolbox
- Nav2
- AMCL
- URDF / Xacro

## Project Structure

```text
my_bot/
├── config/
│   ├── mapper_params_online_async.yaml
│   └── nav2_params.yaml
├── description/
│   └── Robot description files
├── launch/
│   ├── launch_sim.launch.py
│   ├── localization_launch.py
│   ├── navigation_launch.py
│   └── online_async_launch.py
├── maps/
│   ├── smap.yaml
│   └── smap.pgm
├── worlds/
│   └── Gazebo world files
├── CMakeLists.txt
├── package.xml
└── README.md
```

## Prerequisites

Install ROS 2 Humble on Ubuntu 22.04.

Make sure the following tools and packages are available:

- Gazebo ROS integration
- RViz2
- SLAM Toolbox
- Nav2
- AMCL
- Map Server

## Build Instructions

Open a terminal and source ROS 2:

```bash
source /opt/ros/humble/setup.bash
```

Navigate to the workspace:

```bash
cd ~/s_ws
```

Install package dependencies:

```bash
rosdep install --from-paths src --ignore-src -r -y
```

Build the package:

```bash
colcon build --packages-select my_bot
```

Source the workspace:

```bash
source ~/s_ws/install/setup.bash
```

## 1. Launch the Robot Simulation

Start the Gazebo simulation:

```bash
ros2 launch my_bot launch_sim.launch.py
```

The differential drive robot will be spawned in the simulation environment.

## 2. Mapping

The environment was mapped using SLAM Toolbox.

The generated map is included in the package:

```text
maps/smap.yaml
maps/smap.pgm
```

The YAML file contains the map resolution, origin, and occupancy thresholds. The PGM file contains the occupancy grid image.

To perform mapping again, launch the SLAM Toolbox configuration provided in the package and move the robot through the environment.

A map can be saved using the ROS 2 map saver:

```bash
ros2 run nav2_map_server map_saver_cli -f ~/s_ws/src/my_bot/maps/smap
```

## 3. Robot Localization

After generating or selecting the saved map, start the localization system.

```bash
ros2 launch my_bot localization_launch.py map:=/home/user/s_ws/src/my_bot/maps/smap.yaml use_sim_time:=true
```

The localization system uses AMCL to estimate the robot's position on the saved map.

In RViz2:

1. Set the Fixed Frame to `map`.
2. Display the map.
3. Select **2D Pose Estimate**.
4. Set the robot's initial position and orientation.

The TF transformation chain is:

```text
map → odom → base_link → base_footprint
```

## 4. Autonomous Navigation

Start Nav2:

```bash
ros2 launch my_bot navigation_launch.py use_sim_time:=true params_file:=/home/user/s_ws/src/my_bot/config/nav2_params.yaml
```

Nav2 provides path planning, motion control, and autonomous navigation.

In RViz2:

1. Select **2D Goal Pose**.
2. Click a destination on the map.
3. Set the desired orientation.
4. The robot will plan a path and move towards the goal.

The robot can be given additional navigation goals after reaching the first destination.

## Expected Results

- Robot successfully spawns in Gazebo.
- The environment is represented by a saved occupancy grid map.
- AMCL estimates the robot's position on the map.
- Nav2 generates a path to the selected destination.
- The robot autonomously navigates to the goal.

## Repository

GitHub Repository:

https://github.com/shimaazssheikh14-jpg/ros2-diff-drive-nav

## Author

ROS 2 Differential Drive Robot Simulation, Mapping and Navigation Project



<img width="1731" height="1098" alt="image" src="https://github.com/user-attachments/assets/bb00f879-19c3-49d4-bf0f-cb7bdca5514e" />
<img width="1731" height="1098" alt="image" src="https://github.com/user-attachments/assets/f9d8a743-20ba-413d-9c22-6eb0571efab9" />
<img width="1731" height="1098" alt="image" src="https://github.com/user-attachments/assets/f58f5556-0309-49e6-b552-29c69d6da17f" />


