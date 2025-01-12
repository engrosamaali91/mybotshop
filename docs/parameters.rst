Understanding Robot Decision-Making: Local and Global Planners
==============================================================

Now that we have discussed the need to validate safety protocols and data protection policies—and identified each—it is time to explore what makes a robot autonomous. Specifically, we will dive into **how robots make decisions in different scenarios** and how planners influence these decisions during operation.

Robots rely on two types of planners to navigate their environments: **local planners** and **global planners**. Each plays a distinct role in ensuring safe, efficient, and autonomous operation. Take a look at the table below to understand the key differences between them:

.. list-table:: Key Differences Between Local and Global Planners
   :header-rows: 1
   :widths: 20 40 40

   * - **Aspect**
     - **Local Planner**
     - **Global Planner**
   * - **Scope**
     - Handles short-term, real-time navigation and obstacle avoidance.
     - Plans long-term paths from the robot’s start point to its goal.
   * - **Focus**
     - Dynamic obstacle handling and maintaining a smooth, collision-free trajectory.
     - Optimizing the overall route based on the map, environment, and defined goals.
   * - **Frequency**
     - Operates at a higher frequency (e.g., 10 Hz) for real-time adjustments.
     - Operates at a lower frequency (e.g., 1 Hz) to minimize computational overhead.
   * - **Impact on Safety**
     - Ensures immediate responsiveness to nearby obstacles and path deviations.
     - Avoids hazardous routes or areas that could compromise the robot's operation.
   * - **Key Parameters**
     - Velocity limits, inflation radius, yaw tolerance for precise control.
     - Map cost layers, goal tolerance for efficient and safe long-term planning.

.. note::
    Robots leverage these planners to make informed decisions, balancing safety, efficiency, and adaptability in diverse scenarios.

Nav2 Global Planners and Local Controllers
===========================================

The Nav2 stack provides a robust framework for implementing local and global planners, each tailored to specific use cases and operational environments. The table below categorizes the available planners and controllers:

.. list-table:: Nav2 Global Planners and Local Controllers
   :header-rows: 1
   :widths: 20 20 60

   * - **Type**
     - **Name**
     - **Description**
   * - **Global Planner**
     - **NavFn Planner**
     - Utilizes Dijkstra's algorithm to compute the shortest path on a costmap.
   * - **Global Planner**
     - **Smac Planner**
     - Offers different variants, including 2D and Hybrid-A* planners, suitable for various robot types and environments.
   * - **Global Planner**
     - **Theta Planner**
     - Computes paths that are more direct by allowing diagonal movements, reducing unnecessary turns.
   * - **Local Controller**
     - **DWB (Dynamic Window Approach)**
     - Evaluates a set of possible trajectories and selects the one that optimally balances progress toward the goal, speed, and obstacle avoidance.
   * - **Local Controller**
     - **Regulated Pure Pursuit**
     - Focuses on following the global path accurately, adjusting the robot's speed based on proximity to obstacles and path curvature.
   * - **Local Controller**
     - **MPPI (Model Predictive Path Integral)**
     - Uses a model predictive control approach to optimize control commands over a future horizon, considering the robot's dynamics and environmental constraints.
   * - **Local Controller**
     - **Rotation Shim Controller**
     - Handles in-place rotation behaviors, ensuring the robot can correctly orient itself before proceeding along the path.

.. note::
    In the following sections, we will explore how these planners influence robot behavior in specific scenarios:

1. **Going in a Straight Line**  
2. **Navigating Around Static Obstacles**  
3. **Navigating Around Dynamic Obstacles**  

For each scenario, we will analyze how different local and global planners affect safety, efficiency, and overall performance.


Relevant Parameters for Navigation Experiments
==============================================

These are the default parameters of the Nav2 stack. In the following experiments, these parameters will be tweaked for different scenarios, planners, and controllers.

.. list-table:: Navigation Experiment Parameters
   :header-rows: 1
   :widths: 20 25 15 40

   * - **Parameter Group**
     - **Parameter Name**
     - **Value**
     - **Purpose/Description**
   * - **AMCL Configuration**
     - `use_sim_time`
     - `True`
     - Ensures simulation time is used for synchronization.
   * - 
     - `base_frame_id`
     - `base_footprint`
     - Specifies the robot's base frame for localization.
   * - 
     - `global_frame_id`
     - `map`
     - Specifies the global frame for localization.
   * - 
     - `max_particles`
     - `2000`
     - Sets the maximum number of particles for localization accuracy.
   * - 
     - `min_particles`
     - `500`
     - Sets the minimum number of particles for efficiency.
   * - 
     - `transform_tolerance`
     - `1.0`
     - Ensures smooth transform updates.
   * - **Controller Server**
     - `controller_frequency`
     - `20.0`
     - Frequency at which local controllers compute control commands.
   * - 
     - `min_x_velocity_threshold`
     - `0.001`
     - Minimum allowable velocity along the x-axis.
   * - 
     - `FollowPath.max_vel_x`
     - `0.26`
     - Maximum linear velocity in the x-direction.
   * - 
     - `FollowPath.max_vel_theta`
     - `1.0`
     - Maximum angular velocity.
   * - 
     - `FollowPath.sim_time`
     - `1.7`
     - Simulation time for trajectory evaluation.
   * - 
     - `FollowPath.xy_goal_tolerance`
     - `0.25`
     - Tolerance for reaching the goal in the x and y directions.
   * - **Costmap Parameters**
     - `local_costmap.width`
     - `3.0`
     - Defines the width of the local costmap in meters.
   * - 
     - `local_costmap.height`
     - `3.0`
     - Defines the height of the local costmap in meters.
   * - 
     - `local_costmap.inflation_radius`
     - `0.55`
     - Adds a buffer zone around obstacles for safety.
   * - 
     - `global_costmap.inflation_radius`
     - `0.55`
     - Adds a buffer zone in the global map for safety.
   * - **Planner Server**
     - `GridBased.plugin`
     - `nav2_navfn_planner/NavfnPlanner`
     - Uses the NavFn global planner for path computation.
   * - 
     - `GridBased.tolerance`
     - `0.5`
     - Tolerance for reaching the goal in global planning.
   * - 
     - `GridBased.allow_unknown`
     - `true`
     - Allows planning through unknown areas on the map.
   * - **Behavior Server**
     - `cycle_frequency`
     - `10.0`
     - Frequency at which behaviors are checked.
   * - 
     - `transform_tolerance`
     - `0.1`
     - Ensures smooth transform updates for behaviors.
   * - **Velocity Smoother**
     - `smoothing_frequency`
     - `20.0`
     - Frequency of smoothing velocity commands.
   * - 
     - `max_velocity`
     - `[0.26, 0.0, 1.0]`
     - Maximum linear and angular velocities for the robot.
   * - 
     - `max_accel`
     - `[2.5, 0.0, 3.2]`
     - Maximum acceleration limits for the robot.
   * - **General Parameters**
     - `use_sim_time`
     - `True`
     - Enables simulation time for all components.
   * - 
     - `robot_base_frame`
     - `base_link`
     - Specifies the base frame for the robot’s operations.
   * - 
     - `global_frame`
     - `map`
     - Specifies the global frame for navigation.
