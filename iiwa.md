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

