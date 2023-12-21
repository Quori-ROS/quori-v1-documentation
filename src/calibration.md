# Calibration

<!-- TODO: fix link to spreadsheet -->
Calibration values for your robot can be found here Spreadsheet. See below for instructions on how to program each microcontroller. You should not need to recalibrate your robot. If you need to recalibrate your robot, likely due to a significant hardware modification or repair, see the steps below.

## Arm

You will need to set the zero position for the two sensors in each arm. This is done in the calibration configuration where the joints should read zero.

The arm should be straight out and the abduction axis of the shoulder joint facing forward. The part of the shoulder 3d printed piece with the sensor should be closest to the back for the right arm while for the left arm should be calibrated with the sensor face closest to the front of the robot. The two images of the left and right arms almost in calibration (the abduction is not zeroed since it is not perpendicular to the module as with the left most animation image), that is, the proper alignment in one axis for each showing how the sensor should be parallel to different faces depending on while arm you are working with.

Below, the target calibration position:

![Calibration position](images/quori_arm_alignment.png)

Right arm sensor alignment example:

![Right arm sensor alignment example](images/quori_arm_sensor.png)

Left arm sensor alignment example:

![Left arm sensor alignment example](images/quori_arm_sensor_2.png)

Flash the microcontroller for the arm you are calibrating with the code as instructed from [`quori_embedded`](https://github.com/Quori-ROS/quori_embedded); however, you will set the `ARM_ZERO_POSITION` variables in calibration.hpp to zero for the arm you are calibrating.

Next launch the controller file in quori_ros. You should now be able to view the sensor’s value by using rostopic echo to see the joint’s state. Use these value for their corresponding `ARM_ZERO_POSITION` variables. You can now flash the microcontroller with the update calibration. Verify the calibration was successful by reading the joint’s position in the zero configuration. The position should be reported as something close to zero.

## Waist

The waist has two sensors to calibrate. The raw value of each sensor is not displayed and so it is a bit more difficult to calibrate this. While there may be an easier option, here is one option for how to recalibrate the waist.

Each sensor for the waist is calibrated with the torso upright in its zero configuration.
The calibration value for the waist can be found by flashing the waist code from [`quori_embedded`](https://github.com/Quori-ROS/quori_embedded) with the `QUORI_CONFIG_ZERO_POSITION_WAIST` values as `0`.
You can then echo the joint’s state to get the proper calibration value for the waist.

For the QUORI_CONFIG_ZERO_POSITION_MOTOR, you will need to change the line with

```cpp
states.measured[0] = -state->waist[0];//state->measured[0];
```

To

```cpp
states.measured[0] = state->measured[0];
```

When you echo the joint’s position you will now be reading the motor position. Use this value for `QUORI_CONFIG_ZERO_POSITION_MOTOR`

Be sure to change the code back to its original state with

```cpp
states.measured[0] = -state->waist[0];//state->measured[0];
```

## Base

The base calibration does not require the microcontroller to be flashed. The calibration value is stored in `src/quori_controller/config/calibration.yaml`. To find the value to use for calibration set the value in the calibration file to `0`. Then:

- `roslaunch quori_controller quori_control_holo.launch`
- `roslaunch quori_teleop quori_teleop.launch`
- Hold the left bumper LB and use the thumbsticks to rotate the top plate of the base into your desired zero heading. [See teleop repo](https://www.google.com/url?q=https://github.com/Quori-ROS/quori_ros/tree/master/src/quori_teleop&sa=D&source=editors&ust=1703158334603099&usg=AOvVaw0ti8R1g06ZxG_J2iSaMmy2) for more information on how to command the robot
- `rostopic echo /quori/base/pos_status`
- Use the value reported in the echo above as the new calibration value in the calibration file