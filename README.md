# Intro-To-ROS2-With-MoboBot-Workshop
Introduction to ROS2 (Nav2) With MoboBot Workshop for the [**ROS Naija Abuja Meetup**]() March 2026.

<br/>

---
<br/>

## 📁 PC SETUP

> 📝 **Note:**
> - You would be setting up **Ubuntu 24.04**, **ros-jazzy-desktop**, and **Gazebo Harmonic**.
> - You can also follow with Windows 11 and WSL with Ubuntu24.04 LTS
> - Those who use Ubuntu 22.04 and  ros-humble can also follow along

<br/>

### 1. System Setup and Configuration (Ubuntu 24.04 LTS)

#### Option 1: Dual Boot (Highly Recommended | If you can)

- Watch Tutorial: [YouTube Tutorial](https://www.youtube.com/watch?v=alFosqQ1ang&list=PLhfTXXGugELOo21NOv8D4uJm59JaWpYIS&index=31&pp=iAQBsAgC)

#### Option 2: Using WSL (Recommended Alternative for Windows 11 Users)
- Open PowerShell from windows start menu and run the following command to install WSL
  ```shell
  wsl --install
  ```
- Follow this [**Tutorial**](https://www.youtube.com/watch?v=Cn1DYQwGY8o) to Install ubuntu 24.04 on WSL

#### Option 3: Virtual Machine Installation

- Watch Tutorial: [YouTube Tutorial](https://www.youtube.com/watch?v=kSy3NX3Pe-c&list=PLNWNEEf8BvG6z60R4r9_wQ6Ekmqj-BmFr&index=1)

#### Option 4: ros2env -> DevContainer with VSCode + Docker

- Visual Studio Code: [Install VSCode](https://code.visualstudio.com/)
- Docker Desktop: [Install Docker](https://www.docker.com/products/docker-desktop/)
- Follow this repo: [ROS2env](https://github.com/SakshayMahna/ros2env)
- Watch this video  [ROS2env](https://youtu.be/mt8DTLkWNyA)
- In VSCode: Click `Reopen in Container`

> The `.devcontainer` folder is pre-configured with ROS2 Jazzy and tools.

<br/>

### 2. ROS2 Jazzy Installation

- **Robocre8 Tutorial (Recommended):** [How To Install ROS2 Jazzy Desktop On PC (FULL INSTALL)](https://robocre8.gitbook.io/robocre8/tutorials/how-to-install-ros2-jazzy-desktop-on-pc-full-install)
- **Official ROS Documentation:** [ROS 2 Jazzy (Ubuntu Noble 24.04)](https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html)
- **Post-Installation Check:**

  ```bash
  echo $ROS_DISTRO
  ```

<br/>

---
<br/>

## 🧰 Workshop Package: [MoboBot](https://github.com/robocre8/mobo_bot)

Give the package a ⭐ and learn more about ROS and robotics by [Robocre8](https://github.com/robocre8).

<br/>

---
<br/>

### MoboBot Gazebo Simulation

> 📝 **Note:**
> - Your Dev PC must be running **Ubuntu 24.04**, **ros-jazzy-desktop**, and **Gazebo Harmonic**.
> - If you followed the installation guide, you should not worry about this info
> - just follow the instructions below by just copying and pasting. There's no need to worry much.

<br/>

---
<br/>

### 🔧 Prerequisites

- **Cyclone DDS Setup:**
  > **NOTE**: if you follow the installation guide, you'd have installed this. You can skip this step.
  ```shell
  sudo apt install ros-jazzy-rmw-cyclonedds-cpp
  ```
  ```shell
  export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp
  ```
  ```shell
  echo "export RMW_IMPLEMENTATION=rmw_cyclonedds_cpp" >> ~/.bashrc
  ```

<br/>

---
<br/>

### 📦 Clone and Build MoboBot
  
- **Create Workspace:**
  ```shell
  mkdir -p ~/mobo_bot_ws/src && cd ~/mobo_bot_ws && colcon build
  ```
  ```shell
  source ~/mobo_bot_ws/install/setup.bash
  ```

- **Clone Arrow Key Teleop Package:**
  ```shell
  sudo apt install python3-pip -y && sudo apt install python3-pynput -y
  ```
  ```shell
  cd ~/mobo_bot_ws/src && git clone https://github.com/samuko-things/arrow_key_teleop_drive.git
  ```
  Learn more about the [**arrow_key_teleop_drive**](https://github.com/samuko-things/arrow_key_teleop_drive)
  

- **Clone MoboBot Packages:** 
  ```shell
  cd ~/mobo_bot_ws/src && git clone -b jazzy https://github.com/robocre8/mobo_bot.git
  ```

- **Ignore Hardware (optional):**
  ```shell
  cd ~/mobo_bot_ws/src/mobo_bot/mobo_bot_base && touch COLCON_IGNORE
  ```

- **Install Dependencies:**
  ```shell
  cd ~/mobo_bot_ws && rosdep update && rosdep install --from-paths src --ignore-src -r -y
  ```

- **Build Packages:**
  ```shell
  cd ~/mobo_bot_ws && colcon build --symlink-install
  ```
  
- **Export MOBOBOT_BASE_TYPE env variable**

  ```shell
  export MOBOBOT_BASE_TYPE=2WD
  ```
  ```shell
  echo "export MOBOBOT_BASE_TYPE=2WD" >> ~/.bashrc
  ```

<br/>

---
<br/>

### 🔭 View Robot and TF Tree

- **Robot State Publisher, Rviz Visualization, and TF tree View:**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup tf_view.launch.py \
  use_hardware:=false
  ```

<br/>

---
<br/>

### 🎮 Run MoboBot Simulation
> **NOTE**: run in different terminals.

- **Start Simulation:**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup sim.launch.py
  ```

- **Control with Keyboard:**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 run arrow_key_teleop_drive arrow_key_teleop_drive 0.15 0.7 true
  ```
  >NOTE: you would need to click into the rviz or simulation for the 
  > arrow_key_teleop drive to start woking. because it uses pynput
  >
  >NOTE: also feel free to use any other **teleop package** you want 
  
#
---

