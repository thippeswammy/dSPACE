# Car Vehicle Feature Simulation Model for dSPACE SCALEXIO HIL

## Overview

This Simulink model simulates various features of a car for a Hardware-in-the-Loop (HIL) testing environment using the dSPACE SCALEXIO system. The model includes controls for ignition, gearbox, acceleration, braking, steering angle, indicators, and hand brake functionality. The HIL setup enables real-time simulation and communication between the Simulink model and Arduino Uno, which interfaces with the physical output components (e.g., servos, LEDs). The model is configured for use in ConfigurationDesk and ControlDesk, allowing seamless input manipulation and output monitoring.

## Project Structure

- **Simulink Model**: Contains subsystems for each car feature.
- **ConfigurationDesk Setup**: Configures I/O channels for the dSPACE SCALEXIO and Simulink interface.
- **ControlDesk Layout**: Provides a GUI for live input/output monitoring and control.
- **Arduino Interface**: Communicates with the dSPACE SCALEXIO system to control physical components.
- **Signal Generation Basics**: All the basics of signal generation are provided in the .docx file available in the [GitHub repository](https://github.com/thippeswammy/dSPACE/tree/main/dSPACE_Basics).


## System Requirements

- **Software**:
  - MATLAB/Simulink
  - dSPACE ConfigurationDesk and ControlDesk
- **Hardware**:
  - dSPACE SCALEXIO HIL System
  - Arduino Uno
  - Servo Motors, LEDs, and other required components

## Model Features and Specifications

### Inputs and Outputs

| Feature          | Input Range                | Output                  | Description                                                               |
|------------------|----------------------------|-------------------------|---------------------------------------------------------------------------|
| Ignition ON/OFF  | `0` (OFF) / `1` (ON)       | `0` or `5V`            | Controls the power state of the vehicle.                                 |
| Gearbox          | `0-341`, `341-682`, `682-1023` | `-1` (Reverse), `0` (Neutral), `1` (Forward) | Defines the gear position.                       |
| Acceleration     | `0-1023`                   | `0-100` (Speed Value)   | Controls the speed based on acceleration input.                           |
| Car Brake        | `0-1023`                   | `0` if input < 200      | Engages brakes when input is within threshold.                            |
| Hand Brake       | `0` (OFF) / `1` (ON)       | Warning Light, Speed Reduction | Activates hand brake light and reduces speed.   |
| Steering Angle   | `0-1025`                   | `-27.8 to 27.8` degrees | Controls steering servo based on angle input.                             |
| Indicator        | `0-341`, `341-682`, `682-1023` | Left, Null, Right     | Activates corresponding indicator lights with steering behavior.          |

### Functional Description

1. **Ignition**: Toggles vehicle’s ON/OFF state, driving a digital output for voltage control (0V for OFF, 5V for ON).
2. **Gearbox**: Reads input values to set vehicle gear (Reverse, Neutral, Forward) using specified ranges and outputs.
3. **Acceleration**: Scales input to match a 0-100 speed output, with the range between 0-1023 for smooth acceleration.
4. **Car Brake**: If the input value is below 200, braking is engaged, reducing the speed to zero.
5. **Hand Brake**: When engaged, triggers a warning light and gradually decreases vehicle speed.
6. **Steering Angle**: Converts input into angle output for servo motor control, with a range of -27.8 to 27.8 degrees.
7. **Indicators**: Responds to directional input to turn left or right indicators ON/OFF, with real-time behavior integration.

## Implementation and Configuration Steps

### 1. Simulink Model Development

   - Use blocks to model each subsystem representing vehicle features.
   - Define input ranges, output signals, and conversion logic.
   - Integrate signal processing and control algorithms based on specified input-output requirements.

### 2. dSPACE ConfigurationDesk Setup

   - Configure SCALEXIO I/O channels and link the Simulink model inputs/outputs with dSPACE I/O pins.
   - Use I/O mapping to control signal communication with the Arduino.

### 3. ControlDesk Interface

   - Set up a custom ControlDesk layout for real-time input manipulation and output monitoring.
   - Define parameters for each feature to allow controlled testing.

### 4. Arduino Uno Integration

   - Connect Arduino Uno to dSPACE SCALEXIO via appropriate communication ports.
   - Program the Arduino to read inputs from dSPACE and control physical components (servos, LEDs).

## Testing and Validation

1. **Simulink Simulation**: Test the model in Simulink to validate each feature’s behavior and interactions.
2. **HIL Testing**: Connect to the dSPACE SCALEXIO system, then use ConfigurationDesk and ControlDesk to monitor and modify inputs.
3. **Arduino Verification**: Verify that the Arduino correctly interprets signals from dSPACE and activates physical components accordingly.

## Troubleshooting

- **Model not responding**: Check connections between dSPACE and Arduino, verify channel mappings in ConfigurationDesk.
- **Signal delay**: Adjust sample times in Simulink model and ConfigurationDesk settings.
- **Incorrect outputs**: Ensure signal ranges match specified input-output mappings.

## Additional Notes

- Ensure Arduino sketch is correctly configured to interpret the signal range and control outputs based on the model.
- Regularly save and version control the Simulink model and ConfigurationDesk setup to track changes.


