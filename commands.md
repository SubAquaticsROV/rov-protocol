# Commands

## Motors

These are the commands that relate to the motors

### `set_motor_pins` (0x10)

This command tells the robot which pins are related to which motor

```
	0          4         8
0	+----------+---------+
	| Motor Id |   PWM   |
1	+----------+---------+
	|        Pin A       |
2	+----------+---------+
	|        Pin B       |
3	+----------+---------+
```

### `control_motor` (0x11)

This command tells the robot to turn a motor left, right, or off.

```
	0          4         8
0	+----------+---------+
	| Motor Id |  Flags  |
1	+----------+---------+
	|         PWM        |
2	+----------+---------+
```

### `set_pwm_bounds` (0x12)

__Deprecated.__

This command tells the robot to limit the pwm values to a minimum
and a maximum.

```
	0          4         8
0	+----------+---------+
	|       Minimum      |
1	+----------+---------+
	|       Maximum      |
2	+----------+---------+
```

### `set_safety_timeout` (0x13)

__Deprecated.__

This command tells the robot how long it should wait before the
values of and and b flip. It is supposed to prevent a short condition
that can occur.

```
	0          4         8
0	+----------+---------+
	|  Timeout (millis)  |
1	+                    +
	|                    |
2	+----------+---------+
```

## Stepper Motors

The gripper needed a command to control it.

### `set_stepper_pins` (0x20)

This tells the arduino which pin the stepper motor is on.

```
    0          4         8
0   +----------+---------+
    |    Direction Pin   |
1   +----------+---------+
    |      Step Pin      |
2   +----------+---------+
    |     Enable Pin     |
3   +----------+---------+
```

### `control_stepper` (0x21)

The DR field tells which direction the stepper should turn, and the RN field
tells if the stepper should be turning.

```
    0  1  2    4         8
0   +--+--+----+---------+
    |DR|RN|    Unused    |
1   +--+--+----+---------+
```

### `set_stepper_state` (0x22)

This tells the arduino to set the mode of the enable pin.

```
    0          4         8
0   +----------+---------+
    |       Enable       |
1   +----------+---------+
```

## Sensors

These commands will allow you to configure and turn on sensor feedback.

### `set_sensor_state` (0x30)

Turns on the sensor and begins streaming it to the surface.

| ID |Sensor            |
|----|------------------|
|0x31|Voltage Sensor    |
|0x32|Temperature Sensor|
|0x33|Depth Sensor      |

```
	0          4         8
0	+----------+---------+
	|      Sensor ID     |
1	+----------+---------+
	|        Mode        |
2	+----------+---------+
```

### `set_voltage_sensor_pin`(0x31)

Configures the voltage sensor pin.

```
	0          4         8
0	+----------+---------+
	|         Pin        |
1	+----------+---------+
```

### `set_temperature_sensor_pin`(0x32)

Configures the temperature sensor pin.

```
	0          4         8
0	+----------+---------+
	|         Pin        |
1	+----------+---------+
```

### `set_depth_sensor_density`(0x33)

Configures the density of the depth sensor, and it also initializes the sensor.
This MUST be called before the depth sensor can be used.

```
	0          4         8
0	+----------+---------+
	|                    |
1	+                    +
	|    Density (int)   |
2	+                    +
	|                    |
3	+                    +
	|                    |
4	+----------+---------+
```


## Cameras

The cameras need their own commands! You use them to tell the ROV which pins
the multiplexer is connected to, and which camera is supposed to be on.

### `set_camera_pins` (0x40)

This configures all of the multiplexer pins! The multiplexer requires the most
pins, as well as the most bytes to configure. And since a second multiplexer was
added, this command is by far the longest.

```
    0          4         8
0   +----------+---------+
    |        Pin 1       |
1   +----------+---------+
    |        Pin 2       |
2   +----------+---------+
    |        Pin 3       |
3   +----------+---------+
    |        Pin 4       |
4   +----------+---------+
    |        Pin 5       |
5   +----------+---------+
    |        Pin 6       |
6   +----------+---------+
    |        Pin 7       |
7   +----------+---------+
    |        Pin 8       |
8   +----------+---------+
```

### `switch_camera` (0x41)

This tells the arduino to switch the camera. The fourth bit of the flags
indicates which multiplexer to use.

```
    0          4         8
0   +----------+---------+
    |  Flags   | Camera  |
1   +----------+---------+
```

## Misc

These commands don't really fit into any category. These are mostly for testing.

### `echo` (0xF0)

This command tells the arduino board to repeat the byte that follows to the
computer.

```
	0          4         8
0	+----------+---------+
	|        Data        |
1	+----------+---------+
```


### `version` (0xF1)

Get the current version of the software running on the arduino.

This command has no data associated with it.
