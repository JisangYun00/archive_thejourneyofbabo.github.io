---
title: 3DLiDAR - Livox Mid-360 setup
draft: false
tags:
  - LiDAR
  - 3DLiDAR
aliases:
---
## [Livox Mid-360 3D LiDAR](https://www.livoxtech.com/mid-360)
![[mid360-3d-lidar.png|500]]
## How to setup?
1. From the [User-Manual](https://terra-1-g.djicdn.com/851d20f7b9f64838a34cd02351370894/Livox/Livox_Mid-360_User_Manual_EN.pdf) page10 connection part, setup the Network.
	`static IP address of the computer` to **192.168.1.50** // Netmask as **255.255.255.0**
	
    ![[livox_network_setup.png|450]]

2. Follow the instruction at the [livox_ros_driver-github](https://github.com/Livox-SDK/livox_ros_driver2). 
	```
	git clone https://github.com/Livox-SDK/livox_ros_driver2.git ws_livox/src/livox_ros_driver2
	```
- Check the Serial Number. And last two digit used for the LiDAR ip address.   
  For example `192.168.1.1xx -> 192.168.1.158`

	![[livox-mid360-code.jpg|300]]
- Update IP address inside the config file(MID360_config.json)
	```
	~/ws_livox/src/livox_ros_driver2/config (master*) » vim MID360_config.json
	```
	
	```
	{
	  "lidar_summary_info" : {
	    "lidar_type": 8
	  },
	  "MID360": {
	    "lidar_net_info" : {
	      "cmd_data_port": 56100,
	      "push_msg_port": 56200,
	      "point_data_port": 56300,
	      "imu_data_port": 56400,
	      "log_data_port": 56500
	    },
	    "host_net_info" : { ## update here
	      "cmd_data_ip" : "192.168.1.50", #
	      "cmd_data_port": 56101,
	      "push_msg_ip": "192.168.1.50", #
	      "push_msg_port": 56201,
	      "point_data_ip": "192.168.1.50", #
	      "point_data_port": 56301,
	      "imu_data_ip" : "192.168.1.50", #
	      "imu_data_port": 56401,
	      "log_data_ip" : "",
	      "log_data_port": 56501
	    }
	  },
	  "lidar_configs" : [
	    {
	      "ip" : "192.168.1.158", # also update here
	      "pcl_data_type" : 1,
	      "pattern_mode" : 0,
	      "extrinsic_parameter" : {
	        "roll": 0.0,
	        "pitch": 0.0,
	        "yaw": 0.0,
	        "x": 0,
	        "y": 0,
	        "z": 0
	      }
	    }
	  ]
	}
	```
- Build file
	```
	~/ws_livox/src/livox_ros_driver2 (master*) » ./build.sh humble      
	```
- Launch with rviz2
	```
	~/ws_livox » source install/setup.zsh
	```
	```
	~/ws_livox » ros2 launch livox_ros_driver2 rviz_MID360_launch.py
	```
## Result
![[mid360-rviz-img.png]]

> [!note] Common Errors
>  - [Livox-SDK2](https://github.com/Livox-SDK/Livox-SDK2/tree/master) Need to setup SDK
>  - When point clouds not showing after all setup, checkout firewall setting for the ports

 > [!tip]
> - You can also change point clouds publish-frequency(publish_freq = 10.0 / 20.0 / 50.0 ...)

---
## Reference
- [livox_ros_driver2_github](https://github.com/Livox-SDK/livox_ros_driver2)
- [livox_mid-360_user_manual_en](https://terra-1-g.djicdn.com/851d20f7b9f64838a34cd02351370894/Livox/Livox_Mid-360_User_Manual_EN.pdf)