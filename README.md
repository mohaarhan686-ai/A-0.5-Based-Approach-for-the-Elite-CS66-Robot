# Step 02 – Robotic Hardware Fundamentals and ROS 2 Integration

![Robotics](https://img.shields.io/badge/Domain-Robotics-blue)
![Learning](https://img.shields.io/badge/Level-Beginner%20to%20Intermediate-green)
![Focus](https://img.shields.io/badge/Focus-Hardware%20%7C%20Perception%20%7C%20ROS2-orange)

## 1. Introduction

Robotic manipulation requires the integration of mechanical hardware, sensors, actuators and software systems. A robot must understand its surroundings, identify objects, calculate movements and execute physical actions with appropriate accuracy.

This module focuses on understanding the fundamental hardware and software components of an autonomous robotic manipulation system.

The system studied in this module consists of:

1. **Elite Robots CS66:** Six-axis collaborative robotic arm.
2. **Robotiq 2F-85:** Adaptive two-finger gripper.
3. **Intel RealSense D405 and D435i:** RGB-D vision cameras.
4. **ROS 2:** Robotics software communication and integration framework.

The objective is to understand the individual functions of these components and how they work together to perform manipulation tasks.

### Learning Objectives

- Understand the mechanical structure and working principle of a six-axis robotic arm.
- Study payload, reach, degrees of freedom and repeatability.
- Understand adaptive parallel-jaw gripping mechanisms.
- Learn the difference between RGB images, depth images and point clouds.
- Understand the purpose of multiple camera viewpoints.
- Learn ROS 2 communication concepts.
- Understand the role of robot drivers and hardware controllers.
- Develop a basic understanding of the complete robotic manipulation architecture.

---

# 2. Robotic Arm – Elite Robots CS66

## 2.1 Introduction

The Elite Robots CS66 is a six-axis collaborative robotic arm designed for industrial automation, material handling, assembly and robotic manipulation applications.

A robotic arm consists of interconnected mechanical links and joints. The joints provide the movement required to position and orient the end-effector.

In a six-axis robotic arm, six independently controlled rotary joints work together to provide movement in three-dimensional space.

The robot's end-effector can be equipped with different tools, such as:

- Parallel-jaw grippers
- Vacuum grippers
- Welding tools
- Assembly tools
- Inspection equipment

For manipulation applications, a gripper is commonly attached to the robot's flange.

## 2.2 Understanding Six Degrees of Freedom

A rigid object in three-dimensional space has six degrees of freedom:

**Three translational movements:**

| Movement | Description |
|---|---|
| X-axis | Forward and backward |
| Y-axis | Left and right |
| Z-axis | Up and down |

**Three rotational movements:**

| Rotation | Description |
|---|---|
| Roll | Rotation around the X-axis |
| Pitch | Rotation around the Y-axis |
| Yaw | Rotation around the Z-axis |

A six-axis robotic arm combines the movement of its six joints to achieve the required end-effector position and orientation.

This flexibility is important for tasks such as picking objects from different orientations, inserting components and manipulating objects in restricted spaces.

## 2.3 Important Technical Specifications

| Parameter | Elite CS66 |
|---|---|
| Robot Type | Collaborative robotic arm |
| Degrees of Freedom | 6 |
| Rated Payload | 6 kg |
| Maximum Reach | Approximately 914 mm |
| Repeatability | Verify exact datasheet revision |
| Protection Rating | Verify exact model specification |
| Application | Industrial and collaborative manipulation |

*Note: Specifications must be checked against the official datasheet for the exact robot version.*

## 2.4 Understanding Payload

Payload refers to the rated load that a robot can carry under specified operating conditions.

For a robotic manipulation system, the payload calculation must consider the total mounted and manipulated mass.

For example:

- Robotic gripper
- Camera mounted on the wrist
- Mounting adapters
- Connecting accessories
- Object being manipulated

The combined load must remain within the robot's rated limits.

However, payload alone does not determine whether a robot can perform a particular task. The load's centre of gravity, distance from the flange, wrist torque and robot configuration also affect the permitted operating conditions.

## 2.5 Understanding Reach

Reach represents the maximum distance the robot can access within its working envelope.

The CS66 has a nominal maximum reach of approximately 914 mm.

This is important when designing a workspace because the robot must be able to access:

- Object pickup locations
- Assembly positions
- Storage locations
- Working tables
- Inspection points

Maximum reach does not mean that every position within a circular 914 mm radius is accessible at every orientation.

## 2.6 Understanding Repeatability

Repeatability describes how consistently a robot can return to a previously commanded position.

For example, during repeated pick-and-place operations, the robot should approach the same pickup position consistently.

Repeatability is different from absolute accuracy.

- **Repeatability:** Consistency between repeated movements.
- **Accuracy:** Difference between the commanded position and the actual position.

Both are important in robotic assembly and manipulation.

## 2.7 What is a Collaborative Robot?

A collaborative robot, commonly known as a cobot, is designed for applications where humans and robots may work in a shared workspace.

Collaborative robot applications can use different safety approaches:

1. Safety-rated monitored stop.
2. Hand guiding.
3. Speed and separation monitoring.
4. Power and force limiting.

Speed scaling and force limits may be used as part of a safety strategy.

However, collaborative classification does not automatically make the entire application safe.

A proper risk assessment must consider:

- Robot movement speed
- Applied forces
- Gripper design
- Sharp edges
- Pinch points
- Object weight
- Workspace conditions
- Human interaction

### Practical Understanding

The Elite CS66 provides the mechanical movement required for manipulation.

Its six joints position the attached gripper, while the robot controller manages joint movements and provides feedback about the robot's current state.

**Official Resource:**  
https://www.eliterobots.com/

---

# 3. Robotic Gripper – Robotiq 2F-85

## 3.1 Introduction

A robotic gripper is an end-effector used to hold, grasp and manipulate physical objects.

The Robotiq 2F-85 is an electrically operated adaptive two-finger gripper.

It is designed to handle objects with different geometries and sizes using two moving fingers.

It can be mounted on a compatible robotic arm, including the Elite CS66, subject to the correct mechanical and electrical integration.

## 3.2 Working Principle

The 2F-85 uses two parallel-moving fingers to grasp objects.

During operation:

1. The gripper receives a control command.
2. Its fingers move towards the requested position.
3. The fingers make contact with the object.
4. The gripping mechanism applies the configured force.
5. The object is held for manipulation.
6. The fingers open when the release command is executed.

The gripper supports configurable position, speed and force parameters.

## 3.3 Important Specifications

| Parameter | Specification |
|---|---|
| Model | Robotiq 2F-85 |
| Gripper Type | Adaptive two-finger gripper |
| Number of Fingers | 2 |
| Opening Stroke | 85 mm |
| Gripping Force | 20–235 N |
| Closing Speed | 20–150 mm/s |
| Weight | Approximately 1 kg |

*Values are nominal product specifications. Refer to the official manual for exact operating conditions and revision-specific details.*

## 3.4 Understanding Parallel-Jaw Gripping

In a parallel-jaw gripper, the two fingers move in approximately parallel directions.

This arrangement is suitable for grasping objects between two opposing contact surfaces.

Examples include:

- Cubical blocks
- Rectangular components
- Small containers
- Bottles within the gripper's capacity
- Industrial workpieces

The gripping process depends on the object's dimensions, surface friction, weight and geometry.

## 3.5 Understanding Stroke

Stroke refers to the opening range of the gripper fingers.

The Robotiq 2F-85 has an 85 mm nominal stroke.

This means that the gripper can accommodate objects within its specified gripping geometry and operating range.

The stroke is an important selection parameter when choosing a gripper for different object sizes.

## 3.6 Understanding Gripping Force

Gripping force is the force applied by the gripper fingers when holding an object.

The 2F-85 provides a programmable gripping force range of approximately 20–235 N.

The correct force depends on:

- Object weight
- Surface friction
- Object material
- Object geometry
- Required grasp stability

Excessive force may damage fragile objects, while insufficient force may allow objects to slip.

## 3.7 Gripper Control Parameters

Three important control parameters are:

| Parameter | Function |
|---|---|
| Position | Determines finger opening or closing position |
| Speed | Determines the movement speed of the fingers |
| Force | Determines the gripping force applied |

The gripper may also provide status information, depending on the control interface and integration method.

### Practical Application

During a pick-and-place task:

1. The robot approaches the object.
2. The gripper opens to the required width.
3. The robot aligns its fingers with the object.
4. The gripper closes using the selected force.
5. The robot lifts and moves the object.
6. The gripper opens at the target location.

### Engineering Consideration

The gripper's mass and the manipulated object's mass must be included in the robot's payload calculations.

The gripping force rating is not the same as the maximum object weight that the gripper can safely lift.

**Official Resource:**  
https://robotiq.com/products/adaptive-grippers

---

# 4. Vision System – Intel RealSense D405 and D435i

## 4.1 Introduction

Vision systems allow robots to collect information about their surroundings.

In autonomous manipulation, cameras are used to identify objects, estimate their positions and understand the workspace.

Intel RealSense RGB-D cameras provide colour and depth information.

This information can be processed to estimate the three-dimensional location of objects.

## 4.2 Understanding RGB Images

An RGB image contains three colour channels:

- Red
- Green
- Blue

It provides visual information about the scene.

An RGB image can help a perception model identify:

- Object appearance
- Object colour
- Object boundaries
- Object categories
- Visual features

However, a standard RGB image does not directly provide the actual distance of an object from the camera.

## 4.3 Understanding Depth Images

A depth image provides distance measurements for visible pixels.

Each valid depth measurement represents the estimated distance between the camera and a point in the observed scene.

Depth information helps a robotic system estimate:

- Object distance
- Object height
- Surface geometry
- Relative object position
- Spatial relationships between objects

Depth measurements may contain invalid or noisy values, especially on reflective, transparent or poorly textured surfaces.

## 4.4 Understanding Point Clouds

A point cloud is a collection of three-dimensional points representing the observed environment.

A depth camera uses its depth measurements and camera calibration parameters to estimate 3D coordinates.

Each point can be represented using:

- X coordinate
- Y coordinate
- Z coordinate

Point clouds are useful for:

- 3D object localization
- Workspace reconstruction
- Collision checking
- Surface estimation
- Robotic grasp planning

## 4.5 RealSense D405 vs D435i

The two cameras are designed for different sensing requirements.

| Feature | RealSense D405 | RealSense D435i |
|---|---|---|
| Camera Category | RGB-D | RGB-D |
| Main Application | Close-range perception | Wider workspace perception |
| Typical Published Depth Range | Approximately 7–50 cm | Approximately 30 cm–3 m |
| IMU | No | Yes |
| Suitable Application | Close-up inspection | General scene observation |

Actual depth performance depends on the object surface, lighting, camera configuration and environmental conditions.

## 4.6 Intel RealSense D405

The D405 is intended for close-range depth sensing.

It can be useful when a robot needs detailed information about objects near its end-effector.

Potential applications:

- Close-up object inspection
- Grasp alignment
- Small component handling
- Near-field depth measurement

## 4.7 Intel RealSense D435i

The D435i is designed for wider-scene depth sensing.

It also includes an inertial measurement unit (IMU).

An IMU measures inertial motion information, such as acceleration and angular velocity.

Potential applications:

- Workspace observation
- Object localization
- Scene understanding
- Wider-area depth sensing
- Robotics perception experiments

The IMU can provide additional motion information, but it does not independently determine the absolute position of the camera.

## 4.8 Camera Placement in Robotic Manipulation

Camera placement determines which part of the workspace can be observed.

### A. Wrist-Mounted Camera

A wrist camera is attached near the robotic end-effector.

Its main purpose is to provide close-up visual information during manipulation.

Applications:

- Final grasp alignment
- Object inspection
- Close-range positioning
- Monitoring the gripper approach

### B. Overview Camera

An overview camera is mounted above or around the workspace.

Its purpose is to observe the overall working area.

Applications:

- Detecting multiple objects
- Estimating object positions
- Identifying free workspace
- Understanding the scene layout

### C. Side Camera

A side camera observes the workspace from a different angle.

Applications:

- Estimating object height
- Observing vertical surfaces
- Understanding stacked arrangements
- Reducing visual occlusion

## 4.9 Why Use Multiple Cameras?

A single camera may not provide sufficient visual information for every stage of a manipulation task.

Multiple cameras provide different viewpoints of the same environment.

For example:

- The overview camera identifies the target object.
- The side camera provides additional information about object height.
- The wrist camera provides close-range information during grasping.

Combining these observations can improve the perception system.

However, multi-camera integration introduces additional requirements:

1. Camera calibration.
2. Coordinate-frame transformation.
3. Timestamp synchronization.
4. Data association.
5. Sensor noise management.
6. Computational resource management.

**Important:** More cameras do not automatically guarantee better performance. Their observations must be correctly calibrated, synchronized and processed.

**Official Resource:**  
https://www.intelrealsense.com/

---

# 5. ROS 2 – Robot Operating System 2

## 5.1 Introduction

ROS 2 is an open-source robotics software framework used to develop, integrate and manage robotic applications.

It provides communication mechanisms that allow different software components to exchange information.

A robotic manipulation system may contain several independent components:

- Camera drivers
- Object detection algorithms
- State estimation systems
- Motion planning software
- Robot hardware drivers
- Gripper control interfaces

ROS 2 allows these components to communicate through a distributed architecture.

It is important to understand that ROS 2 is not a traditional operating system. It is a middleware and software framework built for robotics applications.

## 5.2 Understanding ROS 2 Nodes

A node is an independent software process that performs a specific function.

Examples:

| Node | Function |
|---|---|
| Camera Node | Captures and publishes camera data |
| Perception Node | Detects and identifies objects |
| State Estimation Node | Estimates object and robot states |
| Policy Node | Selects the next action |
| Motion Planning Node | Calculates robot trajectories |
| Robot Driver Node | Communicates with the robotic arm |
| Gripper Node | Controls the gripper |

Each node can perform its function independently while exchanging information with other nodes.

## 5.3 Understanding ROS 2 Topics

Topics are used for continuous data communication.

A publisher sends messages to a topic, and one or more subscribers receive those messages.

Example:

A camera node publishes image data to:

`/camera/color/image_raw`

A perception node subscribes to that topic to process the image.

Other examples:

- `/camera/depth/image_rect_raw`
- `/joint_states`
- `/tf`
- `/tf_static`

The exact topic names depend on the robot and camera configuration.

## 5.4 Understanding ROS 2 Services

Services use a request-response communication model.

A client sends a request, and a server provides a response.

Services are suitable for operations that require a quick response rather than continuous feedback.

Example:

A software component requests a configuration change from another node.

## 5.5 Understanding ROS 2 Actions

Actions are designed for longer-running tasks.

They provide:

- Goal submission
- Execution feedback
- Completion result
- Goal cancellation

Example:

A robot receives a goal to move its end-effector to a particular position.

While the movement is running, the action server can provide progress feedback.

## 5.6 Difference Between Node, Topic, Service and Action

| Component | Communication Type | Main Purpose |
|---|---|---|
| Node | Software process | Performs a specific function |
| Topic | Publish/Subscribe | Continuous data exchange |
| Service | Request/Response | Short operations |
| Action | Goal/Feedback/Result | Long-running tasks |

---

# 6. ros2_control – Hardware and Controller Integration

## 6.1 Introduction

`ros2_control` is a ROS 2 framework designed to connect robot hardware with control software.

It provides a standardized structure for managing hardware interfaces and controllers.

In a robotic arm, the control system must communicate with the robot's joints and retrieve their current states.

## 6.2 Main Functions

- Reading joint positions.
- Reading joint velocities.
- Reading available joint effort information.
- Sending joint position commands.
- Sending joint velocity commands.
- Managing hardware interfaces.
- Integrating controllers with robot hardware.

The available interfaces depend on the robot driver and hardware implementation.

## 6.3 Hardware Interface

A hardware interface connects the control framework to the physical robot.

It provides access to the robot's available state and command interfaces.

For example:

**State interfaces:**
- Current joint position.
- Current joint velocity.
- Available effort feedback.

**Command interfaces:**
- Desired joint position.
- Desired joint velocity.
- Other supported control commands.

The exact supported interfaces depend on the hardware driver.

## 6.4 Why is ros2_control Important?

Without a suitable hardware integration layer, different robotic hardware systems may require completely different control implementations.

`ros2_control` provides a common framework that makes it easier to integrate supported hardware with ROS 2 controllers.

It also separates the control logic from the hardware-specific communication implementation.

**Official Documentation:**  
https://control.ros.org/

---

# 7. Elite Robots CS66 – ROS 2 Driver Integration

## 7.1 Introduction

Elite Robots provides a ROS 2 driver repository for its CS-series robotic arms.

The driver enables integration between ROS 2 applications and compatible Elite robotic hardware.

The repository includes driver packages and robot-specific configurations.

It also provides integration resources for simulation and motion planning.

## 7.2 Basic Integration Requirements

Before connecting a physical robot, the following requirements must be considered:

- Compatible Ubuntu and ROS 2 environment.
- Correct Elite Robots driver version.
- Robot network configuration.
- Correct robot model configuration.
- Robot-side ExternalControl program.
- Required controller configuration.
- Appropriate safety procedures.

The exact installation and launch instructions must follow the official repository for the selected software version.

## 7.3 Understanding ExternalControl

ExternalControl is used in the Elite robot-side integration workflow.

The robot must be configured to accept external control through the required communication interface.

In a typical integration workflow:

1. Configure the robot's network.
2. Prepare the required ExternalControl program.
3. Start the appropriate ROS 2 driver.
4. Establish communication between the robot and ROS 2 system.
5. Verify joint-state feedback.
6. Confirm the robot is ready for controlled operation.

The exact procedure varies with the driver version and robot controller configuration.

## 7.4 Official Driver Repository

Elite Robots CS ROS 2 Driver:

https://github.com/Elite-Robots/Elite_Robots_CS_ROS2_Driver

This repository should be treated as the primary reference for installation, configuration and compatibility.

---

# 8. Complete Robotic Manipulation Architecture

The main objective of this module is to understand how the hardware and software components work together.

A robotic manipulation system can be divided into five major layers.

## 8.1 Layer 1 – Visual Sensing

The camera subsystem captures information about the environment.

Inputs:

- RGB images
- Depth images
- Camera calibration information

Output:

Visual information about the workspace and surrounding objects.

## 8.2 Layer 2 – Perception and State Estimation

The perception system processes the camera information.

Its functions may include:

- Object detection
- Object classification
- Object localization
- Depth processing
- 3D position estimation

The state estimation system can combine perception results with robot feedback to represent the current state of the environment.

## 8.3 Layer 3 – Decision Making

The decision-making system determines what action the robot should perform.

Depending on the application, this can use:

- Rule-based planning
- Classical motion planning
- Machine learning
- Reinforcement learning
- Vision-language-action models

The output may be a target pose, motion command or higher-level task instruction.

## 8.4 Layer 4 – Motion Planning and Control

The selected action must be converted into feasible robot movement.

This layer may include:

- Inverse kinematics
- Trajectory generation
- Collision checking
- Joint control
- Gripper commands
- Safety constraints

MoveIt 2 can be used for motion planning and manipulation, while suitable controllers and robot drivers handle execution.

## 8.5 Layer 5 – Physical Execution and Feedback

The robotic arm performs the movement.

The gripper interacts with the object.

Feedback from available sensors and the robot controller is used to monitor execution.

The system can then update its state and determine the next action.

## 8.6 System Architecture Diagram

```text
                ENVIRONMENT
                     |
                     v
             RGB-D CAMERAS
              D405 / D435i
                     |
                     v
              VISUAL DATA
              RGB + DEPTH
                     |
                     v
           PERCEPTION SYSTEM
          Object Detection
          Object Localization
          Depth Processing
                     |
                     v
            STATE ESTIMATION
          Object Position
          Robot Joint State
                     |
                     v
          DECISION-MAKING MODEL
           Policy / Task Planner
                     |
                     v
             MOTION PLANNING
              MoveIt 2
                     |
                     v
               ROS 2 CONTROL
                     |
             +-------+-------+
             |               |
             v               v
         ELITE CS66      ROBOTIQ 2F-85
         ROBOT ARM          GRIPPER
             |               |
             +-------+-------+
                     |
                     v
             PHYSICAL ACTION
             Object Manipulation
                     |
                     v
              SENSOR FEEDBACK
                     |
                     +----------> STATE UPDATE
```

---

# 9. Example – Robotic Pick-and-Place Operation

A pick-and-place task is a basic robotic manipulation operation.

It involves identifying an object, approaching it, grasping it, transporting it and placing it at a target location.

## Step 1 – Scene Observation

The RealSense camera captures RGB and depth information.

The system observes the workspace and identifies the target object.

## Step 2 – Object Localization

The perception system estimates the object's position.

Depth information helps convert visual observations into spatial information.

The estimated position must be transformed into the robot's reference coordinate frame.

## Step 3 – Action Selection

The task planner or learned policy determines the next operation.

For example:

- Approach the object.
- Align the gripper.
- Close the fingers.
- Lift the object.
- Move to the destination.

## Step 4 – Motion Planning

The motion planning system calculates a feasible trajectory.

It must consider:

- Robot joint limits
- Workspace boundaries
- Obstacle avoidance
- End-effector orientation
- Collision constraints

## Step 5 – Grasping

The gripper opens to the required width.

The robot positions the gripper around the object.

The fingers close using an appropriate force setting.

## Step 6 – Object Transportation

The robotic arm moves the object towards the target location.

Joint feedback and available gripper information can be monitored during execution.

## Step 7 – Object Release

The robot reaches the target location.

The gripper opens and releases the object.

## Step 8 – Verification

The vision system can inspect the resulting scene to determine whether the object was placed successfully.

This creates a feedback-based manipulation process rather than relying only on predefined movement commands.

---

# 10. Engineering Challenges and Important Considerations

Although the hardware components provide the required capabilities, successful integration involves several engineering challenges.

| Challenge | Explanation |
|---|---|
| Camera Calibration | Camera coordinates must be related correctly to robot coordinates. |
| Coordinate Transformation | Object positions must be converted into the appropriate robot reference frame. |
| Sensor Synchronization | Multiple cameras should provide appropriately synchronized observations. |
| Payload Management | The combined mass and load distribution must remain within the robot's limits. |
| Gripper Selection | The gripping force and finger opening must suit the object. |
| Motion Planning | Robot movements must respect joint and collision constraints. |
| Communication | ROS 2 and the hardware driver must communicate reliably. |
| Safety | Robot speed, force, workspace and human interaction must be assessed. |
| Perception Errors | Incorrect object localization can lead to failed manipulation. |

## 10.1 Camera-to-Robot Calibration

A camera measures the environment from its own coordinate frame.

The robot operates using its own coordinate frames.

Therefore, the system needs calibration and coordinate transformations to relate the detected object position to the robot's working coordinate system.

This is especially important for wrist-mounted cameras, where the camera moves along with the robot.

## 10.2 Simulation and Real-World Differences

A robot may be tested in a simulation environment before deployment.

However, simulated and physical systems can behave differently because of:

- Friction differences
- Mechanical tolerances
- Sensor noise
- Communication delays
- Actuator dynamics
- Object properties

Simulation testing does not eliminate the need for physical validation and safety testing.

---

# 11. Learning Outcomes

After completing this module, the following concepts should be understood:

### Mechanical Hardware

- Six-axis robotic arm structure.
- Degrees of freedom.
- Payload and reach.
- Repeatability and accuracy.
- Collaborative robot safety concepts.

### End-Effector

- Adaptive parallel-jaw gripping.
- Stroke and gripping force.
- Position, speed and force control.
- Gripper integration considerations.

### Vision System

- RGB image processing.
- Depth measurement.
- Point cloud generation.
- RealSense D405 and D435i differences.
- Multi-camera placement and calibration.

### Robotics Software

- ROS 2 architecture.
- Nodes and topics.
- Services and actions.
- ros2_control framework.
- Robot driver integration.
- ExternalControl concept.

### System Integration

- Camera-to-perception communication.
- Object localization.
- Decision-making.
- Motion planning.
- Robot and gripper execution.
- Sensor feedback.

---

# 12. Technical Summary

| Component | Primary Function | Output / Role |
|---|---|---|
| Elite CS66 | Robotic movement | Six-axis arm motion |
| Robotiq 2F-85 | Object grasping | Controlled finger movement |
| RealSense D405 | Close-range perception | RGB and depth data |
| RealSense D435i | Wider-scene perception | RGB, depth and IMU data |
| ROS 2 | Software communication | Node-based integration |
| ros2_control | Hardware and controller integration | State and command interfaces |
| MoveIt 2 | Motion planning | Feasible robot trajectories |
| Perception Model | Visual understanding | Object information |
| Decision-Making Model | Action selection | Target actions or commands |

---

# 13. Conclusion

This module establishes the hardware and software foundation required to understand autonomous robotic manipulation.

The Elite CS66 provides the mechanical structure and movement capabilities. The Robotiq 2F-85 performs object grasping. Intel RealSense cameras provide visual and depth information about the working environment.

ROS 2 connects these components through a distributed software architecture, while motion planning and control systems convert high-level tasks into executable robot movements.

The most important understanding is that robotic manipulation is not performed by a single component. It requires coordinated operation between mechanical hardware, perception, decision-making, motion planning, control and feedback.

This foundation is essential before moving towards advanced topics such as reinforcement learning, autonomous manipulation, simulation-based training and real-world deployment.

---

# 14. References and Official Documentation

### Robotic Arm
- [Elite Robots – Official Website](https://www.eliterobots.com/)
- [Elite Robots CS ROS 2 Driver – GitHub](https://github.com/Elite-Robots/Elite_Robots_CS_ROS2_Driver)

### Gripper
- [Robotiq – Adaptive Grippers](https://robotiq.com/products/adaptive-grippers)

### Vision System
- [Intel RealSense – Official Website](https://www.intelrealsense.com/)

### ROS 2
- [ROS 2 Documentation](https://docs.ros.org/)
- [ROS 2 Concepts](https://docs.ros.org/en/rolling/Concepts/Basic.html)
- [ros2_control Documentation](https://control.ros.org/)
- [MoveIt 2 Documentation](https://moveit.picknik.ai/)

---

## Module Information

| Field | Details |
|---|---|
| Module | Step 02 |
| Title | Robotic Hardware Fundamentals and ROS 2 Integration |
| Domain | Robotics and Autonomous Systems |
| Main Hardware | Elite CS66, Robotiq 2F-85 |
| Vision Hardware | Intel RealSense D405 / D435i |
| Software Framework | ROS 2 |
| Learning Duration | 3–4 Hours |
| Module Status | Conceptual Study and Technical Analysis |

**Next Learning Stage:** Understanding robotic manipulation pipelines, perception-to-action systems and reinforcement learning fundamentals.
