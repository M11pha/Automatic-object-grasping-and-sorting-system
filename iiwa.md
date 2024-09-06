# iiwa机械臂

## 机械臂

```bash
# package ws_moveit - test_kuka
$ roslaunch test_kuka demo_gazebo.launch
```



## 机械臂 with 夹爪

```bash
# package ws_moveit - iiwa_with_gripper
$ roslaunch iiwa_with_gripper demo_gazebo.launch
```



## ArbotiX控制机械臂

```bash
# ~/ros_workspace/ws_moveit
$ roslaunch d435_with_gripper fake_arm_and_gripper_ekko.launch

# ~/ros_workspace/ws_moveit/src/d435_with_gripper/scripts
$ python3 trajectory_demo.py _reset:=false

# 目前还办法控制夹爪
```



## 命令行控制机械臂

### 思路

```bash
# 首先得找到在哪个话题里发布topic----------------------------------------------------------------------------
$ rostopic list

/arm_controller/command     # 这是通过命令行控制机械臂的话题
/gripper_controller/command # 这是通过命令行控制夹爪的话题

# 然后查询该topic的信息------------------------------------------------------------------------------------
$ rostopic info [topic] # 用info命令，会查询到该话题的消息类型，发布者，订阅者
Type: trajectory_msgs/JointTrajectory
Publishers: None
Subscribers: 
 * /gazebo (http://rog-z:34755/)

$ rostopic type [topic] # 用type命令，会查询到该话题的消息类型
trajectory_msgs/JointTrajectory

$ rostopic type [topic] | rosmsg show # 将type结果给show，可以打印该消息的格式
std_msgs/Header header
  uint32 seq
  time stamp
  string frame_id
string[] joint_names
trajectory_msgs/JointTrajectoryPoint[] points
  float64[] positions
  float64[] velocities
  float64[] accelerations
  float64[] effort
  duration time_from_start

```



### 控制夹爪

```bash
$ rostopic pub /gripper_controller/command trajectory_msgs/JointTrajectory "{
  joint_names: ['finger_joint'], 
  points: [{positions: [0.0], time_from_start: {secs: 1, nsecs: 0}}]
}"
 # positions为0时为打开的极限弧度，0.7为闭合的极限弧度
```

+ `joint_names`：这个字段应该填写你要控制的夹爪关节名称，例如`finger_joint`。具体的关节名称可以参考你机械臂和夹爪的URDF文件。
+ `positions`：这里设置为`0.0`表示完全闭合。
+ `time_from_start`：执行该动作的时间，可以设置为1秒（`secs: 1`）。

### 控制机械臂

```bash
$ rostopic pub /arm_controller/command trajectory_msgs/JointTrajectory "{
  joint_names: ['joint_a1', 'joint_a2', 'joint_a3', 'joint_a4', 'joint_a5', 'joint_a6', 'joint_a7'],
  points: [{
    positions: [-1.412, -0.845, 0.003, 0.819, 0.001, -1.563, -0.002],
    time_from_start: {secs: 7, nsecs: 0}
  }]
}"

$ rostopic pub /arm_controller/command trajectory_msgs/JointTrajectory "{
  joint_names: ['joint_a1', 'joint_a2', 'joint_a3', 'joint_a4', 'joint_a5', 'joint_a6', 'joint_a7'],
  points: [{
    positions: [0, 0, 0, 0, 0, 0, 0],
    time_from_start: {secs: 7, nsecs: 0}
  }]
}"
```

