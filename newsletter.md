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

#### A Drawback: Lack of Realistic Crowd Animation
While Isaac Sim offers realistic crowd animation to test moving humans in a simulated environment, Gazebo Classic does not have this feature. However, Gazebo Classic compensates for this limitation by allowing objects to be dropped in the middle of navigation to test **dynamic obstacle detection**. This functionality ensures that algorithms can still be validated for real-world scenarios involving unexpected obstacles.

#### Use Cases for Gazebo Classic:
Gazebo Classic is an excellent choice for testing algorithms, designing robots, and simulating indoor and outdoor environments. Its combination of moderate computational requirements, reasonable graphics, and faster performance makes it a practical option for those who prioritize functionality over high-definition realism.

----

### Gazebo Fortress: The Bridge Between Classic and Modern Simulation

Gazebo Fortress, the successor to Gazebo Classic, brings modern features and improved performance while maintaining the familiar usability of its predecessor. It offers enhanced simulation capabilities, making it a strong contender for robotics testing. However, it also introduces some complexities compared to Gazebo Classic, especially for those migrating existing ROS2 packages.

#### Key Features of Gazebo Fortress:
- **Improved Graphics and High-Definition Simulation:**  
  Gazebo Fortress enhances the graphical fidelity over Classic, offering more immersive environments. While not as graphically detailed as Isaac Sim, Fortress strikes a balance between realism and performance.
- **Better Support for Dynamic Environments:**  
  Fortress introduces features like improved collision detection and smoother handling of dynamic objects, which are critical for testing algorithms involving moving obstacles.
- **Enhanced Plugin Ecosystem:**  
  A rich plugin ecosystem allows for better integration of sensors and actuators, providing more flexibility for robot developers.
