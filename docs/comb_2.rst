Combination 2: NavFn Planner + MPPI Controller
==============================================

This configuration utilizes the **NavFn Planner** for global path planning and the **MPPI (Model Predictive Path Integral) Controller** for local trajectory optimization. This combination is designed to balance efficiency, smoothness, and dynamic obstacle handling.

Why MPPI Controller is a Good Choice
-------------------------------------

The **MPPI Controller** is well-suited for dynamic environments requiring real-time adjustments. It optimizes trajectories by considering the robot’s dynamics and environmental constraints, making it highly effective for:

- **Dynamic Obstacle Avoidance**: Evaluates multiple trajectories to select the optimal path while avoiding collisions.
- **Smooth Path Generation**: Produces jerk-free motions for stable operations.
- **Real-Time Performance**: Delivers responsive and efficient control in dynamic scenarios.


Relevant Parameters for MPPI Controller
---------------------------------------

.. list-table:: MPPI Controller Parameters
   :header-rows: 1
   :widths: 30 20 50

   * - **Parameter**
     - **Value**
     - **Description**
   * - `time_horizon`
     - `1.5`
     - Time horizon over which the trajectory is optimized.
   * - `desired_linear_velocity`
     - `0.5`
     - Target velocity for the robot's linear motion.
   * - `desired_angular_velocity`
     - `1.0`
     - Target velocity for the robot's angular motion.
   * - `linear_acceleration_limit`
     - `2.0`
     - Maximum allowed linear acceleration for smoother motion.
   * - `angular_acceleration_limit`
     - `3.0`
     - Maximum allowed angular acceleration for smoother turns.
   * - `optimizer_iterations`
     - `1000`
     - Number of iterations for trajectory optimization in each cycle.
   * - `cost_weights.path_following`
     - `10.0`
     - Weight for staying close to the planned path.
   * - `cost_weights.collision_avoidance`
     - `15.0`
     - Weight for avoiding collisions with obstacles.
   * - `cost_weights.smoothness`
     - `5.0`
     - Weight for ensuring smooth trajectories.
   * - `lookahead_dist`
     - `0.6`
     - Distance ahead of the robot for trajectory optimization.
   * - `transform_tolerance`
     - `0.1`
     - Tolerance for transform lookups to ensure stability in real-time adjustments.
   * - `visualize_optimizer`
     - `true`
     - Enables visualization of the optimized trajectories for debugging in RViz.

Testing Scenarios and Observations
-----------------------------------

The robot's performance was evaluated under three scenarios using this combination:

1. **Straight-Line Movement**
   - The robot followed a smooth and precise trajectory with minimal drift.
   - Real-time trajectory optimization ensured stable motion.

   .. figure:: media/gifs/comb_2/straightline.webp
      :alt: Straight-Line Movement GIF
      :width: 80%
      :align: center

2. **Navigating Static Obstacles**
   - The controller successfully adjusted the robot's path to avoid obstacles, maintaining smooth transitions.
   - Dynamic trajectory optimization minimized unnecessary deviations.

   .. figure:: media/gifs/comb_2/static.webp
      :alt: Static Obstacles GIF
      :width: 80%
      :align: center

3. **Navigating Dynamic Obstacles**
   - The robot responded effectively to moving obstacles, recalculating the trajectory in real time.
   - The robot maintained a safe distance from the moving object.
   - Optimized control commands reduced delays in avoiding faster-moving objects.

   .. figure:: media/gifs/comb_2/dynamic.webp
      :alt: Dynamic Obstacles GIF
      :width: 80%
      :align: center

Performance Summary
-------------------

.. list-table:: Performance Summary
   :header-rows: 1
   :widths: 30 70

   * - **Scenario**
     - **Performance**
   * - **Straight-Line Movement**
     - Smooth and precise navigation.
   * - **Static Obstacles**
     - Reliable obstacle avoidance with smooth trajectory adjustments.
   * - **Dynamic Obstacles**
     - Effective real-time responses to moving obstacles.


Conclusion
----------

The combination of **NavFn Planner** and **MPPI Controller** provided robust performance across all scenarios. Its ability to handle dynamic obstacles and generate smooth trajectories makes it an excellent choice for complex environments.

**Future Improvements**:
- Further tuning of **cost weights** and **time horizon** could enhance responsiveness in highly dynamic settings.
- Exploring alternate global planners, such as **Smac (Hybrid-A*)**, may yield better path efficiency for intricate environments.
