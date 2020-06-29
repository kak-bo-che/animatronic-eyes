# Eyes robot
This project is an experimental platform to utilize the raspberry pi as a host for ROS and have the eyes robot controlled via various input mechanisms.
* bluetooth joystick to manually controll the eye movement 
* automated prerecorded movement files played back randomly to give the robot a personality while it is waiting for input
* face tracking via the raspberry pi camera that will direct the eye movement to follow faces (this updates only a few times a second so results in jerky movement)

## Design
Almost everything in the project is relying on drop in ROS packages instead of writing custom software. The only custom bits written are:
* replay bag files for the autonomous random movement (eyes reveries)
* translation from the face detection to the coordinatres for the eyes (eyes-follower).
Everything else is configuration of the following existing ROS modules:
* modified [ros-pca9685-board](https://github.com/kak-bo-che/ros-pca9685-board/tree/feature/eyes-project)
* joy
* teleop_twist_joy
* topic_tools/relay
* opencv_apps/face_detection
* raspicam_node
Getting things going...
* You have to hold the deadman's switch to get the joystick to work 
  - in the currently setup it is the right trigger

## Bluetooth Joystick
Most a pain in ass currently it needs to be automated better on boot
```
#!/bin/bash
bluetoothctl -- connect 28:9A:4B:00:0F:AE
```