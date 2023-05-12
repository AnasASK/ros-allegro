# Deployment of Allegro Hand

## Disclaimer

This repository and README is heavily based on Felix Duvallet's Allegro ROS repository (https://github.com/felixduvallet/allegro-hand-ros), with modification for the [in-hand object rotation](https://github.com/HaozhiQi/hora) repository.

## Installation

### PCAN

Download the [peak linux driver](http://www.peak-system.com/fileadmin/media/linux/index.htm#download) and unzip it. In the driver folder, execute the following command:
```
# in peak-linux-driver
make clean
make NET=NO_NETDEV_SUPPORT
sudo make install
sudo /sbin/modprobe pcan
```
After this above installation, you should be able to see `/dev/pcanusb*` in your machine.

### Install this repository

```
cd ${CATKIN_WS}/src/
git clone https://github.com/HaozhiQi/ros-allegro.git
cd ../
catkin_make -j1
catkin_make install
source ./devel/setup.zsh # or other shell name
```

### Hardware 
- Connect the PCAN USB adapter to the arm, and the power supply 
- Turn on the Allegro power (you will hear a sound)

### Runtime instructions

Can use `rostopic list` to monitor the ROS topics.

Try a communication with hand
```
conda activate rosallegro
roslaunch allegro_hand allegro_hand.launch HAND:=left AUTO_CAN:=false CAN_DEVICE:=/dev/pcanusb32 KEYBOARD:=false CONTROLLER:=pd # left hand
roslaunch allegro_hand allegro_hand.launch HAND:=right AUTO_CAN:=false CAN_DEVICE:=/dev/pcanusb32 KEYBOARD:=false CONTROLLER:=pd # right hand

```

Make sure `rostopic list` will display something like:
```shell
/allegroHand_0/envelop_torque
/allegroHand_0/joint_cmd
/allegroHand_0/joint_states
/allegroHand_0/lib_cmd
```