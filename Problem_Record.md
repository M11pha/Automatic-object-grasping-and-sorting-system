# Problem Record

##  工程问题

### CV

+ 小车抖动
+ 相机未设定惯性
+ 左右轮子对调
+ `ERROR] [1723731587.809724926]: SpawnModel: Failure - model name robot already exist.`https://answers.ros.org/question/271978/error-while-launching-robot-model/
  + 机器人加载问题，原因是删除了相机的inertial标签


## Moveit

+ 系统中安装moveit后，在工作区重新编译了别的版本的moveit，二者的冲突问题
    + 根据https://answers.ros.org/question/379810/how-to-correctly-configure-moveit-for-each-workspace/，本工作区的moveit版本在`source devel/setup.bash`后，会优先于其他地方的版本

### Command  ‘rosdep’ not found

+ 先使用`sudo apt install python3-rosdep2`安装rosdep，再`rosdep init`

    ```bash
    rosdep install --from-paths src --ignore-src -r -y
    ```

    

+ 但是该安装会卸载noetic packages，根据https://github.com/ros-infrastructure/rosdep/issues/763，再卸载rosdep，安装noetic

    ```bash
    sudo apt-get remove python3-rosdep2
    sudo apt-get install ros-noetic-desktop-full
    ```

    

### 为了解决以下问题注释掉了d435_with_gripper/config/gazebo_realsense2_camera.urdf 里的650行

```bash
[ERROR] [1725787452.111980346]: Tried to advertise a service that is already advertised in this node [/controller_manager/list_controllers]
[ERROR] [1725787452.112026377]: Tried to advertise a service that is already advertised in this node [/controller_manager/list_controller_types]
[ERROR] [1725787452.112044299]: Tried to advertise a service that is already advertised in this node [/controller_manager/load_controller]
[ERROR] [1725787452.112062065]: Tried to advertise a service that is already advertised in this node [/controller_manager/unload_controller]
[ERROR] [1725787452.112079687]: Tried to advertise a service that is already advertised in this node [/controller_manager/switch_controller]
[ERROR] [1725787452.112099673]: Tried to advertise a service that is already advertised in this node [/controller_manager/reload_controller_libraries]

<!--
    <gazebo>
        <plugin filename="libgazebo_ros_control.so" name="ros_control" />
    </gazebo>
-->
```

+ 参考https://blog.csdn.net/weixin_48319333/article/details/129200789
+ 
