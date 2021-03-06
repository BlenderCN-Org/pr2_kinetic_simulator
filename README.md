# PR2 Simulator for Grasping

This repository provides the guidelines to install the PR2 simulator, for reaching and grasping purposes, in ROS kinetic and Ubuntu 16.04LTS environment.

### Pre-requisites
* If your system does not have the OMPL installation then clone this repository and extract the contents of the folder "prerequisites".
* Navigate to the folder `cd path/to/prerequisites` and run:`./install_pr2_kinetic.sh`. This script will install the needed dependencies for the simulator and the OMPL libraries for the planning.
* If your system does not have MoveIt then: `sudo apt-get install ros-kinetic-moveit`.
* This repository contains a slightly modified graspIt version (with files later used for the Gazebo simulator). Copy the folder "graspit".
* Navigate to the folder `cd ~/path/to/graspit` and install:
```
mkdir build
cd build
cmake ..
make -j8
sudo make install
```
* The original graspit can be found [here](https://github.com/graspit-simulator/graspit_interface)
* Export the library path and environmental variable (Preferably copy them to your ~/.barshc file):
```
export LD_LIBRARY_PATH=/usr/local/lib:$LD_LIBRARY_PATH
export GRASPIT=~/.graspit
```

### Simulator installation
* Create a workspace for the simulator `mkdir pr2_kinetic_simulator_ws`
* Navigate to the workspace 'cd path/to/pr2pr2_kinetic_simulator_ws' and copy the folder "src"
* Build it with: `catkin_make`

### Test the modules
* Open a terminal and:
```
source ~/pr2_kinetic_simulator_ws/deve/setup.bash
roslaunch system_launch pr2_mug.launch
```
* You should see the gazebo, rviz and graspit
* Open a second terminal and:
```
source ~/pr2_kinetic_simulator_ws/deve/setup.bash
cd ~/pr2_kinetic_simulator_ws/src/grasp_it_modules/script
python grasp_execution.py
```
* You should see the gazebo and rviz with the object (mug) and the graspit module with the plans:


<img src="https://github.com/PaolaArdon/pr2_kinetic_simulator/blob/master/images/pr2_kitchen.png" width="240" height="200">   <img src="https://github.com/PaolaArdon/pr2_kinetic_simulator/blob/master/images/rviz_pr2.png" width="240" height="200"> <img src="https://github.com/PaolaArdon/pr2_kinetic_simulator/blob/master/images/graspIt_plans.png" width="240" height="200">

### Modifying the objects to grasp

* In the folder ~/path/to/grasp_it_modules/scripts there are two scripts: utils_grasp.py and grasp_execution.py. In the script utils_grasp.py you can change the object to be grasped. Two types of files have been tested: urdf and sdf.

* If you wish to make use a different object make sure to have the 3D file of the object and place it in ~/path/to/graspit/models/objects alongside the respective .xml. Additionally,  add the .xml that describes your world (transformation matrices and camera position) in ~/path/to/graspit/worlds and change the gc.loadWorld name in the utils_grasp.py (line 18).
