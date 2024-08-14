# Command Record

## rosdep

+ #### Install dependency of all packages in the workspace

    ```bash
    # Go to the top directory of your catkin workspace where the source code of the ROS packages you'd like to use are. Then run:
    rosdep install --from-paths src --ignore-src -r -y
    ```

+ Command  ‘rosdep’ not found 问题详见Problem_Record.md

## 小乌龟

```bash
$ rosrun turtelsim turtlesim_node # 可视化界面
$ rosrun turtlesim turtle_teleop_key # 键盘控制
```



## 常用命令

```bash
$ env | grep ros # 查看所有ROS相关的环境变量
$ echo $ROS_PACKAGE_PATH
$ rosmsg show <msg_name> # 显示某种消息的路径和内容


# 初始化工作区--------------------------------------------------------------------------------
$ mkdir -p ~/catkin_ws/src
$ cd ~/catkin_ws/src
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

