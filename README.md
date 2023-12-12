# The rb1_ros2_desc_ctr package

This package contains a ROS2 robot model description for Robotnik's RB-1 mobile base. 

## Table of Contents

- [Introduction](#Introduction)
- [Instalation](#Instalation)
- [Simulation](#Simulation)
- [Controller activation](#Controller activation)
- [Moving the robot's lifting unit](#Moving the robot's lifting unit)

## Introduction

This ROS2 package is destinanted to implement ROS2 CONTROL FRAMEWORK in order to practice its usage in simulated robots. You are going to be able to activate
the actuator controller drivers of a RB1 Robot and make the test and investigation you requiere. 

## Instalation 

In order to be able to make this package work you must to follow the next steps:

    1- Download this repositories https://github.com/Romu10/ROS2_CONTROL_RB1.git
    2- Go to the CLI 
    3- Go to you workspace: /ros2_ws
    4- Compile: colcon build
    5- Source your workspace: source/install/setup.bash

## Simulation

To start the simulation you must to follow the following steps:

    1- Go to your work space: /ros2_ws
    2- Use the next command to launch the simulation: ros2 launch rb1_ros2_description rb1_ros2_xacro.launch.py
    
    if the simulation is launched properly you will see 3 grean lines in the same window you are running the command.
        
        - The 3 lines: [spawner-5] [INFO] [1702338649.928748582] [spawner_joint_state_broadcaster]: Configured and started joint_state_broadcaster
                       [spawner-7] [INFO] [1702338652.016002776] [spawner_effort_controllers]: Configured and started effort_controllers
                       [spawner-6] [INFO] [1702338655.073203486] [spawner_rb1_base_controller]: Configured and started rb1_base_controller
    
    This indicate that the controller have been launched correctly, so you are gonna be able to play around with the robot. 

## Controller activation

If you run the command specified in the past topic, the controller will be activated automatically. But if you want to activate it by your own, just follow the next step:

    - Activate the joint_state_broadcaster: ros2 control load_controller --set-state start joint_state_broadcaster
    - Activate the rb1_base_controller: ros2 control load_controller --set-state start rb1_base_controller
    - Activate the effort_controllers: ros2 control load_controller --set-state start effort_controllers --> This controller activate the lifting unit.

## Moving the robot's lifting unit

In order to activate the lifting unit or deactivate it you just need to use the following commnds:

    - For lift down: ros2 topic pub /effort_controllers/commands  std_msgs/msg/Float64MultiArray "data:
                     - 0" -1

    - For lift up: ros2 topic pub /effort_controllers/commands  std_msgs/msg/Float64MultiArray "data: 
                     - 1" -1


## Disclaimer:  
This package only modifies/adapts files from these repositories/packages:  
- [RobotnikAutomation/rb1_base_sim](https://github.com/RobotnikAutomation/rb1_base_sim) licensed under the BSD 2-Clause "Simplified" License
- [RobotnikAutomation/rb1_base_common/rb1_base_description](https://github.com/RobotnikAutomation/rb1_base_common/tree/melodic-devel/rb1_base_description), licensed under the BSD License
- [RobotnikAutomation/robotnik_sensors],(https://github.com/RobotnikAutomation/robotnik_sensors) licensed under the BSD License