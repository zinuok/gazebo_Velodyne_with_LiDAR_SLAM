***
# Velodyne-gazebo
+ velodyne: [link](https://bitbucket.org/DataspeedInc/velodyne_simulator/src/master/)
***
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
####    &nbsp;&nbsp;&nbsp;&nbsp;● LiDAR SLAM: LeGO-LOAM
### 2. Applying Model
####    &nbsp;&nbsp;&nbsp;&nbsp;● sensor attachment to the robot model
### 3. Run
<br><br>
+ **reference github link**: [LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM)



## 1. Install
+ **installing Velodyne**
```
$ cd <your_ws>/src
$ git clone https://bitbucket.org/DataspeedInc/velodyne_simulator.git
$ cd .. && catkin build -$(nproc)
```

+ **installing robot model** <br>
refer [quad-legged](https://github.com/zinuok/quad-legged)

+ **installing LiDAR SLAM: LeGO-LOAM** <br>
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
$ cd <your_ws>/src
$ git clone https://github.com/RobustFieldAutonomyLab/LeGO-LOAM.git
$ cd .. && catkin build -$(nproc)
$ source ./devel/setup.bash
```
**< Trouble shooting >**
+ removing GTSAM <br>
GTSAM is not deleted in the normal way
```
$ cd <your GTSAM build dir> && xargs rm -rf < install_manifest.txt
``` 
+ [mapOptmization-7] process has died
refer [here]()
```
```

<br><br>

## 2. Applying Model
#### ● Actually
<br><br>

## 3. Run
+ please r

