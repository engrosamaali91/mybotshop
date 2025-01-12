Combination 1: NavFn Planner + DWB Local Planner
================================================

This experiment evaluates the robot’s navigation capabilities using various combinations of global planners and local controllers from the Nav2 stack. Each combination was tested under three distinct scenarios:

1. **Straight-Line Movement**
2. **Navigating Static Obstacles**
3. **Navigating Dynamic Obstacles**

This configuration employs the **NavFn Planner** for global path planning and the **DWB Local Planner** for local trajectory adjustments.

.. list-table:: Configuration Details
   :header-rows: 1
   :widths: 20 30 20 30

   * - **Component**
     - **Plugin/Server**
     - **Type**
     - **Description**
   * - **Planner Server**
     - `nav2_navfn_planner/NavfnPlanner`
     - Global Planner
     - Computes the shortest path from start to goal using Dijkstra's algorithm on a costmap.
   * - **Controller Server**
     - `dwb_core::DWBLocalPlanner`
     - Local Controller
     - Evaluates possible trajectories and selects the one that optimally balances progress, speed, and obstacle avoidance.

Observations and Results
------------------------

1. **Straight-Line Movement**
   - The robot adhered closely to the planned trajectory with minimal drift.
   - Smooth motion was achieved by tuning parameters such as `max_velocity` and `yaw_goal_tolerance`.

   .. figure:: media/gifs/comb_1/straightline.webp
      :alt: Straight-Line Movement GIF
      :width: 80%
      :align: center

   .. note::
      The scene is speed-forwarded and does not reflect the true speed (0.26 m/s).

2. **Static Obstacles**
   - The robot slowed down at the junction and adjusted its speed.
   - Trajectory adjustments were made by the robot, and it remained on the global path.
   - Minor path deviations were corrected by the local controller.

   .. figure:: media/gifs/comb_1/aroundstatic.webp
      :alt: Static Obstacles GIF
      :width: 80%
      :align: center

3. **Dynamic Obstacles**
   - The robot successfully responded to a moving cube as a placeholder for a moving person but exhibited slight delays when encountering faster objects.
   - The robot did not collide with the moving cube.
   - The robot did not maintain a safe distance, likely due to suboptimal tuning of parameters such as `inflation_radius`, `PathDist.scale`, or `obstacle_max_range` in the local and global costmaps.

   .. figure:: media/gifs/comb_1/DynamicObstacles.webp
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
     - Reliable obstacle avoidance with minor deviations.
   * - **Dynamic Obstacles**
     - Adequate responsiveness to slow-moving obstacles; improvement needed for fast-moving objects and maintaining a safe distance.

Future Considerations
---------------------

- The **TEB Local Planner** could be explored for enhanced handling of dynamic obstacles.
- The **Theta* Global Planner** may be utilized for more direct and efficient path generation.