- **Support for ROS 2 Packages:**  
  Migrating ROS 2 packages from Gazebo Classic to Fortress is relatively straightforward, thanks to the [migration guide](https://gazebosim.org/docs/fortress/migrating_gazebo_classic_ros2_packages/). However, some adaptation may be needed, especially for custom robots or environments.

#### Example: A Custom Four-Wheel Robot in Gazebo Fortress
Take a look at the **GIF below**, showcasing **a custom four-wheel robot designed in Gazebo Fortress**. The robot demonstrates how Fortress’s enhanced features allow for more detailed and accurate simulations of navigation and other robotic functions.

![Gazebo Fortress Custom Robot Design](nl/fortress_robot.gif)

#### Observations on Gazebo Fortress Environment
The **Gazebo Fortress environment** supports advanced features such as better collision detection and handling of dynamic obstacles. This makes it a suitable choice for testing algorithms in environments requiring higher fidelity than Gazebo Classic while maintaining a manageable computational load compared to Isaac Sim.

#### Observations and Trade-Offs:
- **Performance vs. Graphics:**  
  While Gazebo Fortress improves graphical fidelity, it requires more processing power than Classic, though significantly less than Isaac Sim. This makes it a middle ground between the two platforms.

- **Dynamic Obstacle Handling:**  
  Fortress performs better than Classic in handling dynamic objects, making it suitable for navigation scenarios involving moving humans or obstacles. However, Isaac Sim still leads in dynamic crowd animation.

- **Learning Curve:**  
  For those already familiar with Gazebo Classic, transitioning to Fortress is manageable with the help of the [migration guide](https://gazebosim.org/docs/fortress/migrating_gazebo_classic_ros2_packages/). On the other hand, Isaac Sim’s steep learning curve might pose a challenge for newcomers.

#### Recommendation:
Gazebo Fortress is ideal for those seeking a balance between performance, graphics, and usability. It is particularly well-suited for developers migrating from Gazebo Classic or those looking for advanced features without the heavy computational requirements of Isaac Sim.



---


### Exploring Object Detection with ZED 2i Camera

Before discussing use cases using Navigation2 in ROS2 Humble, I wanted to explore validation in a simulation environment by tackling a hands-on task. To do this, I worked with the industrial-level depth camera **ZED 2i** (refer to the image below).  

Depth cameras are a crucial component of any robot. Acting as the robot's eyes, they enable the robot to not only see objects but also infer their distance from the camera. Unlike standard fisheye cameras, depth cameras like the ZED 2i allow robots to estimate the 3D pose of objects relative to the camera, which is vital for tasks such as navigation and object interaction.

#### Why Depth Cameras Matter
In scenarios where a robot relies heavily on its depth camera:
- **Object Localization:** Depth cameras help estimate the location of objects in the environment while the robot is moving.  
- **Human-Robot Interaction:** They enable robots to classify objects and humans, improving situational awareness in dynamic environments like retail stores.  
- **Pose Estimation:** The 3D pose of objects can be calculated, helping robots identify the orientation and position of objects.  

As shown in the **GIF below**, the robot classified a handbag with approximately 84% accuracy, demonstrating the capability to detect and classify objects. This was achieved using a trained YOLOv8 model, with data preprocessing and augmentation performed using **RoboFlow**.

![3d Object pose detection](nl/Object_detection_wrt_camera_frame.gif)

---

### Why I Chose YOLOv8
I selected the YOLOv8 model for this task because of its flexibility and support for multiple tasks such as detection, classification, and segmentation. Below is a comparison of its key features, which influenced my decision:

| **Feature**                 | **YOLOv8**          | **YOLOv5** | **YOLOv4** |
|-----------------------------|---------------------|------------|------------|
| **Architecture**            | Unified Detection, Segmentation, Classification | Separate models | Separate models |
| **Speed**                   | Faster than YOLOv5 | Moderate   | Slower     |
| **Accuracy**                | Improved           | High       | Moderate   |
| **Supported Modes**         | Detection, Classification, Segmentation | Detection, Classification | Detection only |
| **Ease of Use**             | Intuitive          | Intuitive  | Moderate   |

For more details, refer to the [YOLOv8 documentation](https://docs.ultralytics.com/models/yolov8/).

Additionally, the comparison image below illustrates YOLOv8’s performance metrics relative to previous versions, highlighting its superior speed and accuracy.  

![YOLOv8 Comparison](https://github.com/ultralytics/docs/releases/download/0/yolov8-comparison-plots.avif)  
*Source: [YOLOv8 Documentation](https://docs.ultralytics.com/models/yolov8/)*

These attributes make YOLOv8 a clear choice for real-time robotics applications where detection and classification tasks demand both accuracy and efficiency.


---

### Why I Chose ZED 2i
The **ZED 2i** camera was an ideal choice for this task due to its built-in **body tracking feature**. In dynamic environments like retail stores, where humans are continuously moving, it is critical to track human bodies effectively. The ZED 2i’s advanced capabilities, such as tracking 18 key points of the human body, enable precise and reliable tracking.

> Refer to the [ZED 2i Body Tracking Documentation](https://www.stereolabs.com/docs/body-tracking/) for more details.

Here’s a visual representation of the 18 key points tracked by the ZED 2i camera:  
![Body Tracking Key Points](https://docs.stereolabs.com/body-tracking/images/keypoints_body18.png)

Below is a **GIF of a scene showcasing keypoints being detected in real-time** using the ZED 2i camera:  
![Keypoints Detection GIF](nl/bodytracking.gif)

The GIF illustrates how the ZED 2i camera accurately tracks and detects human movements by identifying body keypoints, ensuring seamless performance in dynamic environments like retail stores.


---

### Outcome and Applications
The combination of the ZED 2i camera and YOLOv8 allowed the robot to:
1. **Classify Objects with High Accuracy:** For example, identifying handbags, as shown in the GIF.  
2. **Track Human Movements:** The built-in body tracking feature ensured accurate tracking of humans, which is crucial in environments like retail stores.  
3. **Process Augmented Data:** Using RoboFlow for data preprocessing and augmentation streamlined the training process and improved detection accuracy.

These insights and tools lay a strong foundation for creating robust object detection systems, especially in settings where robots need to navigate and interact with complex environments efficiently.

---

Would you like any further refinements or additions? Let me know! 😊
