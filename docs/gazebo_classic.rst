Why Gazebo Classic Can Do the Job Too
=====================================

Gazebo Classic is a straightforward and reliable simulation platform for robotics. Unlike NVIDIA Isaac Sim, which demands high processing power, Gazebo Classic balances speed, graphics, and computation power, making it a practical choice for many use cases.

Features of Gazebo Classic
--------------------------

- **Ease of Sensor Integration:**  
  Gazebo plugins for both exteroceptive and proprioceptive sensors can be directly added to the robot description. Once configured, the robot can be spawned in a launch file with minimal setup.

- **Customizable Environments:**  
  Gazebo Classic allows custom environments to be designed with ease. Built-in primitives like walls, doors, and other elements can be directly picked and placed within the simulation interface. This feature enables users to create detailed environments even before generating a map.

- **Example: Custom Robot in a Custom Environment**  
  Take a look at the **custom robot in a custom Gazebo Classic environment**.


.. figure:: media/gifs/gazebo_env.webp                                                              
   :width: 100%                                                                                                                         
   :align: center
                                    
   *Gazebo classic environment with custom robot* 

In this example, the robot operates within a slightly modified environment, featuring walls surrounding the right side of the compound. Such modifications are effortless thanks to the built-in graphical interface.

Advantages of Gazebo Classic
----------------------------

- **Speed:**  
  Gazebo Classic is faster than Isaac Sim because it does not require high-definition simulations. While it is slightly slower than Gazebo Fortress during initial loading, it operates seamlessly once loaded.

- **User-Friendly Interface:**  
  Gazebo Classic’s built-in graphical interface simplifies the process of designing and testing environments for both indoor and outdoor scenarios.

- **Community Support:**  
  As a legacy platform, Gazebo Classic boasts extensive online support and documentation, unlike the relatively newer Gazebo Fortress.

A Drawback: Lack of Realistic Crowd Animation
---------------------------------------------

While Isaac Sim offers realistic crowd animation to test moving humans in a simulated environment, Gazebo Classic does not have this feature. However, Gazebo Classic compensates for this limitation by allowing objects to be dropped in the middle of navigation to test **dynamic obstacle detection**. This functionality ensures that algorithms can still be validated for real-world scenarios involving unexpected obstacles.

Use Cases for Gazebo Classic
----------------------------

Gazebo Classic is an excellent choice for testing algorithms, designing robots, and simulating indoor and outdoor environments. Its combination of moderate computational requirements, reasonable graphics, and faster performance makes it a practical option for those who prioritize functionality over high-definition realism.
