# Project Submission format
## 1. Create a Repository on GitHub

Follow these steps to create a repository on GitHub:

1. Go to [GitHub](https://github.com/).
2. Sign in with your credentials (or [create an account](https://github.com/join) if you don't have one).
3. Click on the `+` icon in the upper right corner and select **New repository**.
4. Name your repository (e.g., `C_Electronics_Project`).
5. Add a description (optional).
6. Choose the repository type:
    - **Public**: Anyone can see it.
    - **Private**: Only collaborators can see it.
7. Initialize the repository by checking the "Add a README file" box.
8. Click **Create repository**.

---

## 2. Add Collaborators

To add collaborators to your repository:

1. Go to your repository’s page.
2. Click on the **Settings** tab.
3. In the left-hand sidebar, click **Collaborators and Teams**.
4. In the "Collaborators" section, enter the GitHub usernames or email addresses of the people you want to add as collaborators.
5. Click **Add Collaborator**.
6. Each collaborator will receive an invitation to collaborate on your project. They need to accept it.

---

By following these steps, you'll be able to set up your project repository and work with collaborators on GitHub!

# Passenger-Side Power Window System - Project Requirements

## 1. High-Level Requirements (HLR)
The following high-level requirements describe the functionality expected from the passenger-side power window system:

1. **Window Control**  
   The passenger should be able to operate the power window (up and down) using a switch located on the passenger door.

2. **Auto-Down Feature**  
   The window should automatically roll down completely when the passenger presses and holds the switch for more than 2 seconds.

3. **Obstacle Detection (Anti-Pinch)**  
   The window should stop and reverse its movement if an obstacle is detected during the upward motion.

4. **Child Lock Functionality**  
   When the child lock is activated from the driver's side, the passenger should not be able to operate their window.

5. **Ignition Lockout**  
   The window should only be operational when the vehicle’s ignition is on or within 30 seconds after the ignition is turned off.

6. **Manual Override**  
   In the event of system failure, the window should have a manual override option for emergency operation.

---

## 2. Low-Level Requirements (LLR)
The following low-level requirements detail how the high-level requirements will be technically implemented:

### 2.1 Motor Control
- The motor should receive commands from the microcontroller based on the input from the passenger’s window switch.
- PWM (Pulse Width Modulation) should be used to control the motor's speed for smooth operation.

### 2.2 Switch Interface
- The passenger window switch should have two states: up and down.
- The microcontroller should detect the switch position (pressed or released) and send appropriate commands to the motor driver.

### 2.3 Obstacle Detection
- A current sensor should be integrated with the motor driver to detect any significant increase in motor current, signaling an obstacle in the window path.
- When an obstacle is detected, the control algorithm should reverse the motor direction within 200ms to prevent injury or damage.

### 2.4 Communication with Driver’s Control Unit
- The passenger window switch must send signals via the CAN bus to the driver’s control unit to determine whether the child lock feature is active.

### 2.5 Power Management
- When the vehicle ignition is turned off, the passenger window system should remain powered for 30 seconds, then enter a low-power sleep mode.

### 2.6 Safety Features
- The system should have overcurrent protection to prevent damage to the motor during operation.

---

## 3. Non-Functional Requirements (NFR)
Non-functional requirements define the overall quality attributes of the system, such as performance, reliability, and hardware/software specifications:

### 3.1 Hardware Requirements
- **Microcontroller**:  
  - 8-bit or 16-bit microcontroller with CAN bus support for communication.
  - Minimum of 2 PWM channels for motor control.
  
- **Motor**:  
  - DC motor capable of handling variable loads with feedback from current sensors.

- **Sensors**:  
  - Current sensor to monitor motor load for obstacle detection.  
  - Optional temperature sensor to prevent motor overheating.

- **Switches**:  
  - Durable, automotive-grade window switches with tactile feedback.

### 3.2 Software Requirements
- **Control Algorithm**:  
  - The software should have a real-time operating system (RTOS) or time-sensitive task scheduler to handle window control inputs, motor control, and sensor monitoring in a deterministic manner.

- **Safety & Redundancy**:  
  - The software should implement debouncing for switch inputs to prevent false readings.  
  - Anti-pinch logic should be embedded in the software to ensure the window reverses when an obstacle is detected.

- **CAN Bus Communication**:  
  - The software should be able to exchange data with the driver’s control unit via the CAN bus to handle child lock status, power state, and control signals.

- **Diagnostics**:  
  - Self-diagnostic routines should be built in to check the motor’s health, sensor functionality, and communication integrity at regular intervals.

---

## 4. Conclusion
This document outlines the high-level, low-level, and non-functional requirements for the passenger-side power window system. 
