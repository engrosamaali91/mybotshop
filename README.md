# Assemble a Custom Robot in ISAAC Sim
Connect rigid bodies using joints, add a joint drive to control the joints, turn a chain of joints into an articulation, and control the robot using an Articulation Velocity Controller. [Step by step guide](https://docs.omniverse.nvidia.com/isaacsim/latest/gui_tutorials/tutorial_gui_simple_robot.html#isaac-sim-app-tutorial-gui-simple-robot:~:text=a%20Simple%20Robot-,Assemble%20a%20Simple%20Robot,%EF%83%81,-Omniverse%20Isaac%20Sim%E2%80%99s)

# Add Camera and Sensors
After assembling a custom robot learn how to attach a camera. Isaac Sim provides a variety of sensors that can be used to sense the environment and robot’s state. 
- [Attach camera](https://docs.omniverse.nvidia.com/isaacsim/latest/gui_tutorials/tutorial_gui_camera_sensors.html#isaac-sim-app-tutorial-gui-camera-sensors:~:text=Camera%20and%20Sensors-,Add%20Camera%20and%20Sensors,%EF%83%81,-Isaac%20Sim%20provides) 
- [Attach lidar](https://docs.omniverse.nvidia.com/isaacsim/latest/advanced_tutorials/tutorial_advanced_range_sensor_lidar.html#isaac-sim-app-tutorial-advanced-range-sensor-lidar:~:text=Using%20Sensors%3A%20LIDAR-,Using%20Sensors%3A%20LIDAR,%EF%83%81,-Learning%20Objectives)

Also understand how convention differs in isaac sim environmet and ros environment [Conventions](https://docs.omniverse.nvidia.com/isaacsim/latest/reference_conventions.html#isaac-sim-cameras:~:text=Isaac%20Sim%20Conventions-,Isaac%20Sim%20Conventions,-%EF%83%81)

# Interactive Scripting
This [tutorial](https://docs.omniverse.nvidia.com/isaacsim/latest/gui_tutorials/tutorial_gui_interactive_scripting.html#:~:text=Interactive%20Scripting-,Interactive%20Scripting,-%EF%83%81) covers:
- Script Editor window and Python editing environment
- Isaac Python REPL extension
- Adding a Cube using USD API
- Adding a Cube using Isaac Sim API

# Omnigraph
OmniGraph is Omniverse’s visual programming framework. In simple words OmniGraph is the visual scripting language of Omniverse. Inside Omniverse Isaac Sim, OmniGraph is the main engine for the Replicators, ROS and ROS2 bridges, sensor access, controllers, external input/output devices, UI, and much more.
There are two graph editors, the Action Graph and the Generic Graph. They can both be found under ‘Window > Visual Scripting’. For majority of cases in Isaac Sim,
we will be using Action graphs

Let’s build an action graph to control a robot in Isaac Sim the Jetbot.

Follow this [tutorial](https://docs.omniverse.nvidia.com/isaacsim/latest/gui_tutorials/tutorial_gui_omnigraph.html#isaac-sim-app-tutorial-gui-omnigraph:~:text=22%20/%2000%3A32-,Try%20It%20Out,-%EF%83%81) to import NVIDIA robot 'jetbot' in the scene and create action graph for the differential drive robot 



# Create a bridge between ROS2 and ISAAC sim
First clone turtlebot3 repository in your workspace 
```
git clone -b humble-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
```

Built this package only for the tutorial 
```
cd humble_ws && colcon built --package-select  turtlebot3_description
```
Dont forget to source it
```
source install/setup.bash
```
Go back to isaac sim and import simpl_room environment in a new stage.
Note. Only open isaac sim after building humble_ws otherwise the topic wont appear.


Ensure ros2_bridge extension is enabled. It can be enabled from the Extension Manager by searching for ```omni.isaac.ros2_bridge```. Note ROS and ROS2 bridges cannot be enabled simultaneously. To enable one, make sure the other is disabled first.





