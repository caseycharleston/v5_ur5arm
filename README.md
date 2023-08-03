

# Installation

This package is meant to be used within a catkin workspace inside of the [bwi-docker](https://github.com/utexas-bwi/bwi-docker) repository.

Follow the [install](https://github.com/utexas-bwi/bwi-docker#install) and [setup](https://github.com/utexas-bwi/bwi-docker#setup) instructions to configure the docker.

Once installed, navigate to the bwi-docker projects folder and download the arm package into your workspace:
```
cd projects
mkdir -p catkin_ws/src
cd catkin_ws/src
git clone https://github.com/caseycharleston/v5_ur5arm.git
```

# Dependencies
The **ur5_robotiq_gripper.urdf.xacro** file in `ur5_description/urdf` requires the related robotiq gripper URDF files to be installed.

Install the robotiq repository:
```
cd path/to/catkin_ws/src
git clone https://github.com/filesmuggler/robotiq.git
```

Once installed, there is one edit you need to make before running. Navigate to the `robotiq_85_gripper.transmission.xacro` file and do the following:
1. uncomment lines 10 and 15
2. comment lines 9 and 14

So it resembles this (lines 6 - 17):
```
    <transmission name="${prefix}robotiq_85_left_knuckle_trans">
      <type>transmission_interface/SimpleTransmission</type>
      <joint name="${prefix}robotiq_85_left_knuckle_joint">
        <!-- <hardwareInterface>PositionJointInterface</hardwareInterface> -->
        <hardwareInterface>EffortJointInterface</hardwareInterface>
      </joint>
      <actuator name="${prefix}robotiq_85_left_knuckle_motor">
        <mechanicalReduction>1</mechanicalReduction>
        <!-- <hardwareInterface>PositionJointInterface</hardwareInterface> -->
        <hardwareInterface>EfforJointInterface</hardwareInterface>
      </actuator>
    </transmission>
```
This will put the gripper's primary joint on the correct interface so it can be used for simulation.

# Building

Building this package requires the use of the bwi-docker bash tools. For descriptions of their usage, see the bwi-docker [usage](https://github.com/utexas-bwi/bwi-docker#usage) section.

Start the docker environment:
```
cd path/to/bwi-docker
bwi-start
bwi-shell
```

build necessary packages with catkin:
```
cd catkin_ws
catkin_make
```

# Testing

To ensure that the the package was installed successfully, run the gazebo demo launch file within the `ur5_moveit_config` package. Before running this, make sure you first do the building instructions in the previous seciton.
```
source devel/setup.bash
roslaunch ur5_moveit_config demo_gazebo.launch
```
