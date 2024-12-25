# Digital Twin-Driven Safety Protocol Development for HRI in German Retail Stores
![workflow](nl/workflow.jpg)
Autonomous mobile robots are becoming increasingly intelligent through the integration of Artificial Intelligence (AI). These robots are now capable of making real-time decisions, such as determining optimal paths, navigating around obstacles, and dynamically choosing new routes. With advanced sensors like LiDAR and cameras, robots can detect and respond to both stationary and moving objects, ensuring the safety of people, themselves, and the surrounding environment.

However, to operate safely and effectively, robots must adhere to strict safety protocols and comply with data protection regulations when interacting with humans. This is crucial to minimize risks, especially when deploying autonomous robots in settings such as retail stores or warehouses. Without thorough testing, there is a risk of accidents, injuries, or inventory damage. As a result, authorities have established safety regulations to ensure that robots are designed with compliance in mind.

To address these challenges, MYBOTSHOP is investing significant time and resources into training students to test and validate safety protocols and data protection policies for both new and existing robots within simulation environments. These simulated tests ensure that robots can be safely deployed in real-world scenarios without jeopardizing human lives or privacy.

## Comparision of Simulation Environments

![Simulation Environments](nl/SE.jpg)


Testing autonomous robots in simulation environments is essential to evaluate their performance under both expected and unexpected conditions. This raises an important question: **Which simulation environment is best for testing diverse scenarios?**

To answer this, let’s compare three prominent simulation platforms: **Gazebo Classic**, **Gazebo Fortress**, and **NVIDIA Isaac Sim** (developed by Omniverse). Each platform has unique strengths and limitations, as highlighted in the **comparison chart above**.

- **Gazebo Classic** offers ease of environment setup and a fast simulation speed but lacks support for high-definition simulations and crowd animation. It is a reliable choice for basic ROS2 integration without requiring high-end hardware.
- **Gazebo Fortress** improves on crowd animation and introduces high-definition simulation capabilities. However, it is more resource-intensive and less user-friendly in terms of built-in plugins.
- **NVIDIA Isaac Sim** stands out for its high-fidelity simulation and reinforcement learning support, making it ideal for advanced robotics applications. However, it demands high processing power and has a steeper learning curve for ROS2 integration.

As illustrated in the **image above**, Gazebo Classic excels in simplicity, while NVIDIA Isaac Sim leads in advanced simulation capabilities. Choosing the right platform depends on your project's specific requirements, such as simulation fidelity or hardware limitations.


### Observations on NVIDIA Isaac Sim for Simulation

NVIDIA Isaac Sim is a cutting-edge simulation platform that serves dual purposes: simulation testing and reinforcement learning. In Omni Isaac Gym, robots can be trained effectively for complex tasks. However, while Isaac Sim offers many advantages, as highlighted in the comparison table, it may not always be the best solution for simulations as a test bench.

#### Pros of Isaac Sim:
- High-definition, realistic 3D scenes for immersive simulations.
- Integration with reinforcement learning frameworks for advanced robotic training.
- Built-in examples like Nova Carter robot navigation in warehouse environments.

#### Cons of Isaac Sim:
- Requires high processing power, leading to potential lag in real-time applications.
- Challenges in adapting custom robots and environments, especially with configuring TF for parent-child relations.
- Slower map updates in RViz2, making real-time obstacle detection less reliable.

---

### Real-World Test: Navigation in a Warehouse Environment

