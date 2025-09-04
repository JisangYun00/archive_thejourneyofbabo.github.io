---
title: AutoDRIVE RoboRacer Setup Guide
draft: false
tags:
  - F1Tenth
aliases:
  - autodrive install
---
>**Complete setup guide for the AutoDRIVE RoboRacer simulation environment. [[F1Tenth]] sim racing**

## Overview
The AutoDRIVE ecosystem consists of two main components:
- **Simulator**: Unity-based racing simulator
- **Devkit**: ROS 2 API for autonomous driving algorithm development
## Prerequisites
- **Supported Python Versions**: 3.8, 3.9, 3.10
- **ROS 2** workspace setup
- **Ubuntu/Linux** environment recommended

## Installation
### Step 1: Download Components
Visit the [ROBORACER ICRA 2025 webpage](https://autodrive-ecosystem.github.io/competitions/roboracer-sim-racing-icra-2025/#resources) and download:
1. **AutoDRIVE Simulator**
2. **AutoDRIVE Devkit**

_Note: Local installation recommended if Docker setup encounters issues_
![[autodrive-f1tenth.png|700]]

### Step 2: Setup Simulator
1. **Extract and prepare simulator files:**
    
    ```bash
    # Navigate to simulator directory
    cd ~/Programming/autodrive_ws/sim_autodrive
    
    # Make executable
    sudo chmod +x AutoDRIVE\ Simulator.x86_64
    ```
    
2. **Expected directory structure:**
    
    ```
    sim_autodrive/
    ├── AutoDRIVE Simulator.x86_64
    ├── Data/
    ├── GameAssembly.so
    ├── UnityPlayer.so
    └── nohup.out
    ```
    

### Step 3: Setup Devkit

1. **Place devkit in ROS 2 workspace:**
    
    ```bash
    # Copy autodrive_devkit to your ROS 2 source directory
    cp -r autodrive_devkit ~/ros2_ws/src/
    cd ~/ros2_ws/src/autodrive_devkit
    
    # Make Python scripts executable
    sudo chmod +x *.py
    ```
    
2. **Install dependencies:**
    
    ```bash
    # Check your Python version
    python3 --version
    
    # Install appropriate requirements
    pip3 install -r requirements_python_3.8.txt   # For Python 3.8
    pip3 install -r requirements_python_3.9.txt   # For Python 3.9
    pip3 install -r requirements_python_3.10.txt  # For Python 3.10
    
    # Additional requirements
    
    # Fix setuptools compatibility 
	pip3 install 'setuptools<66.0.0' 
	
	# Install Python dependencies 
	pip3 install transforms3d attrdict 
	
	# Install ROS2 dependencies
	sudo apt update
	
	sudo apt install ros-humble-cv-bridge
	sudo apt install ros-humble-tf-transformations
	sudo apt install ros-humble-rviz-imu-plugin
    ```
    
3. **Build ROS 2 workspace:**
    
    ```bash
    cd ~/ros2_ws
    colcon build
    source install/setup.bash
    ```

## Usage

### 1. Launch Simulator

```bash
# Navigate to simulator directory
cd ~/Programming/autodrive_ws/sim_autodrive

# Run simulator
./AutoDRIVE\ Simulator.x86_64
```

### 2. Launch Devkit

```bash
# Source ROS 2 workspace
source ~/ros2_ws/install/setup.bash

# Launch with graphics (recommended for visualization)
ros2 launch autodrive_roboracer bringup_graphics.launch.py

# Alternative: Launch headless mode
ros2 launch autodrive_roboracer bringup_headless.launch.py
```

### 3. Connect Components

1. **Start the simulator** (Step 1)
2. **Launch devkit** (Step 2)
3. **Click "Connect" button** in the simulator interface
4. **RViz visualization** should appear showing the racing environment

### 4. Vehicle Control

```bash
# Manual keyboard control
ros2 run autodrive_roboracer teleop_keyboard
```

## Architecture

```
┌─────────────────┐    WebSocket     ┌─────────────────┐
│   AutoDRIVE     │◄────────────────►│   AutoDRIVE     │
│   Simulator     │    Bridge        │   Devkit        │
│   (Unity)       │                  │   (ROS 2)       │
└─────────────────┘                  └─────────────────┘
                                             │
                                             ▼
                                     ┌─────────────────┐
                                     │   Algorithm     │
                                     │  Development    │
                                     │ (Python/C++)    │
                                     └─────────────────┘
```

## Troubleshooting

- **Docker issues**: Use local installation as described above
- **Connection problems**: Ensure both simulator and devkit are running before connecting
- **Python version conflicts**: Use virtual environments and match exact dependency versions
- **Permission errors**: Ensure executable permissions are set correctly

## Competition Resources

- **Official webpage**: [ROBORACER ICRA 2025](https://autodrive-ecosystem.github.io/competitions/roboracer-sim-racing-icra-2025/#resources)
- **Documentation**: Check README files in downloaded packages
- **Support**: Refer to official AutoDRIVE ecosystem documentation

## Next Steps

1. **Verify setup** by launching both components and establishing connection
2. **Test teleoperation** to ensure vehicle control works
3. **Explore RViz** visualization for sensor data and environment mapping
4. **Begin algorithm development** using the ROS 2 API


**Simulator looks like**  

![[autodrive_sim.png|700]]

**rviz diplay after connected**  

![[autodrive_dev_rviz.png|700]]



---
### Reference
[ROBORACER ICRA 2025 webpage](https://autodrive-ecosystem.github.io/competitions/roboracer-sim-racing-icra-2025/#resources)

check IP Address
`hostname -I`

**Clone repository (if needed):**
```bash
git clone https://github.com/AutoDRIVE-Ecosystem/AutoDRIVE-RoboRacer-Sim-Racing.git
```

## Key Dependencies

### WebSocket Communication (Version Critical)

|Package|Version|
|---|---|
|eventlet|0.33.3|
|Flask|1.1.1|
|Flask-SocketIO|4.1.0|
|python-socketio|4.2.0|
|python-engineio|3.13.0|

### Data Processing Libraries

|Package|Minimum Version|
|---|---|
|numpy|1.13.3|
|opencv-contrib-python|4.5.1.48|
|pillow|5.1.0|
