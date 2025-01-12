Why I Chose ZED 2i
===================

The **ZED 2i** camera was an ideal choice for this task due to its built-in **body tracking feature**. In dynamic environments like retail stores, where humans are continuously moving, it is critical to track human bodies effectively. The ZED 2i’s advanced capabilities, such as tracking 18 key points of the human body, enable precise and reliable tracking.

> Refer to the `ZED 2i Body Tracking Documentation <https://www.stereolabs.com/docs/body-tracking/>`_ for more details.

Here’s a visual representation of the 18 key points tracked by the ZED 2i camera:  

.. image:: https://docs.stereolabs.com/body-tracking/images/keypoints_body18.png
   :alt: Body Tracking Key Points
   :width: 70%
   :align: center

Below is a **GIF of a scene showcasing keypoints being detected in real-time** using the ZED 2i camera:  

.. figure:: media/gifs/bodytracking.webp
   :alt: Keypoints Detection GIF
   :width: 70%
   :align: center

The GIF illustrates how the ZED 2i camera accurately tracks and detects human movements by identifying body keypoints, ensuring seamless performance in dynamic environments like retail stores.

Another compelling reason for experimenting with the ZED 2i camera is its **availability within Isaac Sim**. NVIDIA Isaac Sim supports the ZED 2i camera as a virtual sensor, allowing developers to test and validate robotics applications in high-fidelity simulated environments before deploying them in real-world scenarios.

.. figure:: https://docs.stereolabs.com/isaac-sim/images/ZED_in_isaac_sim.jpg
   :alt: ZED2i in Isaac Sim
   :width: 70%
   :align: center

`ZED2i Documentation <https://www.stereolabs.com/docs/isaac-sim>`_

.. note::
   For more information, visit the `Isaac Sim ZED 2i Documentation <https://www.stereolabs.com/docs/isaac-sim>`_.

Outcome and Applications
========================

The combination of the ZED 2i camera and YOLOv8 allowed the robot to:

1. **Classify Objects with High Accuracy:** For example, identifying handbags, as shown in the GIF.  
2. **Track Human Movements:** The built-in body tracking feature ensured accurate tracking of humans, which is crucial in environments like retail stores.  
3. **Process Augmented Data:** Using RoboFlow for data preprocessing and augmentation streamlined the training process and improved detection accuracy.

These insights and tools lay a strong foundation for creating robust object detection systems, especially in settings where robots need to navigate and interact with complex environments efficiently.
