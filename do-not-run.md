### 🎮 MoboBot 2D Mapping with SLAM (Simulation)
> **NOTE**: run in different terminals.

- **Start Mapping:**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup sim_mapping.launch.py \
   world_name:=room_with_walls
  ```

- **Control with Keyboard To Update Map:**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 run arrow_key_teleop_drive arrow_key_teleop_drive 0.15 0.7 true
  ```
  >NOTE: you would need to click into the rviz or simulation for the 
  > arrow_key_teleop drive to start woking. because it uses pynput
  >
  >NOTE: also feel free to use any other **teleop package** you want 

- **Delete Existing Maps (Optional):**
  ```shell
  rm -rf /home/$USER/mobo_bot_ws/src/mobo_bot/mobo_bot_navigation/maps/room_with_walls*
  ```

- **Save Occupancy Grid Map (Optional):**
  ```shell
  ros2 run nav2_map_server map_saver_cli -f /home/$USER/mobo_bot_ws/src/mobo_bot/mobo_bot_navigation/maps/room_with_walls
  ```

- **Save PoseGraph Map (Optional):**
  ```shell
  ros2 service call /slam_toolbox/serialize_map slam_toolbox/srv/SerializePoseGraph "{filename: '/home/$USER/mobo_bot_ws/src/mobo_bot/mobo_bot_navigation/maps/room_with_walls'}"
  ```
  
<br/>

---
<br/>

### 🎮 MoboBot Navigation (Simulation)
> **NOTE**: run in different terminals.

- **Start Navigation (with AMCL Localization and Occupancy Grid Map):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup sim_navigation.launch.py \
  world_name:=room_with_walls \
  ```

**OR**

- **Start Navigation (with SLAM Localization and Posegraph Map):**
  ```shell
  source ~/mobo_bot_ws/install/setup.bash && ros2 launch mobo_bot_bringup sim_navigation.launch.py \
  world_name:=room_with_walls \
  use_slam:=True \
  serialized_map_name:=room_with_walls \
  # nav_params_name:=nav2_params_omni
  ```
  
#