Navigation Performance and Suitability for Safety Scenarios
===========================================================

.. list-table:: Performance Summary
   :header-rows: 1
   :widths: 30 20 20 20 20 20

   * - **Global Planner + Local Controller**
     - **Straight-Line Movement**
     - **Static Obstacles**
     - **Dynamic Obstacles**
     - **Obstacle Clearance**
     - **Dynamic Obstacle Handling**
   * - **NavFn + DWB**
     - ✅
     - ✅
     - ❌
     - Good
     - Moderate responsiveness
   * - **NavFn + MPPI**
     - ✅
     - ✅
     - ✅
     - Excellent
     - Highly responsive
   * - **NavFn + RPP**
     - ✅
     - ❌
     - ❌
     - Average (struggles in gaps)
     - Slow
   * - **Theta_* + RPP**
     - ✅
     - ✅
     - ❌
     - Excellent
     - Slow
   * - **Smac Planner Hybrid + MPPI**
     - ✅
     - ✅
     - ❌
     - Bad
     - Moderate responsiveness


.. note::

    - **✅**: Suitable
    - **❌**: Not Suitable
    - **Obstacle Clearance**: Describes the ability to navigate close proximities without collisions (e.g., Excellent, Good, Bad).
    - **Dynamic Obstacle Handling**: Describes the responsiveness to moving obstacles (e.g., Highly responsive, Moderate, Slow).


.. important::
   Controllers perform differently based on drive types (e.g., differential, Ackermann), impacting navigation results. Proper pairing and tuning are crucial for optimal performance.

.. note::
   Different drives may give varying results.

Planner Suitability for Different Robot Types
=============================================

.. list-table:: Planner Suitability for Robot Types
   :header-rows: 1
   :widths: 20 20 20 20 20 20 20

   * - **Planner Name**
     - **Circular Differential**
     - **Circular Omnidirectional**
     - **Non-Circular Ackermann**
     - **Non-Circular Legged**
     - **Non-Circular Differential/Omnidirectional**
     - **Arbitrary**
   * - **NavFn Planner**
     - ✅
     - ✅
     - ❌
     - ❌
     - ❌
     - ❌
   * - **Smac Planner 2D**
     - ✅
     - ✅
     - ❌
     - ❌
     - ❌
     - ❌
   * - **Theta* Planner**
     - ✅
     - ✅
     - ❌
     - ❌
     - ❌
     - ❌
   * - **Smac Hybrid-A* Planner**
     - ✅
     - ✅
     - ✅
     - ✅
     - ✅
     - ❌
   * - **Smac Lattice Planner**
     - ❌
     - ❌
     - ✅
     - ✅
     - ✅
     - ✅

.. note::

    - **✅**: Suitable for this type of robot.
    - **❌**: Not suitable for this type of robot.

    This table provides a clear summary of which planner is best suited for each type of robot, helping users make informed decisions based on their robot's design and operational needs.

.. note::
   Not all controllers are suitable for all robot tasks; it depends on the type of robot as well as the task being performed.

Controller Suitability for Different Robot Types and Tasks
==========================================================

.. list-table:: Controller Suitability for Robot Types and Tasks
   :header-rows: 1
   :widths: 20 20 20 20 20 40

   * - **Controller Name**
     - **Differential**
     - **Omnidirectional**
     - **Ackermann**
     - **Legged**
     - **Primary Task**
   * - **DWB Controller**
     - ✅
     - ✅
     - ❌
     - ❌
     - Dynamic obstacle avoidance
   * - **MPPI Controller**
     - ✅
     - ✅
     - ✅
     - ✅
     - Dynamic obstacle avoidance
   * - **RPP Controller**
     - ✅
     - ❌
     - ✅
     - ✅
     - Exact path following
   * - **Rotation Shim**
     - ✅
     - ✅
     - ❌
     - ❌
     - Rotate to rough heading
   * - **VP Controller**
     - ✅
     - ❌
     - ✅
     - ✅
     - High-speed path tracking

.. note::

    - **✅**: Suitable for this type of robot.
    - **❌**: Not suitable for this type of robot.

    This table offers a clear summary of controller suitability based on robot type and primary tasks, helping users make informed decisions about their controller configuration.
