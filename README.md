# 环境准备
安装ROS 2 humble

初始化rosdep
```
sudo rosdep init
rosdep update
```

安装依赖项
```
rosdep install --from-paths src --ignore-src -r -y
```

# 编译工程

编译工作空间

```
colcon build --symlink-install
```

编译成功后，源入工作空间的setup文件
```
source install/setup.bash
```

# 运行节点
机器人节点
```
ros2 run ros_robot_controller ros_robot_controller
```

IMU互补滤波节点
```bash
ros2 run imu_complementary_filter complementary_filter_node
```

若需要启用磁力计数据：
```bash
ros2 run imu_complementary_filter complementary_filter_node --ros-args -p use_mag:=True
```

验证节点通信
使用ros2 topic list查看当前的主题列表，确认各节点之间的通信正常。
```bash
ros2 topic list
```

使用ros2 topic echo查看特定主题的数据：

```bash
ros2 topic echo /imu/data
```

# 调试与监控
使用rqt工具进行可视化监控

```bash
ros2 run rqt_gui rqt_gui
```

检查节点状态

```bash
ros2 node list
ros2 node info /ros_robot_controller
ros2 node info /complementary_filter_node
```

记录和回放数据

```bash
ros2 bag record /imu/data /imu/data_raw
```
```bash
ros2 bag play <bag_file_name>
```