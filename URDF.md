# URDF

```bash
$ sudo catkin_create_pkg mrobot_description urdf xacro # 创建一个新的功能包

# 检查梳理模型文件---------------------------------------------------
$ sudo apt-get install liburdfdom-tools # 
# check_urdf命令会解析URDF文件，并显示解析过程中的错误
$ check_urdf mrobot_chassis.urd 
```

## 使用xacro优化URDF

+ xacro优势
  + 精简模型代码：xacro是一个精简版本的URDF文件，可以通过创建宏定义的方式定义常量或着复用代码
  + 提供可编程接口：xacro的语法支持一些可编程接口，如常量、变量、数学公式、条件语句等
+ 通过在一个xacro文件引用另一个xacro文件，例如把机器人本体写成一个xacro文件，在需要添加别的模块时，引用本体文件即可。这样可以使得模块集成时不用修改机器人的模型文件，只需要在上层实现一个拼装模块的顶层文件即可，灵活性更强

```bash
# 将xacro文件转换为URDF文件
$ rosrun xacro xacro.py mrobot.urdf.xacro > mrobot.urdf 
```

# Gazebo

+ Gazebo官方插件路径`/opt/ros/noetic/lib`，所有插件均以libgazeboXXX.so形式命名

```bash
#　进入ws_moveit文件夹
$ roslaunch mrobot_gazebo view_mrobot_with_kinect_gazebo.launch # Gazebo初始化小车场景
$ roslaunch mrobot_teleop mrobot_teleop.launch # 小车控制
$ rqt_image_view #　图像显示
$ rosrun rviz rviz 
```

