# URDF

```bash
$ sudo catkin_create_pkg mrobot_description urdf xacro # 创建一个新的功能包

# 检查梳理模型文件---------------------------------------------------
$ sudo apt-get install liburdfdom-tools # 
# check_urdf命令会解析URDF文件，并显示解析过程中的错误
$ check_urdf mrobot_chassis.urdf 
$ check_urdf <(xacro model.urdf.xacro)

# 查看urdf文件所描述的结构
$ urdf_to_graphiz [.urdf]
```

## 使用xacro优化URDF

+ xacro优势
  + 精简模型代码：xacro是一个精简版本的URDF文件，可以通过创建宏定义的方式定义常量或着复用代码
  + 提供可编程接口：xacro的语法支持一些可编程接口，如常量、变量、数学公式、条件语句等
+ 通过在一个xacro文件引用另一个xacro文件，例如把机器人本体写成一个xacro文件，在需要添加别的模块时，引用本体文件即可。这样可以使得模块集成时不用修改机器人的模型文件，只需要在上层实现一个拼装模块的顶层文件即可，灵活性更强

```bash
# 将xacro文件转换为URDF文件
$ rosrun xacro xacro mrobot.urdf.xacro > mrobot.urdf 

```

## 写好URDF后如何在rviz里加载进行验证

+ 参考http://www.autolabor.com.cn/book/ROSTutorials/di-6-zhang-ji-qi-ren-xi-tong-fang-zhen/62-fang-zhen-urdf-ji-cheng-rviz.html

+ 首先写一个view.launch文件

```xml
<launch>
    <arg name="model" />
    <!-- 加载机器人模型参数 此处为想可视化的URDF文件-->
    <param name="robot_description" command="$(find xacro)/xacro --inorder $(find realsense2_description)/urdf/test_d435_camera_with_iiwa.urdf.xacro" />

    <!-- 设置GUI参数，显示关节控制插件 -->
    <param name="use_gui" value="true"/>

    <!-- 运行joint_state_publisher节点，发布机器人的关节状态  -->
    
    <node name="joint_state_publisher_gui" pkg="joint_state_publisher_gui" type="joint_state_publisher_gui" />
    <!-- 运行robot_state_publisher节点，发布tf  -->
    <node name="robot_state_publisher" pkg="robot_state_publisher" type="robot_state_publisher"/>

    <!-- 运行rviz可视化界面 -->
    <node pkg="rviz" type="rviz" name="rviz" />
</launch>

```

+ 然后启动该launch文件，在rivz里add Robot Model，并将fixed frame改为base_link，此时可以正常显示

+ 再File-Save Config As保存该配置，退出rviz后将最后一行改为

  ```bash
  <node pkg="rviz" type="rviz" name="rviz" args="-d $(find d435_with_iiwa)/rviz/urdf.rviz"/>
  ```

+ 此时再重新launch，即可直接可视化

# Gazebo

+ Gazebo官方插件路径`/opt/ros/noetic/lib`，所有插件均以libgazeboXXX.so形式命名

```bash
#　进入ws_moveit文件夹
$ roslaunch mrobot_gazebo view_mrobot_with_kinect_gazebo.launch # Gazebo初始化小车场景
$ roslaunch mrobot_teleop mrobot_teleop.launch # 小车控制
$ rqt_image_view #　图像显示
$ rosrun rviz rviz
```

