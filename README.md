### **NOTE**: [Original ROS teleoperation package](https://github.com/ros-teleop/teleop_twist_keyboard) is modified to work with [AirSim](https://microsoft.github.io/AirSim/airsim_ros_pkgs/)


# teleop_twist_keyboard_airsim
Generic Keyboard Teleop for AirSim ROS

# Launch
Run.
```
rosrun teleop_twist_keyboard_airsim teleop_twist_keyboard_airsim.py
```

With custom values.
```
rosrun teleop_twist_keyboard_airsim teleop_twist_keyboard_airsim.py _speed:=0.9 _turn:=0.8
```

Publishing to a different topic (in this case `my_cmd_vel`).
```
rosrun teleop_twist_keyboard_airsim teleop_twist_keyboard_airsim.py /airsim_node/SimpleFlight/vel_cmd_body_frame:=my_cmd_vel
```

For example, if you are using PX4 Multirotor, teleoperate like this:
```
rosrun teleop_twist_keyboard_airsim teleop_twist_keyboard_airsim.py /airsim_node/SimpleFlight/vel_cmd_body_frame:=/airsim_node/PX4/vel_cmd_body_frame
```

# Usage
```
Reading from the keyboard  and Publishing to Twist!
---------------------------
Moving around:
   u    i    o
   j    k    l
   m    ,    .

For Holonomic mode (strafing), hold down the shift key:
---------------------------
   U    I    O
   J    K    L
   M    <    >

t : up (+z)
b : down (-z)

anything else : stop

q/z : increase/decrease max speeds by 10%
w/x : increase/decrease only linear speed by 10%
e/c : increase/decrease only angular speed by 10%

CTRL-C to quit
```

# Repeat Rate

If your mobile base requires constant updates on the cmd\_vel topic, teleop\_twist\_keyboard_airsim can be configured to repeat the last command at a fixed interval, using the `repeat_rate` private parameter.

For example, to repeat the last command at 10Hz:

```
rosrun teleop_twist_keyboard_airsim teleop_twist_keyboard_airsim.py _repeat_rate:=10.0
```

It is _highly_ recommened that the repeat rate be used in conjunction with the key timeout, to prevent runaway robots.

# Key Timeout

Teleop\_twist\_keyboard_airsim can be configured to stop your robot if it does not receive any key presses in a configured time period, using the `key_timeout` private parameter.

For example, to stop your robot if a keypress has not been received in 0.6 seconds:
```
rosrun teleop_twist_keyboard_airsim teleop_twist_keyboard_airsim.py _key_timeout:=0.6
```

It is recommended that you set `key_timeout` higher than the initial key repeat delay on your system (This delay is 0.5 seconds by default on Ubuntu, but can be adjusted).

# Twist with header
Publishing a `TwistStamped` message instead of `Twist` can be enabled with the `stamped` private parameter. Additionally the `frame_id` of the `TwistStamped` message can be set with the `frame_id` private parameter.
```
rosrun teleop_twist_keyboard_airsim teleop_twist_keyboard_airsim.py _stamped:=True _frame_id:=base_link
```
