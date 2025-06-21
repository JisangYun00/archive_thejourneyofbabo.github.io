---
title: F1Tenth 3D LiDAR SLAM
draft: false
tags:
  - F1Tenth
  - 3DLiDAR
aliases:
---
## 3D SLAM - F1Tenth Platform

After [[F1Tenth Build 3 (3D LiDAR - MID360)]] and [[3DLiDAR - Livox Mid-360 setup|Livox Mid-360 setup]], it's time for 3D SLAM! We tried several approaches, including [Kiss-icp](https://github.com/PRBonn/kiss-icp), and found that [Lidarslam_ros2](https://github.com/rsasaki0109/lidarslam_ros2) works quite well.

To set it up, simply change the `/velodyne_points` topic to `/livox/lidar` topic in `lidarslam.launch.py`:

```python
mapping = launch_ros.actions.Node(
    package='scanmatcher',
    executable='scanmatcher_node',
    parameters=[main_param_dir],
    remappings=[('/input_cloud','/livox/lidar'), # velodyne -> livox
                ('/imu', '/sensors/imu')],  # IMU Topic Remapping
)
```

Also, update some parameters in the `/param/lidarslam.yaml` file, such as scan_period, using_imu, and odom settings.

The result is shown below: ![[3D_SLAM.png]]