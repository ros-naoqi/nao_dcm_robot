nao_dcm_robot
=============

DCM stack integrating tools to control NAO robot

Installation
------------
- install dependencies

        sudo apt-get install ros-indigo-nao-robot ros-indigo-nao-meshes ros-indigo-nao-control ros-indigo-naoqi-dcm-driver

- then, install [nao_dcm_bringup](https://github.com/ros-naoqi/nao_dcm_robot) or compile it from source

        sudo apt-get install ros-indigo-nao-dcm-bringup

- optionally, install [nao_moveit_config](http://wiki.ros.org/nao_moveit_config)

        sudo apt-get install ros-indigo-nao-moveit-config

How to use it
-------------

**Trajectory control**

To command your robot remotely with ros control :

- first, wake up your robot and choose a stable pose 
 
- start the DCM Bringup providing the robot's IP

        roslaunch nao_dcm_bringup nao_dcm_H25_bringup_remote.launch robot_ip:=<ROBOT_IP>

- you can control the robot using Moveit! (if installed previously)

        roslaunch nao_moveit_config moveit_planner.launch

- or you can send a trajectory to the desired controller (actionlib)

        rosrun actionlib axclient.py <name of the goal topic of the action server>

example:

        rosrun actionlib axclient.py /nao_dcm/LeftArm_controller/follow_joint_trajectory/goal

To choose the controllers you want to load at launchtime you have to modify nao_control/launch/nao_control_trajectory.launch
To know the list of controllers implemented please refer to : nao_control/config/nao_trajectory_control.yaml 
You can start and stop the ros-controllers using the rqt plugin ControllerManager

**Position control**

To command joints positions via ROS:

* start the DCM bringup proving your robot's IP (be aware that the package will stop Autonomous Life on your robot):

        roslaunch nao_dcm_bringup nao_dcm_H25_bringup_position.launch robot_ip:=<ROBOT_IP>

* send a position to the desired controller, for example

        rostopic pub /nao_dcm/LWristYaw_position_controller/command std_msgs/Float64 "data: 0"
