---
title: ROS2 for Rust (rclrs) - System-wide Installation
draft: false
tags:
  - "#ros2"
  - "#rust"
  - "#rclrs"
aliases:
---
## [ROS2 for Rust (rclrs)](https://github.com/ros2-rust/ros2_rust)
**Write ROS2 applications in Rust**
## Basic Installation Method from GitHub

```bash
# Install Rust, e.g. as described in https://rustup.rs/
# Install ROS 2 as described in https://docs.ros.org/en/humble/Installation.html
# Assuming you installed the minimal version of ROS 2, you need these additional packages:
sudo apt install -y git libclang-dev python3-pip python3-vcstool # libclang-dev is required by bindgen

# Install these plugins for cargo and colcon:
pip install git+https://github.com/colcon/colcon-cargo.git
pip install git+https://github.com/colcon/colcon-ros-cargo.git

mkdir -p workspace/src && cd workspace
git clone https://github.com/ros2-rust/ros2_rust.git src/ros2_rust
vcs import src < src/ros2_rust/ros2_rust_humble.repos
source /opt/ros/humble/setup.bash
colcon build
```

## The Question: Should We Build This in Every Workspace?

**What if we could apply this system-wide?**  

Looking at the ROS installation:
```zsh
$ cd /opt
$ ls
    ros
```
The ROS system folder is here, so why don't we clone the 'ros2_rust' folder here as well?

## System-wide Installation Steps
### 1. Create the system directory
```zsh
cd /opt
sudo mkdir -p rust_ros2/src && cd rust_ros2
```

### 2. Clone the repository
```zsh
git clone https://github.com/ros2-rust/ros2_rust.git src/ros2_rust
```

If you encounter a permission error:
```
fatal: could not create work tree dir 'src/ros2_rust': Permission denied
```

### 3. Fix permissions
```zsh
sudo chown -R $USER:$USER .
```

### 4. Import dependencies and build
```zsh
vcs import src < src/ros2_rust/ros2_rust_humble.repos
colcon build --symlink-install
```

## Source System-wide

Edit your shell configuration file:
```zsh
vim ~/.bashrc  # for bash
# or
vim ~/.zshrc   # for zsh
```

Add these lines:
```zsh
source /opt/ros/humble/setup.zsh        # Original ROS2
source /opt/rust_ros2/install/setup.zsh # ROS2 Rust
```

## Benefits of System-wide Installation

- **No need to rebuild** for each workspace
- **Consistent environment** across all projects
- **Reduced disk usage** by avoiding duplicate builds
- **Easier maintenance** with a single installation point

## Adding Custom Message Types

If you want to use additional message types (like Ackermann messages), you can add them to the system-wide installation:
```zsh
cd /opt/rust_ros2/src/ros2_rust/common_interfaces
git clone https://github.com/ros-drivers/ackermann_msgs.git -b ros2
```

Then rebuild the system-wide installation:
```zsh
cd /opt/rust_ros2
colcon build --symlink-install
```

This will make the new message types available system-wide for all your ROS2 Rust projects.

## Usage

After completing the system-wide installation and sourcing the setup files, you can use ROS2 Rust in any workspace without additional setup steps. Simply create your Rust ROS2 packages and build them with `colcon build` as usual.