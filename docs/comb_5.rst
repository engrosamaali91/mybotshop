Combination 5: Smac Planner + MPPI
==================================

Navigation Performance: Testing Smac Planner + MPPI Controller
--------------------------------------------------------------

The combination of the **Smac Planner** and **MPPI Controller** represents an advanced setup designed to handle complex navigation scenarios. While the Smac Planner excels at generating smooth, kinematic-aware paths, the MPPI Controller provides real-time trajectory optimization and dynamic obstacle handling.


Testing Scenarios and Observations
-----------------------------------

1. **Straight-Line Movement**  
   - The robot performed satisfactorily, following a smooth and direct path.  
   - No significant deviations or delays were observed.  

   .. image:: media/gifs/comb_5/Straight.webp
      :alt: Straight-Line Movement GIF
      :width: 80%
      :align: center

2. **Navigating Static Obstacles**  
   - The Smac Planner generated a longer path to avoid obstacles.  
   - As the robot approached the goal, it took additional time to stabilize.  
   - The robot struggled slightly when passing through narrow gaps between walls, experiencing delays due to repeated replanning.

   .. image:: media/gifs/comb_5/Static.webp
      :alt: Static Obstacles GIF
      :width: 80%
      :align: center

3. **Navigating Dynamic Obstacles**  
   - The robot detected a moving wheelchair but was less robust in avoiding it compared to the NavFn + MPPI combination.  
   - Multiple replanning attempts were necessary to successfully navigate around the obstacle.  
   - Despite these challenges, the robot ultimately reached the goal.

   .. image:: media/gifs/comb_5/Dynamic.webp
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
     - Smooth and efficient navigation.
   * - **Static Obstacles**
     - Planned longer paths; delays in narrow gaps and stabilizing near the goal.
   * - **Dynamic Obstacles**
     - Detected moving objects but struggled with robustness; required multiple replans.


Conclusion
----------

The combination of **Smac Planner** and **MPPI Controller** demonstrates strong potential for complex environments, particularly in scenarios requiring kinematic awareness and smooth trajectory optimization. However, challenges remain:

- **Static Obstacles**: Path planning and stabilization need improvement for close proximities.
- **Dynamic Obstacles**: Responsiveness to fast-moving objects requires further tuning.

.. note::
    Future Improvements
    - Optimize Smac Planner parameters for shorter paths and quicker stabilization.
    - Fine-tune MPPI cost weights for better responsiveness to dynamic obstacles.
