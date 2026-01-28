# ROS2 Gazebo Simulation for AgileX Bunker in the Lehrforst

TODO: add scout

![Gazebo Simulation Image](img/gazebo_bunker.png)


## Requirements

- [ROS2 jazzy](https://docs.ros.org/en/jazzy/Installation.html)
- [Gazebo](https://gazebosim.org/docs/harmonic/ros_installation/)


## Installation

Create directory
```bash
mkdir -p bunker_simulation/src
cd bunker_simulation/src
```

Clone repo
```bash
git clone https://github.com/hcai-lab-vienna/ros_gz_bunker_lehrforst_sim.git
```

Build
```bash
cd ..
colcon build --symlink-install
```

## Simulation

Start with
```bash
source install/setup.bash
ros2 launch ros_gz_bunker_lehrforst_sim bunker_in_lehrforst_sim.launch.xml
```

After starting simulation control with arrow keys (press 's' for break) inside Gazebo or via ros with
```bash
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

Alternatively you can publish to `/cmd_vel` for control commands.

Other ROS2 topics:
- `/bunker/odometry` simulated odometry data
- `/bunker/pose` position data in the simulation grid (to approx GNSS)
- `/bunker/tf` transform data over time
- `/bunker/imu` simulated imu
