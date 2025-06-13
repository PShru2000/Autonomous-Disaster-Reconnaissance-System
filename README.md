# Autonomous System for Disaster Response: Navigating and Mapping Hazardous Environments

## Objective 

The goal of this project is to design and implement a complete autonomous system to perform reconnaissance in a simulated disaster environment

1. **Environment Mapping:** Autonomously generate a detailed occupancy grid map of the unknown environment, aiding in the visualization of the area and planning of safe navigation paths.

2. **Victim Location:** Detect simulated victims represented by AprilTags within the environment, providing their ID numbers and precise locations relative to the map.


## Installation

- Ubuntu
- Python
- ROS
- - ROS Packages:
  - `gmapping`
  - `cartographer_ros`
  - `explore_lite`
  - `apriltag_ros`
  - `raspicam_node`

## Step-by-Step Setup Instructions

> These steps are to be followed **on both the TurtleBot3 and the host PC**.

### 1. Network & SSH
Ensure all devices (TurtleBot3 and host PC) are on the **same local network**.

SSH into the TurtleBot:
```bash
ssh ubuntu@<raspberrypi_IP>
````

### 2. Clone the GitHub Repository

Clone your project repo on both the robot and the host PC:

```bash
git clone https://github.com/YourUsername/Disaster-Response-System.git
```

### 3. Launch Required Nodes on the TurtleBot

```bash
export TURTLEBOT3_MODEL=burger
roslaunch turtlebot3_bringup turtlebot3_robot.launch
```

### 4. Start the Raspberry Pi Camera (in a new SSH session)

```bash
roslaunch raspicam_node camerav2_1280x960_10fps.launch enable_raw:=true
```

### 5. Launch SLAM on the Host PC

```bash
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping
```

### 6. Launch AprilTag Detection Node

```bash
roslaunch apriltag_ros continuous_detection.launch
```

### 7. Launch Exploration (Autonomous Navigation)

```bash
roslaunch my_nav exploration.launch
```

### 8. Store AprilTag Global Poses

Run the custom script to compute and log AprilTag global poses:

```bash
rosrun my_nav static_transform.py
```

---

## Process

1. **Deploying the Robot:** Place the robot in the unknown environment where it's set to perform the reconnaissance mission.

2. **SLAM with gmapping:** Initiated SLAM using the **gmapping** package to create a real-time map of the environment while simultaneously tracking the robot's position.

3. **Autonomous Exploration:** Implemented the **explore_lite** package for autonomous navigation, guiding the robot to systematically explore the unknown environment using a greedy frontier-based technique.

4. **Map Generation:** Utilized the **explore_lite** package throughout the exploration to continuously update and complete the occupancy grid map of the environment.

5. **AprilTags Detection:** Deployed the **apriltag_ros** package to detect AprilTags within the environment, interpreting them as simulated victims, and recorded their global poses.

6. **Final Task:** Concluded the search and mapping operation once the robot has traversed the entire environment and all AprilTags have been detected and logged.


## Extension: Integrating Cartographer for Enhanced SLAM and AprilTags Detection

To enhance the SLAM accuracy and reliability, I integrated the Cartographer package, leveraging multi-sensor fusion from LIDAR, IMU, and cameras. This approach improved AprilTags detection and tracking by facilitating robust loop closure, crucial for precise robot localization and orientation in complex environments.

## Results Analysis

### SLAM Performance

* **GMapping:** Enabled basic mapping and navigation but had limitations with loop closure and tag visibility.
* **Cartographer Integration:** Significantly improved map accuracy and AprilTag detection consistency due to sensor fusion from LiDAR, IMU, and camera.

### AprilTags Detection

* **Initial Results (GMapping):** 5/7 tags detected due to field of view and synchronization issues.
* **Enhanced Results (Cartographer):** All 7 tags detected with improved pose estimation and tracking.

### Real-World Testing

* Conducted in indoor environments with obstacles and partial occlusions.
* AprilTags were detected at various heights and orientations.
* Maps were successfully generated and visualized in RViz.

  <table>
  <tr>
    <td><img src="Results/April Tags Detection.png" alt="April Tag Detection" width="300"/></td>
    <td><img src="Results/Base Implementation.png" alt="Base Implementation" width="300"/></td>
    <td><img src="Results/RViz Visualization with April Tag Detection.png" alt="RViz Visualization with April Tag Detection" width="300"/></td>
    <td><img src="Results/Simulated-Final Map generated.png" alt="Simulated-Final Map generated" width="300"/></td>
    <td><img src="Results/Store Tag ID position and orientation.png" alt="Store Tag ID position and orientation" width="300"/></td>
  </tr>
  <tr>
    <td align="center"><b>April Tag Detection</b></td>
    <td align="center"><b>Base Implementation</b></td>
    <td align="center"><b>RViz Visualization with April Tag Detection</b></td>
    <td align="center"><b>Simulated-Final Map generated</b></td>
    <td align="center"><b>Store Tag ID position and orientation</b></td>
  </tr>
</table>


## Conclusion

The project aimed to autonomously map an environment and detect AprilTags, initially utilizing gmapping and explore_lite with a TurtleBot. Initial attempts mapped the environment successfully but detected only five of seven AprilTags due to limitations in LIDAR settings and field of view. To overcome these challenges, I integrated the Cartographer package, leveraging multi-sensor fusion for enhanced accuracy and reliability in SLAM and AprilTags detection. This enhancement fulfilled our objectives by generating a comprehensive environmental map and ensuring all AprilTags are accurately detected, demonstrating significant progress in our autonomous system's development.
