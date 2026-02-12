# perez

ROS 2 package for a mobile robot model with Gazebo (Gazebo Sim) integration, RViz visualization, and teleoperation.

## Features

- Xacro-based robot description
- Gazebo Sim launch with ROS ↔ Gazebo bridge
- RViz visualization configs
- Optional joint state GUI and rqt steering

## Requirements

Tested with ROS 2 and Gazebo Sim. You will need:

- ROS 2 (Humble/Iron/Jazzy compatible)
- `ros_gz_sim`
- `ros_gz_bridge`
- `robot_state_publisher`
- `joint_state_publisher_gui`
- `rviz2`
- `xacro`
- `rqt_robot_steering`
- `urdf_launch`

## Build

From your ROS 2 workspace root:

```bash
colcon build --packages-select perez
source install/setup.bash
```

## Launch

### 1) Display the URDF in RViz (no Gazebo)

```bash
ros2 launch perez display.launch.py
```

Optional arguments:

- `gui:=true|false` — enable joint state publisher GUI
- `rvizconfig:=/abs/path/to/config.rviz`
- `model:=urdf/perez_ros.xacro`

### 2) Gazebo Sim + RViz + joint state GUI

```bash
ros2 launch perez gazebo.launch.py
```

This launches Gazebo Sim (empty world), spawns the robot, starts the ROS ↔ Gazebo bridge, runs `robot_state_publisher`, opens RViz, and starts the joint state publisher GUI.

### 3) Gazebo Sim + RViz + rqt steering

```bash
ros2 launch perez perez_gz_drive.launch.py
```

Optional argument:

- `world_file:=/abs/path/to/world.sdf` — Gazebo world file (defaults to `worlds/empty.world`)

## Project Structure

- [CMakeLists.txt](CMakeLists.txt) — CMake build instructions
- [package.xml](package.xml) — ROS 2 package manifest
- [launch/](launch/) — launch files for RViz/Gazebo workflows
  - [launch/display.launch.py](launch/display.launch.py) — RViz display of the URDF
  - [launch/gazebo.launch.py](launch/gazebo.launch.py) — Gazebo Sim + RViz + joint state GUI
  - [launch/perez_gz_drive.launch.py](launch/perez_gz_drive.launch.py) — Gazebo Sim + RViz + rqt steering
- [urdf/](urdf/) — robot description (Xacro)
  - [urdf/perez_ros.xacro](urdf/perez_ros.xacro) — main robot model
  - [urdf/perez_ros.gazebo.xacro](urdf/perez_ros.gazebo.xacro) — Gazebo-specific extensions
  - [urdf/materials.xacro](urdf/materials.xacro) — materials/colors
- [rviz/](rviz/) — RViz configs
  - [rviz/urdf.rviz](rviz/urdf.rviz)
  - [rviz/model.rviz](rviz/model.rviz)
- [config/](config/) — bridge and runtime configs
  - [config/ros_gz_bridge_gazebo.yaml](config/ros_gz_bridge_gazebo.yaml) — ROS ↔ Gazebo bridge config
- [worlds/](worlds/) — Gazebo world files
  - [worlds/empty.world](worlds/empty.world)
- [include/perez/](include/perez/) — C++ headers (if needed)
- [src/](src/) — source files (if needed)
- [CAD File/](CAD%20File/) — CAD assets for the robot
- [LICENSE](LICENSE) — license file

## Notes

- The Gazebo bridge configuration is defined in [config/ros_gz_bridge_gazebo.yaml](config/ros_gz_bridge_gazebo.yaml).
- The robot model is generated from [urdf/perez_ros.xacro](urdf/perez_ros.xacro).
