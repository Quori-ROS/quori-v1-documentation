# Modular Configurations

You can reconfigure Quori with new modules or use some of its module’s independently. See the [Receiving and Shipping Section](../setup/shipment.md) for instructions on how to attach and remove modules. If you do not use Quori in its default configuration you may need to modify the quori_controller configuration. Here are a few examples to consider:

## Locking the Waist

An optional locking pin feature allows for the torso motion to be locked for shipping or if waist actuation is not desired. You can do this with two torso locking M3 bolts that are 60 mm long. The battery will not fit if these are screwed in too far so you must be careful when inserting these. If you do not use the waist motor remove the 5 Amp fuse near the motor line. See [this video](https://photos.app.goo.gl/qkKNyzurEaRbXw3x9) for reference. Note that there are four options for these locking positions.

## Using the Base Module Independently

You may want to mount your own robot the the base module. The base module has 14 M3 inserts in its mounting plate. See FILE for mounting plate dimensions. To control the base with your own robot you will need to give the base power and ROS to send commands.

For power you will need 12V at atleast 6 Amps to plug into the base’s XT60 cable. For data, you will need to plug the base’s USB cable into a computer running ROS. ROS topics for the base can be found on [the github repository](https://github.com/Quori-ROS/quori_base_embedded).

## Using the Head Module Independently

The head module can be detached from the torso by the four mounting M5 fasteners and the power and HDMI cables. The projector will turn ON if it sees power from its AC power adapter. You can detach the power adapter from the Quori if needed. The projector will automatically select the HDMI input once the projector is connected to a source over HDMI.

## Using the Upper Body Module Independently

The default quori_ros software currently does not support control of the torso without the base module being attached. If you use the Torso without the base be sure to cover the base XT60 connector with a cap or electrical tape to prevent risk of electrical shock and that port shorting. You can modify the `quori_controller` configuration to not register the base. You will need to remove the `base_controller` from `quori_control_holo.yaml` and the base device from the `params.yaml`.

## Swapping out Modules

You may want to use your module on Quori. Please note that any hardware modification will most likely require updating the core ROS software which loads the model of the robot and allows for joint control and feedback.
