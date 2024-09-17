# Why did we choose isaac sim 
![Isaac sim workflow](./isaac.svg)

# Assemble a Custom Robot in ISAAC Sim
Connect rigid bodies using joints, add a joint drive to control the joints, turn a chain of joints into an articulation, and control the robot using an Articulation Velocity Controller. [Step by step guide](https://docs.omniverse.nvidia.com/isaacsim/latest/gui_tutorials/tutorial_gui_simple_robot.html#isaac-sim-app-tutorial-gui-simple-robot:~:text=a%20Simple%20Robot-,Assemble%20a%20Simple%20Robot,%EF%83%81,-Omniverse%20Isaac%20Sim%E2%80%99s)

## Add Camera and Sensors
After assembling a custom robot learn how to attach a camera. Isaac Sim provides a variety of sensors that can be used to sense the environment and robot’s state. 
- [Attach camera](https://docs.omniverse.nvidia.com/isaacsim/latest/gui_tutorials/tutorial_gui_camera_sensors.html#isaac-sim-app-tutorial-gui-camera-sensors:~:text=Camera%20and%20Sensors-,Add%20Camera%20and%20Sensors,%EF%83%81,-Isaac%20Sim%20provides) 
- [Attach lidar](https://docs.omniverse.nvidia.com/isaacsim/latest/advanced_tutorials/tutorial_advanced_range_sensor_lidar.html#isaac-sim-app-tutorial-advanced-range-sensor-lidar:~:text=Using%20Sensors%3A%20LIDAR-,Using%20Sensors%3A%20LIDAR,%EF%83%81,-Learning%20Objectives)

Also understand how convention differs in isaac sim environmet and ros environment [Conventions](https://docs.omniverse.nvidia.com/isaacsim/latest/reference_conventions.html#isaac-sim-cameras:~:text=Isaac%20Sim%20Conventions-,Isaac%20Sim%20Conventions,-%EF%83%81)

## Interactive Scripting
This [tutorial](https://docs.omniverse.nvidia.com/isaacsim/latest/gui_tutorials/tutorial_gui_interactive_scripting.html#:~:text=Interactive%20Scripting-,Interactive%20Scripting,-%EF%83%81) covers:
- Script Editor window and Python editing environment
- Isaac Python REPL extension
- Adding a Cube using USD API
- Adding a Cube using Isaac Sim API

## Omnigraph
OmniGraph is Omniverse’s visual programming framework. In simple words OmniGraph is the visual scripting language of Omniverse. Inside Omniverse Isaac Sim, OmniGraph is the main engine for the Replicators, ROS and ROS2 bridges, sensor access, controllers, external input/output devices, UI, and much more.
There are two graph editors, the Action Graph and the Generic Graph. They can both be found under ‘Window > Visual Scripting’. For majority of cases in Isaac Sim,
we will be using Action graphs

Let’s build an action graph to control a robot in Isaac Sim the Jetbot.

Follow this [tutorial](https://docs.omniverse.nvidia.com/isaacsim/latest/gui_tutorials/tutorial_gui_omnigraph.html#isaac-sim-app-tutorial-gui-omnigraph:~:text=22%20/%2000%3A32-,Try%20It%20Out,-%EF%83%81) to import NVIDIA robot 'jetbot' in the scene and create action graph for the differential drive robot 



# Create a bridge between ROS2 and ISAAC sim
## Driving TurtleBot via ROS2 messages
First clone turtlebot3 repository in your workspace 
```
git clone -b humble-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
```

Built this package only for the tutorial 
```
cd humble_ws && colcon built --packages-select  turtlebot3_description
```
Dont forget to source it
```
source install/setup.bash
```
Go back to isaac sim and import simple_room environment  and turtlebot3 in a new stage.
Note. Only open isaac sim after building humble_ws otherwise the topic wont appear.


Ensure ros2_bridge extension is enabled. It can be enabled from the Extension Manager by searching for ```omni.isaac.ros2_bridge```. Note ROS and ROS2 bridges cannot be enabled simultaneously. To enable one, make sure the other is disabled first.

Play the scene and the topics will be displayed in a terminal. 
check if the topic ```cmd_vel``` is ready to subscribe angular and linear velocities.

```
ros2 topic list
```
Now that a differential base topic is setup, a twist message can be published to /cmd_vel topic to control the robot. Let’s drive it forward with the command:
```
ros2 topic pub /cmd_vel geometry_msgs/Twist "{'linear': {'x': 0.2, 'y': 0.0, 'z': 0.0}, 'angular': {'x': 0.0, 'y': 0.0, 'z': 0.0}}"
```
To stop the robot from moving, publish a zero velocity command:
```
ros2 topic pub /cmd_vel geometry_msgs/Twist "{'linear': {'x': 0.0, 'y': 0.0, 'z': 0.0}, 'angular': {'x': 0.0, 'y': 0.0, 'z': 0.0}}"
```
To make it easier for us to move the Turtlebot around, install the teleop_twist_keyboard by running the following command:
```
sudo apt-get install ros-$ROS_DISTRO-teleop-twist-keyboard
```
Enable driving using the keyboard by running:
```
ros2 run teleop_twist_keyboard teleop_twist_keyboard
```

Follow this [tutorial](https://docs.omniverse.nvidia.com/isaacsim/latest/ros2_tutorials/tutorial_ros2_drive_turtlebot.html#getting-started:~:text=ROS2%20Twist%20message-,Getting%20Started,%EF%83%81,-Important) to understand these ros2 bridge with isac sim concepts

- Drive the robot using the Differential Controller and the Articulation Controller
- Introduction to ROS2 Bridge omnigraph nodes
- Subscribing to a ROS2 Twist message


If you are strictly following the tutorials of isaac sim please do not forget to apply the differential controller on your two wheeled custom robot.
I applied it on custom robot and i am able to control it using keyboard just like turtlebot.

## ROS2 Cameras
Understand how to publish camera and perception data in ROS2.
[attach a camera and visualize it in rviz](https://docs.omniverse.nvidia.com/isaacsim/latest/ros2_tutorials/tutorial_ros2_camera.html#:~:text=ROS2%20Cameras-,ROS2%20Cameras,-%EF%83%81)

Please note we can always use ros2 plugins from isaac utils/common_omni_graphs -> ROS2 Camera, for depth image i was not able to visulize depth image because the camera in isac sim was placed too far away. If needed please adjust the camera position so that tht depth is rendered appropriately.

Also understand how to label objects in isaac sim using replicator but this is an optional [replicator](https://docs.omniverse.nvidia.com/isaacsim/latest/replicator_tutorials/tutorial_replicator_getting_started.html#isaac-sim-app-tutorial-replicator-getting-started:~:text=Overview%20and%20Getting%20Started-,Overview%20and%20Getting%20Started,%EF%83%81,-Isaac%20Sim%20Replicator%20is)

To understand how to publish using python scripts please follow this tutorial(must) [publish using python script](https://docs.omniverse.nvidia.com/isaacsim/latest/ros2_tutorials/tutorial_ros2_camera.html#isaac-sim-app-tutorial-ros2-camera:~:text=image%20is%20limited.-,Additional%20Publishing%20Options,%EF%83%81,-To%20publish%20images)


Even though ros clock is not immediately necessary to sync to either simulation time or system time but it is good to understand the concept of simulation time and ros time. [ROS clock](https://docs.omniverse.nvidia.com/isaacsim/latest/ros2_tutorials/tutorial_ros2_clock.html#isaac-sim-app-tutorial-ros2-clock:~:text=ROS2%20Clock-,ROS2%20Clock,-%EF%83%81)



## Lidar with ROS2
Learn how to interface lidar with ros2. [tutorial](https://docs.omniverse.nvidia.com/isaacsim/latest/ros2_tutorials/tutorial_ros2_rtx_lidar.html#:~:text=RTX%20Lidar%20Sensors-,RTX%20Lidar%20Sensors,-%EF%83%81)

This tutorial covered creating and using the RTX Lidar Sensor with ROS2:

- Adding a RTX Lidar sensor

- Adding a RTX Lidar and PointCloud ROS2 nodes.

- Displaying multiple sensors in RViz2.

Meaning of omni verse nodes used to publish lidar pointcloud and laser scan:
- On playback tick: triggers all the nodes once played
- Isaac Run One Simulation Frame: This is the node to running the create render product pipeline once at the start to improve performance.
- ROS2 Context: This node creates a ros2 context for a given domain id.
- Isaac Create Render Product: Create a render product. target prim select the RTX Lidar.
- ROS2 RTX Lidar Helper: This node will handle publishing of the laser scan message from the rtx lidar
- If you wish to also publish point cloud data, add another ROS2 RTX Lidar Helper node, and under input type select point_cloud and change the topic name to point_cloud. 



When i set the frameid to ```world```  i could see the laser scan as well as camera topic however when i set the frameid to ```sim_lidar``` i could only see camera topic in rviz. You can either make your own action graph for lidar by following the [guide](##lidar-with-ros2)


Now learn how to add global and relative transforms to a TF tree in next section.
[ROS2 Transform Trees and Odometry](https://docs.omniverse.nvidia.com/isaacsim/latest/ros2_tutorials/tutorial_ros2_tf.html#isaac-sim-app-tutorial-ros2-tf:~:text=Trees%20and%20Odometry-,ROS2%20Transform%20Trees%20and%20Odometry,%EF%83%81,-Learning%20Objectives)




## ROS2 Transform Trees and Odometry
The issue realated to frameid could be resolved if following topics are cover in this tutorial.


lets track the camera’s position in the global frame.
Add two cameras i.e ```camera_1```  and ```camera_2``` to a TF tree and add an action graph to both the prims of cameras and publish their TF's and visulaize their orientation in rviz
