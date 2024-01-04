# Testing

The following should be verified after your first assembly to verify no parts were damaged during shipping. You can also use this as a basic test if something is not working.

## Joint Functions

You will need to plug the robot into power and use the e-stop. Be sure the robot is not able to collide with any objects before starting.

### Arms and Waist

- Launch the holonomic controller:

  ```bash
  roslaunch quori_controller quori_control_holo.launch
  ```

- Launch the rqt_trajectory_controller:
  ```bash
  /opt/ros/noetic/lib/rqt_joint_trajectory_controller/rqt_joint_trajectory_controller
  ```
  As a sanity check before you enable control in `rqt` ensure that the arms and waist are reading valid positions (values are within the range of the slider and respond to slight movement)

- Enable control of the joints by pressing the red button in `rqt`.
- Use the slider to move each joint to its extreme position and back to a resting position
- Close out of `rqt` and any ROS nodes

### Base

- Launch the holonomic controller:

  ```bash
  roslaunch quori_controller quori_control_holo.launch
  ```

- Launch the teleop node:

  ```bash
  roslaunch quori_teleop quori_teleop.launch
  ```
  Make sure the USB remote receiver is plugged into Quori (the USB hub on the Quori panel is the recommended location)

- Control the base: hold the left bumper LB and use the thumbsticks to move the robot. See teleop repo for more information

## Testing Sensing Functions

### Camera

- Launch the camera node:
  ```bash
  roslaunch astra_ros default.launch
  ```

- Test that the images are streaming with the following commands.
  The depth image will be difficult to see pixels depending on what the camera is able to see.
  ```bash
  rosrun image_view image_view image:=/astra_ros/devices/default/color/image_color
  ```
  Then close out of this node and run
  ```bash
  rosrun image_view image_view image:=/astra_ros/devices/default/depth/image
  ```

### LIDAR

- Launch the laser scanner node

  ```bash
  roslaunch rplidar_ros rplidar.launch
  ```

  If you are getting an error try unplugging and replugging in the lidar usb cable. You can also see the [Troubleshooting](../troubleshooting.md) section

- Launch the terminal client

  ```bash
  rosrun rplidar_ros rplidarNodeClient
  ```

  If you see numbers streaming on the terminal then the sensor is working

### Microphone

- Launch the sensor’s node(s)

  ```bash
  roslaunch respeaker_ros sample_respeaker.launch
  ```

- Echo a data topic
  ```bash
  rostopic echo /sound_direction
  ```
  If you see data echoing as you make noise around the head of the robot then the sensor is working

## Face

We will test that the calibration image is properly centered. You will need a remote PC with x11 forwarding. `ssh` into Quori and then do the following:

```bash
roslaunch quori_face calibrate.launch
```

You should see a crosshair centered on the robot’s face. You can update hardware calibration with new dx and dy values by using the dynamic reconfigure window that should have appeared on the remote PC (via x11 forwarding). You should not need to update the dx and dy values.

## Navigation Basics

Quori can navigate a map using ROS’s navigation stack. Use a remote laptop to set up a ROS network. The following launch files will get you started.

```bash
roslaunch quori_launch mapping.launch
roslaunch quori_controller quori_control_holo.launch
roslaunch quori_nav move_base.launch # if autonomous otherwise use telop
```

Then run RViz on a remote desktop that is on the same ROS network.

- Load map, laser scanner, and robot model into Rviz
- Use 2d Nav in rviz to move around map
