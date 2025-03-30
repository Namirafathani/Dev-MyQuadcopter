# Dev-MyQuadcopter
Setting up the development of research quadcopter.

Step of Configuring the Laptop

1. Installing Ubuntu 22.04
- Check the python version that already installed on Ubuntu 22.04, On terminal
```javascript
python3 --version
whereis python3
```
(for my installation, python is already installed with version 3.10.12)
(whereis python3, must reply that the python3 on /usr/bin/python3)

2. Install the VSCode
- For VSCode installation on Linux, follow the step like this
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

3. Install ROS2 Humble
4. Install the Miniconda
5. Clone the PX4-Autopilot Repository
