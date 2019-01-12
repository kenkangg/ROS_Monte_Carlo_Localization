
# Simulating Adaptive Monte Carlo Localization

This repository contains a ROS package which localizes a robot in a known map with the use of a 2D LiDAR. Using the estimated pose and the ROS navigation stack, the robot is able to navigate through the environment.

![start_goal](/images/amcl_diagram.png)


## Installation
An installation of the [Robot Operating System (ROS)](http://wiki.ros.org/ROS/Installation) is required to run this package. This package has only been tested on the Kinetic and Melodic distributions of ROS.

Clone this repository into a catkin workspace src directory, and build the package.
```
$ git clone https://github.com/kenkangg/ROS_Monte_Carlo_Localization.git
$
$ cd ~/catkin_ws
$ catkin_make
$ source devel/setup.bash
```

## Usage
The actual usage of this package consists of four steps: launching the Gazebo simulation, localizing the robot, and navigating it to a goal pose.

#### Gazebo Simulation
By launching the udacity_world.launch file, a robot, described in the urdf directory of this repository is placed in the jackal race environment. While this robot is equipped with both a planar laser rangefinder and an rgb camera, only the laser rangefinder is used for localization.
```
$ roslaunch udacity_bot udacity_world.launch
```

#### Localization
The amcl launch file starts the localization node which subscribes to the laser rangefinder, initial pose, robot transforms, and the predefined map. The output of this node is a particle cloud, estimated pose, and odometry transform information. By opening the rviz config file, this information can be easily visualized.
```
$ roslaunch udacity_bot amcl.launch
$ rosrun rviz rviz -d ~/catkin_ws/src/udacity_bot/udacity_bot.rviz
```

#### Navigation
This file is not necessary to run localization, but will send the robot to the pose that is pictured at the beginning of this documentation. A custom goal pose can be chosen by clicking the 2D Nav Goal option at the top of the Rviz GUI and marking the desired location on the map.
```
$ rosrun udacity_bot navigation_goal
```
