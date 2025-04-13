# Dev-MyQuadcopter
Setting up the development of research quadcopter.

Step for testing implementation ros2 offboard control with px4
1. Clone the px4_msgs and px4_ros_com
```javascript
source opt/ros/humble/setup.bash
mkdir my_devQuad1/src
cd my_devQuad1/src
git clone https://github.com/PX4/px4_msgs.git -b release/1.14
# checkout the matching release branch if not using PX4 main.
git clone https://github.com/PX4/px4_ros_com.git -b release/v1.14
```
the new folder has been created again, because before we use the env make the colcon build has not been success
2. Build the source
```shell
cd ..
colcon build
source install/local_setup.bash
```
3. Open your Micro-XRCE-DDS Agent (New Terminal)
```shell
cd dev_myQuad0/Micro-XRCE-DDS-Agent
MicroXRCEAgent udp4 -p 8888
```
4. Running the offboard control programs (back to the terminal step number 2)
```shell
ros2 run px4_ros_com offboard_control
```
![Simulation Offboard Control](Screencastfrom04-08-2025111006AM-ezgif.com-video-to-gif-converter.gif)

This command, execute the px4_ros_com package, and offboard_control from src/examples/offboard/offboard_control.cpp

#
