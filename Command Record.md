# Command Record

## rosdep

+ #### Install dependency of all packages in the workspace

    ```bash
    # Go to the top directory of your catkin workspace where the source code of the ROS packages you'd like to use are. Then run:
    rosdep install --from-paths src --ignore-src -r -y
    ```

+ Command  ‘rosdep’ not found 问题详见Problem_Record.md

## 