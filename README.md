# Robot-Hazard-Analysis-Simulation
## Introduction
This example shows how simulation of collaborative robot workflows can be used to uncover potential hazards for the human worker. It is motivated by the problem of design-time risk assessment of robot systems. The main research questions that are addressed by this example are:
1. How can we use simulation to identify potential hazards in an early development stage (i.e., before the system is built and commissioned in real life)?
2. How can we identify hazardous worker behaviors that are likely to cause unsafe states wen performed in interaction with the robot system?

## Concept
The general approach of this example is to simulate a collaborative workflow of human and robot and to evaluate a risk metric during the simulation. The risk metric is based on factors such as human-robot distance, velocity, estimated collision forces, and more. Our objective is to expose hazards by finding unsafe states (more specifically, human-robot collisions that exceed a certain force limit). We achieve this by varying the behavior of the human worker in simulation, and recording behaviors where the the risk metric exceeds a certain threshold. We vary the behavior of the human worker both on an action-level (e.g. the human worker can omit an action or switch the order of actions in the workflow) and on a motion-level (e.g., the worker can walks to a slighly different position each time). Since this results in a vast search space of possible behaviors, we use a search algorithm that is guided by the risk metric and tries to find as many high-risk behaviors as possible (note to reviewers: At this point, we will link to the paper for more explanation once it is published).

## Prerequisites
This example was developed using Ubuntu 18.04 and CoppeliaSim 4.2). To run this example, you need:
- CoppeliaSim 4.2 or newer (available [here](https://www.coppeliarobotics.com/downloads))
- The Lua Library "String Distance" (Install from [here](http://www.ccpa.puc-rio.br/software/stringdistance/) and place the resulting library file 'stringdistance.so' in the CoppeliaSim installation folder)
- Python 2.7 or newer

## Run the Example
### Preparations
After downloading the repository, you need to set some file paths in CoppeliaSim (using relative paths in CoppeliaSim is somewhat error-prone, so you should set absolute paths). Open the simulation model 'simulation.ttt'. You will see a hierarchy of objects on the left. Click on the text symbol besides the object "SearchAlgorithm". This will open the script which controls the simulation. The comments in the script will direct you to set the appropriate paths.

### Create Action Sequences
We use a finite state machine (FSM) to determine which action sequences of the human worker are feasible:
<img src="https://user-images.githubusercontent.com/56551323/139908780-be75d364-0a08-4130-b7fb-cffe9d959284.png" alt="drawing" width="800"/>

### Search for Hazards
