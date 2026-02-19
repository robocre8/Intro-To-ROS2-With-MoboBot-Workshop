# Intro-To-ROS2-With-MoboBot-Workshop
Introduction to ROS2 (Nav2) With MoboBot Workshop for the [**ROS Naija Abuja Meetup**]() March 2026.

---

## 🧰 Workshop Package: [MoboBot](https://github.com/robocre8/mobo_bot)

Give the package a ⭐ and learn more about ROS and robotics by [Robocre8](https://github.com/robocre8).

---

### MoboBot Gazebo Simulation

> 📝 **Note:**
> - Your Dev PC must be running **Ubuntu 24.04**, **ros-jazzy-desktop**, and **Gazebo Harmonic**.
> - You can also follow with Windows 11 and WSL with Ubuntu24.04 LTS
> - If you followed the installation guide, you should not worry about this info
> - just follow the instructions below by just copying and pasting. There's no need to worry much.

---

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

---

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

---

### 🔭 View Robot and TF Tree

- **Robot State Publisher, Rviz Visualization, and TF tree View:**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup tf_view.launch.py \
  use_hardware:=false
  ```

---

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

