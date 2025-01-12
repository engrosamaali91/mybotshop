Exploring Object Detection with ZED 2i Camera
=============================================

Depth cameras are a crucial component of any robot. Acting as the robot's eyes, they enable the robot to not only see objects but also infer their distance from the camera. Unlike standard fisheye cameras, depth cameras like the ZED 2i allow robots to estimate the 3D pose of objects relative to the camera, which is vital for tasks such as navigation and object interaction.

Why Depth Cameras Matter
------------------------

In scenarios where a robot relies heavily on its depth camera:

- **Object Localization:** Depth cameras help estimate the location of objects in the environment while the robot is moving.  
- **Human-Robot Interaction:** They enable robots to classify objects and humans, improving situational awareness in dynamic environments like retail stores.  
- **Pose Estimation:** The 3D pose of objects can be calculated, helping robots identify the orientation and position of objects.  

As shown in the **GIF below**, the robot classified a handbag with approximately 84% accuracy, demonstrating the capability to detect and classify objects. This was achieved using a trained YOLOv8 model, with data preprocessing and augmentation performed using **RoboFlow**.

.. figure:: media/gifs/Object_detection_wrt_camera_frame.webp                                                               
   :width: 100%                                                                                                                         
   :align: center

   *3d Object pose detection*
                                
Why I Chose YOLOv8
------------------

I selected the YOLOv8 model for this task because of its flexibility and support for multiple tasks such as detection, classification, and segmentation. Below is a comparison of its key features, which influenced my decision:

.. list-table:: YOLOv8 Comparison
   :header-rows: 1
   :widths: 25 25 25 25

   * - **Feature**
     - **YOLOv8**
     - **YOLOv5**
     - **YOLOv4**
   * - **Architecture**
     - Unified Detection, Segmentation, Classification
     - Separate models
     - Separate models
   * - **Speed**
     - Faster than YOLOv5
     - Moderate
     - Slower
   * - **Accuracy**
     - Improved
     - High
     - Moderate
   * - **Supported Modes**
     - Detection, Classification, Segmentation
     - Detection, Classification
     - Detection only
   * - **Ease of Use**
     - Intuitive
     - Intuitive
     - Moderate

For more details, refer to the `YOLOv8 documentation <https://docs.ultralytics.com/models/yolov8/>`_.

Additionally, the comparison image below illustrates YOLOv8’s performance metrics relative to previous versions, highlighting its superior speed and accuracy.  

.. image:: https://github.com/ultralytics/docs/releases/download/0/yolov8-comparison-plots.avif
   :alt: YOLOv8 Comparison
   :target: https://docs.ultralytics.com/models/yolov8/

`YOLOv8 Documentation <https://docs.ultralytics.com/models/yolov8/>`_

.. note::
    These attributes make YOLOv8 a clear choice for real-time robotics applications where detection and classification tasks demand both accuracy and efficiency.
