# MSRR-System
High-Level System and Mediator for Modular Self-Reconfigurable Robot (MSRR)

*by Cheng Jun-Yan*

**Prerequisite:** opencv2, apriltags3, ros, parrot-olympe, parrot-sphinx(for simulation)

This repository contains a MSRR High-Lvel System I developed for the term project in WPI RBE502 ROBOT CONTROL (*Please note that this is not the whole project, it only shows my part in the project*). Final Repors folder contains my part in written final report and final presentation ppt. 

The input of the system is defined by the *Coordinator* which provides the coordinates of all robot modules (implemented by apriltags, coordinated by a drone). *Planner* output a high-level plan which is a sequence of action primitives (by a self-reconfiguration and self-assembly planner). Then the system output which is path or trajectory generated by *Actuator* (implemented by a JPS path planner). And then sent to the robot by *Mediator Server* (use socket to communicate with the high-level system, then relay to other systems(e.g. real robots, ros) with specific protocols). 

This system could be runs on both real robot and simulation by modifying the signals sent by the mediator server. Its a high-level system which means that the system runs regardless of the low-level implementation of real robot (such as motor control). 

#### The Self-Reconfiguration Planning algorithm contained in this system is designed by myself based on many previous literatures (see Final Report - my part). 

## I. How to use:

1.Run BootServer.py (args: 1 for listen ros. none for server., also need run the roscore)

2.Run DroneScript.py (args: 1 for init, none for keep streaming.)

3.Run MSRRScript.py (args: 1 for reset stage, none for continue.)

## II. How to Install Apriltags:

1.Download apriltags from https://github.com/AprilRobotics/apriltag (Or directly use apriltags.zip in /Coordinator)

2.Rename the folder 'apriltags', put it in Coordinator/

3.Enter the folder, then build it:

cmake .

make

## III. How to Activate drone env:

source ~/code/parrot-groundsdk/./products/olympe/linux/env/shell

## IV. How to launch drone simulation:

sudo systemctl start firmwared

sphinx /opt/parrot-sphinx/usr/share/sphinx/drones/anafi4k.drone::stolen_interface=

## V. How to modify

1.Write the MSRRScript.py to plan a high level task

2.Write the DroneScript.py to define the behavior of Drone. Or use Coordinator/drone.py to directly control it.

3.Modify configs.py and also parameters for planner, coordinator and actuator.

## Sample

![image](https://github.com/chengjunyan1/MSRR-System/raw/master/sample.png)
