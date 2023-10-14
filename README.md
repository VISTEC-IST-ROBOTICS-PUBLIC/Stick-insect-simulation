# Stick-insect-simulation
![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/83fc067a-3647-4d35-9fe3-56ba521807a6)


## (a) Systems
- Ubuntu 20.04
- ROS1
- CoppeliaSim simulation (Education version 4.4.0)

## (b) Needed skill
- Ubuntu command line
- C++ and Lua languages programming
- Basic ROS1
  - catkin
  - creat package
  - topic and message
- Basic CoppeliaSim simulation
    - Create object and joint
    - Create joint
    - Move and rotate an object

## (c) Files explaination
![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/27ca4b3d-b55e-4a2a-bc03-7627cf8bf8f8)
![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/0209f8a8-dc17-48c5-8c8a-880ac83315b6)

## (d) Preparing the system
- Create a "catkin workspace" >> [see example](http://wiki.ros.org/catkin/Tutorials/create_a_workspace)
- Download the code from [the repository](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/tree/master/stick_insect_sim_pkg) and catkin_make to compile
- Add "source <your path to workspace>/devel/setup.bash" to .bashrc >> [see example](https://answers.ros.org/question/206876/how-often-do-i-need-to-source-setupbash/)

## (e) How to run the simulation
In the provided files, we have two simulation system
### (1) fixed Leg trajectory simulation
This system contains only __medaextra-fixed_CPG.ttt__, this system is used to observe the leg trajectory data from a real insect and extract it to robot motor commands.
Then, the motor commands are used to be a target in RBF network, and we can obtain RBF weights to transfer CPG signals to motor signals. We can run this simulation file without using ROS1.
See the figure for more explanation.

#### The stick insect system
  ![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/210be94d-f760-4609-87bf-3620cbda53df)

#### Visibility in the simulation
  ![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/2716ed37-7a0f-4997-b213-e749b6217d70)

#### Check the trajectory path
  ![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/ce281b21-f4ae-4a7b-b88c-54a4ac53c32a)



### (2) The stick insect simulation with self-organized locomotion control
This system uses the remaining files to run the system. We use ROS1 for interfacing (sending motor commands, receiving feedback signals, etc) with the simulation.
You can run this system by following the steps below.
- Change the file path to match my own machine!!!
  - In __rbfn.h__ >> line 51
    ![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/4b9acddc-7c95-4242-9d90-66ff14b46ecc)
  - In rbfn_semicircle.h__ >> line 48
    ![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/76156a55-1005-4c66-af2f-a122a7f8fc55)
- Open a terminal and run "__roscore__"
- Open CoppeliaSim >> [see example](https://forum.coppeliarobotics.com/viewtopic.php?t=9148\)
- In the simulation, Open the scene from the downloaded folder “__medaextra_ver2.ttt__”
- You will see the stick insect robot, then run :arrow_forward:
![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/99d05e04-6962-4bd9-8cdf-ec959cdcfa82)


______
##### Author: Thirawat Chuthong (Joe) (contact: thirawat.c_s21[at]vistec.ac.th)













