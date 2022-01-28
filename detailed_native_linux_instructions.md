# Installation Guide for New Linux users
### Date Created: 01/28/2022

Maintainers: Contact Current MEAM520 TAs

# Native Install Instructions (NOT REQUIRED FOR VIRTUAL MACHINE)
---
**NOTE**

We do not recommend that students do this installation.
We have provided a virtual box image, which is supported on Windows and most Linux Distributions as well as a Mac M1 UTM image for those running the Mac M1 with an Arm processor.
This class will not focus on ROS, Bash, or any other skills that you will require to go through this installation.

If you still choose to go through with this installation please read over these instructions carefully. The Teaching Team will point you to this resource when ever possible.

This document will provide resources for installing Ubuntu 20.04, installing ROS noetic, and Installing the panda simulator. Once you have those things setup you can return to the README or the Lab handout to get the course code onto your machine. 

---

## Installing Ubuntu 20.04
You can follow the standard installation instructions for [Ubuntu 20.04](https://phoenixnap.com/kb/install-ubuntu-20-04).

This link will walk you through three main steps:
1. Making a bootable Ubuntu USB device, note a common mistake when doing this for the first time is that making a bootable media is not the equivalent to just copying the downloaded Ubuntu image onto a USB. Please follow the instructions in the link provided.
2. Next you will need to enter your BIOS to select the USB as the bootable drive
3. Once selected you will be taken through a series of GUI windows which will allow you to install and setup your new Ubuntu 20.04 machine.

For specific details please follow the instructions provided in the link above. 

## Installing ROS Noetic
Start here for installing the basics of [ROS noetic](http://wiki.ros.org/noetic/Installation/Ubuntu).

Go to this link, the instructions here are relatively straight forward. You will open a terminal and follow the steps. You want to install the desktop full, and you should go through all of the steps on this link.

If you have not used ROS before a great place to start is with the [ROS Tutorials](http://wiki.ros.org/ROS/Tutorials), which are also found at the end of the installation instructions and are a great resource. 

## Installing the panda_simulator

To get started using this development environment, you must first follow the instructions to install [panda_simulator](https://github.com/justagist/panda_simulator/tree/noetic-devel), a Gazebo-based simulator for the Franka Emika Panda robot.

We will copy the instructions from that git repository here, for more details please see that resource.  

0. Install setup things necessary for later steps

```
$ pip3 install numba scipy future numpy numpy-quaternion
$ sudo apt-get install ros-noetic-libfranka
$ sudo apt-get install ros-noetic-gazebo-ros-control ros-noetic-rospy-message-converter ros-noetic-effort-controllers ros-noetic-joint-state-controller ros-noetic-moveit ros-noetic-moveit-commander ros-noetic-moveit-visual-tools
```

Note if you are copying and pasting from this page please note that there might be typos. You can and should use tab complete when trying to install packages on your computer this helps confirm that the package manager recognizes what you are looking for and that it exists. If there is a typo please let the teaching team know, or if you are a TA fix the typo in these instructions. 


1. Make a ROS Workspace
```
$ mkdir meam520_ws
$ cd meam520_ws
$ mkdir src
```

2. Clone the repository
```
$ cd meam520_ws/src
$ git clone -b noetic-devel https://github.com/justagist/panda_simulator
```

3. Install & Update dependencies
```
$ wstool init
$ wstool merge panda_simulator/dependencies.rosinstall
$ wstool up

# use old ros-compatible version of kdl

$ cd orocos_kinematics_dynamics && rm -rf * && git checkout b35c424e && git reset --hard
$ cd ../.. && rosdep install -y --from-paths src --ignore-src --rosdistro=noetic --skip-keys python-sip
```

4. Build the new packages and set environment variables:
```
$ source /opt/ros/$ROS_DISTRO/setup.bash
$ catkin_make_isolated # if catkin not found, install catkin tools (apt install python-catkin-tools)
$ source devel/setup.bash
```

Note we use catkin_make_isolated instead of catkin build as the original instructions state. 

5. Add the ROS workspace to the `~/.bashrc`: 

```
source ~/meam520_ws/devel_isolated/setup.bash
```

6. If all has been done correctly, you should be able to run

```
roslaunch panda_gazebo panda_world.launch
```

to launch the Gazebo simulation.

## Move back to the README for detailed instructions on how to go about getting the code you will need for this class. 




