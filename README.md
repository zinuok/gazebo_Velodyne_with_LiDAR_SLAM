***
# Velodyne-gazebo
***
**< reference github link >**
+ [Velodyne](https://bitbucket.org/DataspeedInc/velodyne_simulator/src/master/)
+ [LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)
+ [LIO-SAM](https://github.com/TixiaoShan/LIO-SAM#prepare-lidar-data)
<br>

# Index
<!--
### 1. Prerequisites
####    &nbsp;&nbsp;&nbsp;&nbsp;● LCM
####    &nbsp;&nbsp;&nbsp;&nbsp;● Boost
####    &nbsp;&nbsp;&nbsp;&nbsp;● CMake
####    &nbsp;&nbsp;&nbsp;&nbsp;● unitree_legged_sdk
####    &nbsp;&nbsp;&nbsp;&nbsp;● aliengo_sdk
-->
### 1. Install
####    &nbsp;&nbsp;&nbsp;&nbsp;● LiDAR sensor: Velodyne
####    &nbsp;&nbsp;&nbsp;&nbsp;● robot model: champ-anymal_b
####    &nbsp;&nbsp;&nbsp;&nbsp;● LiDAR SLAM: 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  1) LeGO-LOAM  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  2) LIO-SAM
### 2. Applying Model
####    &nbsp;&nbsp;&nbsp;&nbsp;● sensor attachment to the robot model
### 3. Run


<br><br>


## 1. Install
+ **installing Velodyne**
```
$ cd <your_ws>/src
$ git clone https://bitbucket.org/DataspeedInc/velodyne_simulator.git
$ cd .. && catkin build -$(nproc)
```

+ **installing robot model** <br>
refer [quad-legged](https://github.com/zinuok/quad-legged)

+ **installing LiDAR-based SLAM** 
+ **1) LeGO-LOAM** <br>
you have to install **GTSAM ver. 4.0.3**. Otherwise, it could produce some error
```
$ wget -O ~/Downloads/gtsam.zip https://github.com/borglab/gtsam/archive/4.0.3.zip
$ cd unzip gtsam.zip
$ cd ~/Downloads/gtsam-4.0.3/
$ mkdir build && cd build
$ cmake ..
$ sudo make install
```
```
$ sudo apt install -y libparmetis-dev
$ cd <your_ws>/src
$ git clone https://github.com/RobustFieldAutonomyLab/LeGO-LOAM.git
$ cd .. && catkin build -$(nproc)
$ source ./devel/setup.bash
```
**< Trouble shooting >**
+ **removing GTSAM** <br>
from [here](https://github.com/borglab/gtsam/issues/562#issuecomment-721899131). 
GTSAM is not deleted in the normal way.
```
$ cd <your GTSAM build dir> && sudo xargs rm -rf < install_manifest.txt
``` 

<br>

+ **2) LIO-SAM** <br>
install pre-requirities
```
$ sudo apt install -y ros-melodic-navigation
$ sudo apt install -y ros-melodic-robot-localization
$ sudo apt install -y ros-melodic-robot-state-publisher

# GTSAM ver. 4.0.2
$ wget -O ~/<your_ws>/gtsam.zip https://github.com/borglab/gtsam/archive/4.0.2.zip
$ cd ~/<your_ws> && unzip gtsam.zip
$ cd ~/<your_ws>/gtsam-4.0.2/
$ mkdir build && cd build
$ cmake -DGTSAM_BUILD_WITH_MARCH_NATIVE=OFF ..
$ sudo make install -j $(nproc)
```

install LIO-SAM
```
$ cd <your_ws>/src
$ git clone https://github.com/TixiaoShan/LIO-SAM.git
$ cd .. && catkin build -j $(nproc)
$ source ./devel/setup.bash
```

**< Trouble shooting >**
+ **[imageProjection-4] process has died** <br>
refer [here](). <br> 
This is usually because the height and width of the sensor_msgs/PointCloud2 type, which is LiDAR data, are reversed.
For example, to use LIO-SAM, the 'height=1' condition must be satisfied. Check it and if it's the opposite, make a ROS node and reverse it.


<br><br>

## 2. Applying Model
#### ● This is done if you use [my edited version](https://github.com/zinuok/quad-legged) as above install descriptions.
#### ● LiDAR + IMU are loaded with the robot model, for running LIO-SAM.
<br><br>

## 3. Run
```
$ roslaunch lio_sam run.launch
```

