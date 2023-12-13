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
  - In __rbfn_semicircle.h__ >> line 48
    ![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/76156a55-1005-4c66-af2f-a122a7f8fc55)
- Open a terminal and run "__roscore__"
- Open CoppeliaSim >> [see example](https://forum.coppeliarobotics.com/viewtopic.php?t=9148\)
- In the simulation, Open the scene from the downloaded folder “__medaextra_ver2.ttt__”
- You will see the stick insect robot, then run :arrow_forward:
![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/99d05e04-6962-4bd9-8cdf-ec959cdcfa82)
______
##### Author: Thirawat Chuthong (Joe) (contact: thirawat.c_s21[at]vistec.ac.th)
___________________________________

# Upload CSV file to CoppeliaSim (VREP)
## Introduction
In this tutorial, it will be shown how to upload a CSV file to CoppeliaSim (VREP). A script will be used to read
the CSV file and create a trajectory for the robot/object that you intend to move.

## Prerequisites
- CoppeliaSim (VREP) installed.
- CSV file with the trajectory to be followed.
- CoppeliaSim scene with the robot/object that will follow the trajectory.

## Step 1: Create a CSV file with the trajectory to be followe
The CSV file must have the following format:
- ![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/bcd3130a-a172-4f7c-8741-1a00dd61cb52)

For example:
- ![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/dc793bd4-58c5-4ea9-8f7a-4c941b2eddfa)

This is the only format that CoppeliaSim accept for the paths. The first row must contain the names of the
columns, and the following rows must contain the values of the trajectory. By using third part programs like
excel or google sheets, you can create the CSV file and save it in .csv format.

## Step 2: CoppeliaSim scene
In CoppeliaSim scene, you will need to add a dummy object. This object will be the one that will follow the
trajectory. (it can be any kind of object, even a primitive shape like cuboids) After adding the dummy object,
![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/1a0d4106-1394-45d1-99fc-1f29e5a52af5)

you will need to add this script by right clicking on the dummy object and selecting Add -> Associated
child script -> Non-threaded.
![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/8817fa34-6491-467e-a5b0-341fb0a37d6a)

Then, you will need to copy this script to the dummy object script.

```lua
  function sysCall_init()
  -- Check current path of your script file
   local currentPath = sim.getStringParam(sim.stringparam_scene_path)
   print(currentPath)
  -- Create an array to store the data
   local csvPath = {}
  -- Open your csv file : relate to your current path
   local file = io.open(currentPath .. "/path&to&your&file.csv", "r")
   print("open")
   if file then
   print("file")
  -- Read and store each line of data in the array
   for line in file:lines() do
   for value in line:gmatch("([^,]+)") do
   table.insert(csvPath, tonumber(value))
   end
   end
  -- Close the file
   file:close()
  -- Now 'csvPath' contains your CSV data in a Lua array
  -- You can use 'csvPath' for further processing in your simulation
   else
   print("Failed to open the file")
   end
   print(csvPath)
  -- This is a simple path you can use this stead of csvPath
   local simPath = {
   0.1,0.1,0.1,0,0,0,1,
   0.2,0.2,0.2,0,0,0,1,
   0.3,0.3,0.3,0,0,0,1,
   0.4,0.4,0.3,0,0,0,1,
   0.5,0.5,0.2,0,0,0,1,
   0.4,0.4,0.1,0,0,0,1,
   0.3,0.3,0.1,0,0,0,1,
   0.2,0.2,0.2,0,0,0,1,
   0.1,0.1,0.3,0,0,0,1}
  -- Create path
   sim.createPath(csvPath,16)
  end
```

In the script, you will need to change the path to your CSV file. You can do this by changing the following
line:
```lua
  local file = io.open(currentPath .. "/path&to&your&file.csv", "r")
```

## Step 3: Use the script to read the CSV file and create the trajectory
Now, to exploit the script you will need to run the simulation. After running the simulation, the script will
read the CSV file and create the trajectory. To see the trajectory, you will need to select the dummy object
and then select the path that was created by the script.

WHEN THE SIMULATION IS STILL RUNNING is possible to copy the path object, stop the simulation and
paste the path object in the scene. This way you will be able to see the trajectory without running the
simulation

![image](https://github.com/VISTEC-IST-ROBOTICS-PUBLIC/Stick-insect-simulation/assets/21343117/29d8aa84-c1e5-44c3-a291-6a849511450a)


##### Author: 
Gian Paolo Currá (contact: gicur22@student.sdu.dk) and Thirawat Chuthong (contact: thirawat.c_s21[at]vistec.ac.th)

