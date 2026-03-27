### 🎮 Run MoboBot Hardware
- **Start MoboBot Hardware (Raspberry Pi):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup robot.launch.py #use_camera:=true
  ```
- **View MoboBot in RVIZ (Dev PC):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_rviz robot.launch.py
  ```

- **Control with Keyboard (Dev PC):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 run arrow_key_teleop_drive arrow_key_teleop_drive 0.15 0.7 true
  ```
  >NOTE: you would need to click into the rviz or simulation for the 
  > arrow_key_teleop drive to start woking. because it uses pynput
  >
  >NOTE: also feel free to use any other **teleop package** you want 
  
<br/>

---
<br/>

### 🎮 MoboBot 2D Mapping with SLAM (Hardware)
> **NOTE**: run in different terminals.

- **Start Mapping with MoboBot (Raspberry Pi):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup robot_mapping.launch.py #use_nav:=True
  ```

- **View MoboBot in RVIZ (Dev PC):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_rviz mapping_and_navigation.launch.py
  ```

- **Control with Keyboard (Dev PC):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 run arrow_key_teleop_drive arrow_key_teleop_drive 0.15 0.7 true
  ```
  >NOTE: you would need to click into the rviz or simulation for the 
  > arrow_key_teleop drive to start woking. because it uses pynput
  >
  >NOTE: also feel free to use any other **teleop package** you want 

- **Save Occupancy Grid Map (Raspberry Pi):**
  ```shell
  ros2 run nav2_map_server map_saver_cli -f /home/$USER/mobo_bot_ws/src/mobo_bot/mobo_bot_navigation/maps/<map_name> 
  ```

- **Save PoseGraph Map (Raspberry Pi):**
  ```shell
  ros2 service call /slam_toolbox/serialize_map slam_toolbox/srv/SerializePoseGraph "{filename: '/home/$USER/mobo_bot_ws/src/mobo_bot/mobo_bot_navigation/maps/<map_name>'}"
  ```
  
- **Rebuild Package to include newly created map (Raspberry Pi):**
  ```shell
    cd ~/mobo_bot_ws && colcon build --symlink-install
  ```
  
<br/>

---
<br/>

### 🎮 MoboBot Navigation (Hardware)
> **NOTE**: run in different terminals.

- **Start Navigation with AMCL Localization and Occupancy Grid Map (Raspberry Pi):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup robot_navigation.launch.py map_name:=<map_name>
  ```

**OR**

- **Start Navigation with SLAM Localization and PoseGragh Map (Raspberry Pi):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup robot_navigation.launch.py map_name:=<map_name> use_slam:=True serialized_map_name:=<map_name>
  ```

- **View and Control MoboBot in RVIZ (Dev PC):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_rviz mapping_and_navigation.launch.py
  ```

#
