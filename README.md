# Mobile Manipulator Kinematics and PID Control

A MATLAB-based simulation of a mobile manipulator consisting of a differential-drive mobile base and a two-link robotic arm. The project explores forward kinematics, end-effector motion, Jacobian-based velocity mapping, and task-space PID control for Cartesian position tracking.

## Project Overview

The project was developed in two stages:

### 1. Mobile Manipulator Modelling and 3D Simulation

- Modelled a differential-drive mobile robot with a two-link robotic arm.
- Derived and implemented mobile base kinematics.
- Implemented forward kinematics to calculate joint and end-effector positions.
- Simulated base and manipulator motion in MATLAB.
- Visualised the robot configuration and end-effector trajectory in 3D.

### 2. Task-Space PID Control

- Implemented PID control for end-effector position tracking in Cartesian space.
- Derived a 2 × 4 Jacobian relating end-effector velocity to wheel and joint velocities.
- Used the damped Jacobian pseudoinverse to calculate control inputs.
- Implemented control input saturation and integral anti-windup.
- Visualised tracking error, end-effector trajectory and control signals.

## System Architecture

The mobile manipulator consists of:

- Differential-drive mobile base.
- Two-link robotic arm.
- Four control inputs:
  - Right wheel angular velocity (ωr)
  - Left wheel angular velocity (ωl)
  - First joint angular velocity (θ̇1)
  - Second joint angular velocity (θ̇2)

## Kinematic Model

### Mobile Base Kinematics

The linear and angular velocities of the differential-drive base are:

v = (r/2)(ωr + ωl)

ω = (r/L)(ωr - ωl)

### Forward Kinematics

The end-effector position is calculated using:

xe = x + l1 cos(θ + θ1) + l2 cos(θ + θ1 + θ2)

ye = y + l1 sin(θ + θ1) + l2 sin(θ + θ1 + θ2)

### Jacobian-Based Velocity Mapping

The end-effector velocity is related to the control inputs through:

[xe_dot; ye_dot] = J [ωr; ωl; θ1_dot; θ2_dot]

A damped pseudoinverse is used to obtain the control inputs:

u = Jᵀ(JJᵀ + λI)⁻¹v_cmd

This helps improve numerical stability near kinematic singularities.

## PID Controller

The task-space PID controller calculates the desired Cartesian velocity based on the end-effector position error.

- Proportional control for position error.
- Integral control for accumulated error.
- Derivative control for error-rate damping.
- Velocity saturation to constrain commanded motion.
- Integral clamping to reduce integral windup.

## Simulation Parameters

| Parameter | Value |
|---|---:|
| Wheel radius | 0.05 m |
| Wheel separation | 0.3 m |
| Link 1 length | 1.0 m |
| Link 2 length | 0.9 m |
| PID Kp | 3.0 |
| PID Ki | 0.05 |
| PID Kd | 0.8 |
| Simulation duration (PID) | 60 s |
| Time step (PID) | 0.1 s |

## Technologies Used

- MATLAB
- Robotics and Control Systems
- Differential-Drive Kinematics
- Forward Kinematics
- Jacobian-Based Control
- PID Control
- Numerical Simulation

## Repository Structure

```text
Mobile-Manipulator-Kinematics-and-PID-Control/
│
├── Mobile_Manipulator_3D.m
├── PID_Controller.m
├── README.md
└── screenshots/
    ├── 3d_simulation.png
    ├── trajectory.png
    ├── tracking_error.png
    └── control_inputs.png
```

## How to Run

1. Clone or download this repository.
2. Open MATLAB.
3. Navigate to the project directory.
4. Run the modelling simulation:

```matlab
run('Mobile_Manipulator_3D.m')
```

5. Run the PID-controlled simulation:

```matlab
run('PID_Controller.m')
```

## Future Improvements

- Integration with ROS 2.
- Implementation of inverse kinematics.
- Obstacle avoidance and path planning.
- Dynamic modelling and actuator constraints.
- Simulation with a physics-based robotics environment.
- Extension to real-time robotic hardware.

## Author

**Anshul Pareek**

B.Tech – Electrical Engineering (Rail Engineering)  
Gati Shakti Vishwavidyalaya

- GitHub: https://github.com/AnshulPareek
- LinkedIn: https://linkedin.com/in/anshulpareek54

## Disclaimer

This project focuses on mathematical modelling and MATLAB-based simulation. It does not represent physical hardware deployment or real-world experimental validation.