![NOVA CARTER ROBOT](https://media.githubusercontent.com/media/NVIDIA-ISAAC-ROS/.github/main/resources/isaac_ros_docs/robots/nova_carter/nova_carter_diagram_front_left.png/)

*[Figure 1: NOVA Carter Robot navigating a warehouse environment.][1]*

[1]: https://media.githubusercontent.com/media/NVIDIA-ISAAC-ROS/.github/main/resources/isaac_ros_docs/robots/nova_carter/nova_carter_diagram_front_left.png/ "Image source: Website Name"

In our observations, we tested the **Nova Carter robot** as show in the image above, for navigation in a small warehouse environment using Isaac Sim. The robot, equipped with 2D and 3D LiDAR, fisheye, and depth cameras, was tasked to navigate static and dynamic obstacles.

- **Static Obstacle Navigation** (Scene 1):  
  The image below depicts Isaac Sim and RViz2 side-by-side, with the robot planning a path around a static object in the warehouse. While the high-definition scene enhances realism, the robot experiences noticeable lag due to the computational demand of the graphics.

  ![Scene_1](carter_navigation_box.gif)

- **Dynamic Obstacle Detection** (Scene 2):  
  For dynamic obstacles, such as a person walking through the environment, the simulation struggled to update the map in real-time. By the time the person was detected and the map updated in RViz2, the person had already moved forward, leaving outdated occupancy marks. This delay compromises the reliability of real-time obstacle detection, an issue tied to the simulation and less likely to occur in real-world scenarios.

  ![Scene_2](carter_with_human.gif)
---

### Tradeoff: Graphics vs. Speed

Isaac Sim’s high graphics quality comes at the cost of simulation speed as show is the image above. This tradeoff poses challenges when trying to create a digital twin of a realistic environment for algorithm testing. A digital twin must ensure safety protocols and accurate real-time processing. When the simulation platform itself becomes a bottleneck, it may be prudent to switch to alternatives like **Gazebo**, which can provide simpler scenes but better support for real-time algorithm testing without compromising safety.

---

### Challenges with Isaac Sim for Custom Robots

Another critical challenge is adapting Isaac Sim nodes for custom robots and environments. For instance:
Configuring TF for custom robots often leads to issues with Isaac Sim’s built-in nodes failing to recognize parent-child relationships, causing delinked transforms. For example the image below shows proper links with parent and child frames.

![Transforms](nl/TFs.png)

Isaac Sim provides several ROS2 nodes for handling TF transforms and odometry, such as:
- **TF Publisher** for sensors and full articulation trees.
- **Raw TF Publisher** for individual transforms.
- **Odometry Publisher** for robot movement tracking.

These nodes can be visualized in the Isaac Sim viewport for better debugging. However, the overhead in adapting and troubleshooting these nodes can be time-consuming.

![Isaac Sim Nodes](https://docs.omniverse.nvidia.com/isaacsim/latest/_images/isaac_tutorial_ros2_odometry_graph_final.png)

### Recommendations

While Isaac Sim is an excellent platform for high-fidelity simulations, it is not always ideal for scenarios requiring speed and efficiency. For testing safety protocols or creating realistic digital twins, alternatives like Gazebo might offer a more balanced solution. High-definition graphics are secondary to the ability to reliably test algorithms under realistic constraints.


### Why Gazebo Classic Can Do the Job Too

Gazebo Classic is a straightforward and reliable simulation platform for robotics. Unlike NVIDIA Isaac Sim, which demands high processing power, Gazebo Classic balances speed, graphics, and computation power, making it a practical choice for many use cases.

#### Features of Gazebo Classic:
- **Ease of Sensor Integration:**  
  Gazebo plugins for both exteroceptive and proprioceptive sensors can be directly added to the robot description. Once configured, the robot can be spawned in a launch file with minimal setup.

- **Customizable Environments:**  
  Gazebo Classic allows custom environments to be designed with ease. Built-in primitives like walls, doors, and other elements can be directly picked and placed within the simulation interface. This feature enables users to create detailed environments even before generating a map.

- **Example: Custom Robot in a Custom Environment**  
  Take a look at the **custom robot in a custom Gazebo Classic environment**.

  ![Gazebo classic environment with custom robot](nl/gazebo_env.gif)

  In this example, the robot operates within a slightly modified environment, featuring walls surrounding the right side of the compound. Such modifications are effortless thanks to the built-in graphical interface.

#### Advantages of Gazebo Classic:
- **Speed:**  
  Gazebo Classic is faster than Isaac Sim because it does not require high-definition simulations. While it is slightly slower than Gazebo Fortress during initial loading, it operates seamlessly once loaded.

- **User-Friendly Interface:**  
  Gazebo Classic’s built-in graphical interface simplifies the process of designing and testing environments for both indoor and outdoor scenarios.

- **Community Support:**  
  As a legacy platform, Gazebo Classic boasts extensive online support and documentation, unlike the relatively newer Gazebo Fortress.

#### Use Cases for Gazebo Classic:
Gazebo Classic is an excellent choice for testing algorithms, designing robots, and simulating indoor and outdoor environments. Later in the experiments the navigation stack was tested on gazebo classic environment. Its combination of moderate computational requirements, reasonable graphics, and faster performance makes it a practical option for those who prioritize functionality over high-definition realism.



