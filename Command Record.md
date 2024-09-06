# Command Record

## conda

```bash
$ source ~/anaconda3/bin/activate # 激活conda环境
$ conda deactivate # 退出conda环境
```



## rosdep

+ #### Install dependency of all packages in the workspace

    ```bash
    # Go to the top directory of your catkin workspace where the source code of the ROS packages you'd like to use are. Then run:
    rosdep install --from-paths src --ignore-src -r -y
    ```

+ Command  ‘rosdep’ not found 问题详见Problem_Record.md

## 小乌龟

```bash
$ rosrun turtlesim turtlesim_node # 可视化界面
$ rosrun turtlesim turtle_teleop_key # 键盘控制
$ rqt_graph # 计算图可视化工具
#----------------------------------------------------------
$ roslaunch turtle_tf turtle_tf_demo.launch # 轨迹跟踪
$ rosrun rviz rviz -d `rospack find turtle_tf`/rviz/turtle_rviz.rviz # 坐标关系可视化
$ rosrun tf2_tools view_frames.py # 查看例程中的TF树
$ rosrun tf tf_echo turtle1 turtle2 # 查找两乌龟间的坐标变换关系

```



## 常用命令

```bash
$ env | grep ros # 查看所有ROS相关的环境变量
$ echo $ROS_PACKAGE_PATH
$ rosmsg show <msg_name> # 显示某种消息的路径和内容
$ rostopic list
$ rosservice list
$ rostopic type /joint_states | rosmsg show # 显示某话题下的消息格式


# 初始化工作区--------------------------------------------------------------------------------
$ mkdir -p ./catkin_ws/src && cd ~/catkin_ws/src
$ catkin_init_workspace 
$ cd ~/catkin_ws
$ catkin_make # 如果想重新编译，直接删除build与devel文件夹即可

# 创建功能包---------------------------------------------------------------------------------
$ catkin_create_pkg <package_name> [depend1] [depend2] [depend3] 
# 基础depend： std_msgs rospy roscpp
# 同一个工作空间内，不能存在同名功能包
# 不同工作空间存在同名功能包的情况由Overlaying机制处理，见《ROS机器人开发实践》3.3.1
$ rospack find <package_name> # 查找某功能包当前的定位
```

## rostopic

```bash
$ rosmsg show <msg_name> # 显示某种消息的路径和内容
$ rostopic list
$ rostopic type /joint_states | rosmsg show # 显示某话题下的消息格式
```

+ /joint_states

```bash
$ rostopic type /joint_states
sensor_msgs/JointState

$ rosmsg show sensor_msgs/JointState
std_msgs/Header header
  uint32 seq
  time stamp
  string frame_id
string[] name
float64[] position
float64[] velocity
float64[] effort

$ rostopic echo /joint_states  
header: 
  seq: 45596
  stamp: 
    secs: 1210
    nsecs: 815000000
  frame_id: ''
name: 
  - finger_joint
  - joint_a1
  - joint_a2
  - joint_a3
  - joint_a4
  - joint_a5
  - joint_a6
  - joint_a7
  - left_inner_finger_joint
  - left_inner_knuckle_joint
  - right_finger_joint
  - right_inner_finger_joint
  - right_inner_knuckle_joint
  
position: [0.6900001966600602, 
		   1.9500410175510297e-08, 3.696459938140606e-08, 2.063347892544698e-08, -1.9547627516658395e-08, -2.1982348386018202e-08, 2.5298274319851544e-07, 2.9243891752628315e-08, # 关节状态
		   0.6900001966600602, -0.6900001966600593, -0.6900001966600595, 0.6900001966600602, -0.6900001966600595]
		   
velocity: [-2.173883418805282e-10, -7.7265193473613e-08, -2.921140189980606e-09, 1.1672425784200201e-07, -5.6635565304388945e-09, -1.5486689001742689e-07, -3.765326505016794e-09, 5.226544631921374e-08, 7.370965911438688e-07, -1.8536486889308739e-06, -1.1027862216644465e-06, 1.2505064133334275e-06, 1.5953097462507232e-07]

effort: [-0.02260213185272759, -2.403603655384751e-06, -0.0845135914367273, 2.6374171605018644e-06, 0.08085267606338954, -2.7787027686958347e-06, -0.08085020481994906, -2.098980706499281e-06, 0.0, 0.0, 0.0, 0.0, 0.0]

```

