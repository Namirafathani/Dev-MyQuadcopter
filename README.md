# Dev-MyQuadcopter
Setting up the development of research quadcopter.

Step of Configuring the Laptop

1. Installing Ubuntu 22.04
Check the python version that already installed on Ubuntu 22.04, On terminal
```javascript
python3 --version
whereis python3
```
(for my installation, python is already installed with version 3.10.12)
(whereis python3, must reply that the python3 on /usr/bin/python3)

2. Install the VSCode
For VSCode installation on Linux, follow the step like this
```javascript
sudo apt install ./<file>.deb
# If you're on an older Linux distribution, you will need to run this instead:
# sudo dpkg -i <file>.deb
# sudo apt-get install -f # Install dependencies
```
```javascript
echo "code code/add-microsoft-repo boolean true" | sudo debconf-set-selections
```
```javascript
sudo apt-get install wget gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
rm -f packages.microsoft.gpg
```
```javascript
sudo apt install apt-transport-https
sudo apt update
sudo apt install code # or code-insiders
```
- for opening the visual studio code, from terminal
```javascript
code .
```
Install python add-on on Vscode, after complete, access it on View >> Terminal
Check the Intreperter on bottom right corner, you can select the python version for interpreter

3. Install ROS2 Humble
Installation of ROS2 Humble, follow this step
```javascript
locale  # check for UTF-8
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
locale  # verify settings
sudo apt install software-properties-common
sudo add-apt-repository universe
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
sudo apt update
sudo apt upgrade
sudo apt install ros-humble-desktop
sudo apt install ros-humble-ros-base
sudo apt install ros-dev-tools
```
Trying the installation is success, try to source (if source cannot do, maybe the python3 is not on machine or not in /usr/bin/python3)
```javascript
source /opt/ros/humble/setup.bash
```
Try some example
```javascript
source /opt/ros/humble/setup.bash
ros2 run demo_nodes_cpp talker
```
Open new terminal, filled with
```javascript
source /opt/ros/humble/setup.bash
ros2 run demo_nodes_py listener
```
Ctrl+D for ended the simulation

4. Install the Miniconda
Installation of miniconda, follow this step
```javascript
mkdir -p ~/miniconda3
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda3/miniconda.sh
bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
rm ~/miniconda3/miniconda.sh
source ~/miniconda3/bin/activate
conda init --all
```
After this installation, the terminal fisrt name is (base), it is the initial source environment, Check the environment that already we have
```javascript
conda env list
```
When you check the version of python on base environment, it reply thet the version is 3.12.9 (it is from the miniconda)
Create new virtual environment with python version is 3.10.12 with name my_devQuad
```javascript
conda create --name my_devQuad python=3.10.12
```
Activate the venv my_devQuad
```javascript
conda activate my_devQuad
```
When you want Deactivate the venv
```javascript
conda deactivate my_devQuad
```
We use this virtual environment to programming and testing the Quadcopter, try to source on venv my_devQuad
```javascript
source /opt/ros/humble/setup.bash
```
when it  reply nothing, the source of ros2 is succeed

5. Clone the PX4-Autopilot Repository
clone the repository PX4-Autopilot with version v1.14 (using the venv my_devQuad). 
```javascript
mkdir -p Dev_myQuad
cd Dev_myQuad
git clone -b v1.14.3 https://github.com/PX4/PX4-Autopilot.git --recursive
bash ./PX4-Autopilot/Tools/setup/ubuntu.sh
cd PX4-Autopilot
make px4_sitl gz_x500
```
Ctrl+c from terminal for closing the simulation
When the simulation start, it running the pixhawk on gazebo (it define with client)
if the gazebo cannot open, do distclean
```javascript
git submodule update --recursive
make distclean
```
If you still have the error, and the terminal says that "AttributeError": module 'em' has no attribute 'RAW_OPT'. It says that your em module, need another version. Uninstall it and install again with the version that PX4 accepted. Try with this:
```javascript
pip uninstall em
pip install empy==3.3.4
```

6. Clone the Agent repository
Clone the Micro-XRCE-DDS-Agent for later used in Raspberry Pi 
```javascript
git clone https://github.com/eProsima/Micro-XRCE-DDS-Agent.git
cd Micro-XRCE-DDS-Agent
mkdir build
cd build
cmake ..
make
sudo make install
sudo ldconfig /usr/local/lib/
```
Starting the client and then the agent, if the connection of two is succeeded. The ros2 topic can be look by:
```javascript
ros2 topic list
```

7. Install the Client / Ground Control (QGroundcontrol)

