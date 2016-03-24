# ROV Protocol

In these documents I describe the communcations between the ROV and the top side
controller. The protocol is not symmetric. The COMMAND protocol (top-to-bottom)
is optimized for configuring and controlling the robot, while the RESPONSE
protocol (bottom-to-top) is designed for sending sensor information for display.
