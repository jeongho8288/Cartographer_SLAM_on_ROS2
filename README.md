# Cartographer_SLAM_on_ROS2

> The Storapy (mobile robot) and Xarm-lite6 are provided by company XYZ .

Tested environment
```
Ubuntu 22.04
ROS2-humble
python 3.10.11
```

This project aims to design an algorithm that plans and follows a path for a vehicle placed at an arbitrary position and orientation in a 2D environment to reach a target point.
<hr style="border-top: 3px solid #bbb;">  

## Path Planning  

### 1. Results  
<img src="https://github.com/user-attachments/assets/ca46bb0c-b40e-48ef-8006-e062758d0a77" alt="Description2" style="width: 70%; height: 300px;">  

### 2. Transformation matrix    
Since the coordinate system used in the map differs from the one used in the vehicle,  
the vehicle's coordinate system is converted to the map's coordinate system to simplify calculations and reduce errors.  
  
### 3. Selection of Next Candidate Nodes  
To ensure smooth vehicle rotation, the next node can only be within a ±30-degree range on both the front and rear sides.  
Four nodes are sampled for both the front and rear, and these nodes are then converted to the map's coordinate system.  
The transformed nodes become the candidate nodes.  
  
### 4. Hueristic Criteria  
Choosing the shortest path is not always the optimal solution, as the path must satisfy constraints on unreasonable rotations and the final yaw.
  
There are 3 main criteria;

&nbsp;&nbsp;&nbsp;&nbsp;i) Distance  
&nbsp;&nbsp;&nbsp;&nbsp;Distance costs follow euclidian method

&nbsp;&nbsp;&nbsp;&nbsp;ii) Error between current yaw and target end yaw.  
&nbsp;&nbsp;&nbsp;&nbsp;The car trys to match the target end yaw.  
&nbsp;&nbsp;&nbsp;&nbsp;This means that car trys to make a path that can go straight to its target point and match the target end yaw.  

&nbsp;&nbsp;&nbsp;&nbsp;iii) Intersection with the straight line to the end position and virtual barrier around goal.  
&nbsp;&nbsp;&nbsp;&nbsp;The virtual barriers are created around the goal where only the entrance is open.  
&nbsp;&nbsp;&nbsp;&nbsp;The car trys to avoid going straight to the goal when there is a collision with the virtual barrier.  

<hr style="border-top: 3px solid #bbb;">  
  
## Path tracking  

### 1. Results  
<img src="https://github.com/user-attachments/assets/3dc48f8c-4cd5-4c5d-bc57-5bc758692e86" alt="Description2" style="width: 90%; height: 280px;">  

### 2. Angle Calculation  
  
### 3. P control
Reference and error can be calculated by yaw with respect to map coordinate system.  
The yaw valuable is a global variable therefore no localization is needed. By using P Control of yaw error,  
the car can be driven to follow the path.  
  
<hr style="border-top: 3px solid #bbb;">  


