# DeliBot_Real

## Requirements

To make your computer capable of ejecute all the scripts and make them work together, some installatins are needed.

| Plugin | Description |
| ------ | ------ |
| CUDA Toolkit 11.0 | [From the official page without drivers.][CUDA] |
| cuDNN | [Last version of cuDNN for CUDA 11.x][cuDNN] for CUDA configuration. |
| Anaconda | To get the requirements needed. |
| requirements.txt | Create enviroment with reuirements:  conda create --name <environment_name> --file requirements.txt . |

## Connect to he robot:

In order to connect to the robot you have to add some parameters in your _.bashrc_ archive:
```sh
export ROS_MASTER_URI=http://<IP_Robot>:11311
export ROS_HOSTNAME=<IP_PC>
```

Then use the following command in a terminal:
```sh
ssh turtlebot@<IP_Robot>
```
or
```sh
ssh tb2@<IP_Robot>
```

Once you have done that, you should be in the robot. Now, to use it you must add some parameters in the robot's _.bashrc_ archive:

```sh
export ROS MASTER URI=http://localhost:11311
export ROS HOSTNAME=<IP_Robot>
```

## Steps for execution:

Once you get all the requirements, you must follow some steps to archieve the results.

First, you must compile the DeliBot folder as a ROS workspace. From a terminal:
```sh
conda activate <environment_name>
cd <route_to_DeliBot_root>
catkin_make
```

It's compulsory to export the path of the folder as a parameter and it's recomended to include it in the _.bashrc_ archive:
```sh
export DELIBOT_PATH=<path_of_folder>
```

In addition, it is important that you follow the steps below in each terminal before executing the rest of the scripts:
```sh
conda activate <environment_name>
cd <path_to_DeliBot_folder>
source devel/setup.bash
```

__The next step is executing the scripts in the terminals, in the robot:__


First Tab:
```sh
roslaunch turtlebot_bringup minimal.launch
```
Second Tab:

```sh
roslaunch turtlebot_bringup hokuyo_ust10lx.launch
```
Third Tab:
```sh
export TURTLEBOT_3D_SENSOR=astra
roslaunch turtlebot_navigation gmapping_demo.launch
```

Fourth Tab:
```sh
roslaunch turtlebot_navigation amcl_demo.launch map_file:=<path_of_the_map>
```
Fifth Tab:

```sh
roslaunch turtlebot_rviz_launchers view_navigation.launch
```
When it is opened, you have to calibrate it moving around the robot with the following command.

Third Tab:
```sh
roslaunch turtlebot_teleop keyboard_teleop.launch
```
After a few movements you have to stop the teleoperation.

__Also executing the scripts in the terminals, in the personal computer:__

First Tab:
```sh
roslaunch turtlebot3_gazebo Office_world.launch
```
When gazebo have been loaded, you must remove the _waffle_ turtlebot.

Second Tab:

```sh
roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=<path_to_DeliBot_folder>/Delibot/src/siam-mot/Office.yaml
```
When rviz have been loaded, you must adjust the _burger_ turtlebot to the correct position with ''2D Pose Estimate''.



Otherwise, if you just want to take a new photo for a employee, in the personal computer:

First Tab:
```sh
roscore
```

Second Tab:
```sh
rosrun my_code setup.py
```

## References

Some references that have been crucial to achieve the main objective are:

- [Turtlebot3] - Repository needed to use turtlebot3.
- [Turtlebot3_simulations] - To get the results in simulation.
- [SiamMOT] - To get the bounding box of the people detected.
- [Maskrcnn-benchmark] - Ass the main tool of SiamMot.
- [Face Recognition] - To compare the person in search to the person in the bbox.
- [Kobuki_msgs] - To communicate with the real robot.

   [CUDA]: <https://developer.nvidia.com/cuda-11.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=2004&target_type=runfilelocal>
   [cuDNN]: <https://developer.nvidia.com/rdp/cudnn-archive>
   [Turtlebot3]: <https://github.com/ROBOTIS-GIT/turtlebot3/tree/noetic-devel>
   [Turtlebot3_simulations]: <https://github.com/ROBOTIS-GIT/turtlebot3_simulations/tree/noetic-devel>
   [SiamMOT]: <https://github.com/amazon-science/siam-mot>
   [Maskrcnn-benchmark]: <https://github.com/facebookresearch/maskrcnn-benchmark>
   [Face Recognition]: <https://github.com/ageitgey/face_recognition>
   [Kobuki_msgs]: <https://github.com/yujinrobot/kobuki_msgs>
