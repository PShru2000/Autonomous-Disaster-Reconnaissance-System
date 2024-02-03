# Autonomous System for Disaster Response: Navigating and Mapping Hazardous Environments

## Objective 

The goal of this project is to design and implement a complete autonomous system to perform reconnaissance in a simulated disaster environment

1. **Environment Mapping:** Autonomously generate a detailed occupancy grid map of the unknown environment, aiding in the visualization of the area and planning of safe navigation paths.

2. **Victim Location:** Detect simulated victims represented by AprilTags within the environment, providing their ID numbers and precise locations relative to the map.


## Installation

- Ubuntu
- Python
- ROS

## Package Installations

- GMapping
- Cartographer
- explore_lite
- apriltag_ros

## Process

1. **Deploying the Robot:** Place the robot in the unknown environment where it's set to perform the reconnaissance mission.

2. **SLAM with gmapping:** Initiated SLAM using the **gmapping** package to create a real-time map of the environment while simultaneously tracking the robot's position.

3. **Autonomous Exploration:** Implemented the **explore_lite** package for autonomous navigation, guiding the robot to systematically explore the unknown environment using a greedy frontier-based technique.

4. **Map Generation:** Utilized the **explore_lite** package throughout the exploration to continuously update and complete the occupancy grid map of the environment.

5. **AprilTags Detection:** Deployed the **apriltag_ros** package to detect AprilTags within the environment, interpreting them as simulated victims, and recorded their global poses.

6. **Final Task:** Concluded the search and mapping operation once the robot has traversed the entire environment and all AprilTags have been detected and logged.


## Extension: Integrating Cartographer for Enhanced SLAM and AprilTags Detection

To enhance the SLAM accuracy and reliability, I integrated the Cartographer package, leveraging multi-sensor fusion from LIDAR, IMU, and cameras. This approach improved AprilTags detection and tracking by facilitating robust loop closure, crucial for precise robot localization and orientation in complex environments.

## Conclusion

### Conclusion Summary

The project aimed to autonomously map an environment and detect AprilTags, initially utilizing gmapping and explore_lite with a TurtleBot. Initial attempts mapped the environment successfully but detected only five of seven AprilTags due to limitations in LIDAR settings and field of view. To overcome these challenges, I integrated the Cartographer package, leveraging multi-sensor fusion for enhanced accuracy and reliability in SLAM and AprilTags detection. This enhancement fulfilled our objectives by generating a comprehensive environmental map and ensuring all AprilTags are accurately detected, demonstrating significant progress in our autonomous system's development.
