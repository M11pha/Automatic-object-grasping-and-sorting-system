# Automatic-object-grasping-and-sorting-system

+ 工作区记录
    + camera 安装Intel® RealSense™ ROS
    + d435文件夹 测试相机
        + `roslaunch realsense2_description view_d435_model_rviz_gazebo.launch`
    + kuka_robots文件夹 测试机械臂
      
        ```bash
        sudo apt-get install ros-noetic-joint-trajectory-controller
        sudo apt-get install ros-noetic-moveit*
        sudo apt-get install ros-noetic-ros-control ros-noetic-ros-controllers ros-noetic-gazebo-ros ros-noetic-gazebo-ros-control ros-noetic-hector-gazebo-plugins 
        ```
        
        + roslaunch test_iiwa demo_gazebo.launch