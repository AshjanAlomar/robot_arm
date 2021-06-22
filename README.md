# robot_arm
ROS packages that can be used to plan and execute motion trajectories for a robot arm in simulation and real-life.
## Steps to download ros and connected to Arduino :
# 1-	VM:
- You should download virtual box (I download version 6.1 it’s work on windows and mac also https://www.virtualbox.org/wiki/Downloads ).
# 2-	Ubuntu :
-	After you download the VM you starting to download ubuntu you can either download ubuntu 18.04 desktop image (which I did ) https://releases.ubuntu.com/18.04/ 
-	or ubuntu 20.04 or you can download ubuntu mate 18.04 https://ubuntu-mate.org/download/amd64/bionic/ .
# 3-	Ros:
-	Now you can open the terminal and start to download ros http://wiki.ros.org/melodic/Installation/Ubuntu
# •	Setup your sources. list By enter this step in the terminal .
``` sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list' ```

# •	Set up your keys By enter this step in the terminal:
```sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654 ```

# •	Installation By enter this step in terminal :
```
1-	Sudo apt update 
2-	Sudo apt upgrade 
``` 

# •	Desktop-full installation :
``` sudo apt install ros-melodic-desktop-full ``` 
# •	Environment setup:
```
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
# •	Dependencies for building packages: 
```
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
•	Initialize rosdep:
1-	sudo apt install python-rosdep
2-	sudo rosdep init
3-	rosdep update
```
# •	To start the Ros Enter 
``` $roscore ```
# 4-	Workspace:
-	http://wiki.ros.org/catkin/Tutorials/create_a_workspace 
# 1-	 Prerequisites:
```
o	$ source /opt/ros/melodic/setup.bash (be carful her in the name of the version you use )
o	$ mkdir -p ~/catkin_ws/src
o	$ cd ~/catkin_ws/
o	$ catkin_make
o	$ echo "source ~/catkin_ws/devel/setup.bash" >> ~/.bashrc
```
ROS packages that can be used to plan and execute motion trajectories for a robot arm in simulation and real-life.
These packages were tested under ROS kinetic and Ubuntu 16.04 and it works perfectly on ROS melodic The robot arm uses Moveit plugin to apply kinematics by the KDL solver. These packages can be tested in the gazebo simulation tool and the real robot arm, where the ROS system and Arduino code share the /joint_states topic to control motors.(github@smart-methods)
# 5-	Installing the package arduino_robot_arm:
### 1-	Add the “arduino_robot_arm” package to “src” folder:
```
o	$ cd ~/catkin_ws/src
o	$ sudo apt install git
o	$ git clone https://github.com/smart-methods/arduino_robot_arm
```

### 2-	Install all the dependencies :
```
o	$ cd ~/catkin_ws
o	$ rosdep install --from-paths src --ignore-src -r -y
o	$ sudo apt-get install ros-melodic-moveit
o	$ sudo apt-get install ros-melodic-joint-state-publisher ros-melodic-joint-state-publisher-gui
o	$ sudo apt-get install ros-melodic-gazebo-ros-control joint-state-publisher
o	$ sudo apt-get install ros-melodic-ros-controllers ros-melodic-ros-control
```

### 3-	Compile the package:
```
o	$ catkin_make
```
# 6-	Controlling the motors by enter this line :
```
$ roslaunch robot_arm_pkg check_motors.launch
```
# 7-	Arduino IDE in ubuntu :
### 1-	install (https://www.arduino.cc/en/Main/Software)
### 2-	install rosserial http://wiki.ros.org/rosserial_arduino/Tutorials/Arduino%20IDE%20Setup 
- by enter this two commands :
```
o	$ sudo apt-get install ros-kinetic-rosserial-arduino
o	$ sudo apt-get install ros-kinetic-rosserial
```
### 3-	Install ros_lib :
- http://wiki.ros.org/rosserial_arduino/Tutorials/Arduino%20IDE%20Setup 
- by enter this commands:
```
o	$ cd <sketchbook>/libraries
o	$ rm -rf ros_lib
o	$ rosrun rosserial_arduino make_libraries.py .
```
# 8-	Upload the Arduino code
```
o	 select the Arduino port to be used on Ubuntu system
o	change the permissions (it might be ttyACM)
o	$ ls -l /dev |grep ttyUSB
o	$ sudo chmod -R 777 /dev/ttyUSB0
o	upload the code from Arduino IDE
```

# 9-	joint_state_publisher with Arduino:
- •	Run Rviz:
```

o	$ roslaunch robot_arm_pkg check_motors.launch
o	$ rosrun rosserial_python serial_node.py _port:=/dev/ttyUSB0 _baud:=115200
```
# 10-	Controlling the motors in simulation:
```
•	$ roslaunch robot_arm_pkg check_motors.launch
•	$ roslaunch robot_arm_pkg check_motors_gazebo.launch
•	$ rosrun robot_arm_pkg joint_states_to_gazebo.py
•	You may need to change the permission 
o	$ cd catkin/src/arduino_robot_arm/robot_arm_pkg/scripts
o	$ sudo chmod +x joint_states_to_gazebo.py
```

# 11-	Creating the manipulation Movelt In Rviz:
```
•	Used for kinematics, motion planning, trajectory processing and controlling the robot
o	$ roslaunch moveit_setup_assistant setup_assistant.launch
o	In a new terminal ($ roslaunch moveit_pkg demo.launch)
o	$ rosrun rosserial_python serial_node.py _port:=/dev/ttyUSB0 _baud:=115200
o	$ roslaunch moveit_pkg demo_gazebo.launch
```


### If you had any error droning the installation (like me ) you can use this website to see the simulation of the arm 
- 	https://www.theconstructsim.com/rds-ros-development-studio/ 
![image](https://user-images.githubusercontent.com/86170422/123003542-010eed80-d3bc-11eb-933e-3af6b2b7d2e1.png)

![image](https://user-images.githubusercontent.com/86170422/123003595-14ba5400-d3bc-11eb-810a-bb9d7b985c17.png)













