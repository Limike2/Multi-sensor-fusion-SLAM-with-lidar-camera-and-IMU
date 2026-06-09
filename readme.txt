（1）代码结构：
Multi_camera/
├── src/
│   ├── .vscode/
│   ├── c30d_driver/
│   │   └── behavior_trees/
│   │       └── simple_navigate.xml
│   ├── config/
│   │   ├── cartographer_2d.lua
│   │   ├── ekf.yaml
│   │   └── nav2_params.yaml
│   ├── launch/
│   │   ├── cartographer_fusion.launch.py
│   │   ├── nav_sensors.launch.py
│   │   └── navigation.launch.py
│   ├── maps/
│   └── src/
│       ├── c30d_driver_node.cpp
│       └── scan_merger_node.py
├── CMakeLists.txt
├── package.xml
├── cartographer
├── LSLIDAR_ROS2
├── navigation2-humble
└── serial

（2）改进部分
深度相机激光与原激光的融合在scan_merge.cpp
c30d_driver_node.cpp为底盘与上位机通信驱动
Navigation2中的A*算法代码文件位于nav2_smac_planner/src/a_star.cpp的325行

（3）运行命令
cd ~/Multi_camera
colcon build --packages-select c30d_driver
source install/setup.bash
#激光雷达为ttyACM0，底盘为ttyACM1，给串口权限
sudo chmod -R 777 /dev/ttyACM0
sudo chmod -R 777 /dev/ttyACM1
#运行融合建图launch文件
ros2 launch c30d_driver cartographer_fusion.launch.py
#导航launch文件
ros2 launch c30d_driver nav_sensors.launch.py
ros2 launch c30d_driver navigation.launch.py