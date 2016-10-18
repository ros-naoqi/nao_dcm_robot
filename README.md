nao_dcm_robot
=============

DCM stack integrating tools to control NAO robot

Installation
------------
- install dependencies

        sudo apt-get install ros-indigo-nao-robot ros-indigo-nao-meshes ros-indigo-nao-control ros-indigo-naoqi-dcm-driver

- then, clone the code from [this repo] (https://github.com/ros-naoqi/nao_dcm_robot), documentation [nao_dcm_bringup] (http://wiki.ros.org/nao_dcm_bringup>) and compile

- optionally, install [nao_moveit_config] (http://wiki.ros.org/nao_moveit_config>)
        sudo apt-get install ros-indigo-nao-moveit-config

How to use it
-------------

To command your robot remotely with ros control :

- first, re-start NAOqi without autonomous life

        nao stop
    
        naoqi-bin --disable-life

- export your robot IP address or set it in nao_dcm_bringup/config/nao_dcm.yaml (in old versions)

        export NAO_IP=<your_robot_ip>
    
- then, start the DCM bringup

        roslaunch nao_dcm_bringup nao_dcm_H25_bringup_remote.launch

- you can control the robot using Moveit! (install it previously)

        roslaunch nao_moveit_config moveit_planner.launch

- or you can send a trajectory to the desired controller (actionlib)

        rosrun actionlib axclient.py <name of the goal topic of the action server>

        example:

        rosrun actionlib axclient.py /nao_dcm/LeftArm_controller/follow_joint_trajectory/goal

To choose the controllers you want to load at launchtime you have to modify nao_control/launch/nao_control_trajectory.launch
To know the list of controllers implemented please refer to : nao_control/config/nao_trajectory_control.yaml 
You can start and stop the ros-controllers using the rqt plugin ControllerManager
