# phantomx_reactor_arm_v2

<h2>Description</h2>
The PhantomX Reactor Robot Arm is the first in Interbotix Labs' offering of Arbotix based research grade robotic arms. The Reactor Arm was designed with reach and agility in mind, but it still boasts considerable strength for an arm of its size. The PhantomX Reactor Robot Arm was designed with entry-level research and university use in mind, providing one of the highest featured arms on the market today while not breaking one's budget.

<h2>Supported Hardware</h2>

![Image of PhantomX reactor arm](http://www.trossenrobotics.com/resize/Shared/images/PImages/reactor/reactor-1a.jpg?bw=1000&bh=1000)


# phantomx_reactor_arm_description
This package contains the PhantomX reactor arm model (urdf, meshes, ...).

# phantomx_reactor_arm_description_v2
This package contains the configuration files for the controllers used by the model.
The arm can only be controlled through USB2Dynamixel.

## Installation and configuration 

### Downloading the package

clone the repo into your workspace and compile it.
```bash
git clone https://github.com/RobotnikAutomation/phantomx_reactor_arm.git
```
### Creating the udev rule for the device

#### For the USB2Dynamixel

In the phantomx_reactor_arm_description_v2/config folder there's the file 57-reactor_usb2dynamixel.rules. You have to copy it into the /etc/udev/rules.d folder.

```bash
sudo cp 57-reactor_usb2dynamixel.rules /etc/udev/rules.d
```

You have to set the attribute ATTRS{serial} with the current serial number of the ftdi device

```bash
udevadm info -a -n /dev/ttyUSB0 | grep serial 
```
Once modified you have to reload and restart the udev daemon

```bash
sudo service udev reload
sudo service udev restart
sudo udevadm trigger
```

### Running the controller

#### USB2Dynamixel Controller

* Run the controller
```bash
roslaunch phantomx_reactor_arm_description_v2 dynamixel_phantomx_reactor_arm_no_wrist.launch 
```

* Run Moveit plugin for RVIZ
Running moveit with the real controllers
```bash
roslaunch phantomx_reactor_arm_moveit_config demo_real.launch
```

### Commanding the controller 

```bash
rostopic pub /shoulder_yaw_joint/command std_msgs/Float64 "data: 0.0"
rostopic pub /shoulder_pitch_joint/command std_msgs/Float64 "data: 0.0"
rostopic pub /elbow_pitch_joint/command std_msgs/Float64 "data: 0.0"
rostopic pub /wrist_yaw_joint/command std_msgs/Float64 "data: 0.0"
rostopic pub /wrist_pitch_joint/command std_msgs/Float64 "data: 0.0"
rostopic pub /gripper_revolute_joint/command std_msgs/Float64 "data: 0.0"
rostopic pub /gripper_prismatic_joint/command std_msgs/Float64 "data: 0.0"
```
