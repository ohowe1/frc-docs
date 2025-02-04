Getting to know your Romi
=========================

Directional Conventions
-----------------------

The front of the Romi is where the Raspberry Pi USB ports, GPIO pins and suspended caster wheel are.

.. image:: images/getting-to-know-romi/romi-front-view.png
   :alt: Romi Front View

In all Romi documentation, references to driving forward use the above definition of "front".

.. image:: images/getting-to-know-romi/romi-forward.png
   :alt: Romi Forward Driving Direction

Hardware, Sensors and GPIO
--------------------------

The Romi has the following built-in hardware/peripherals:

- 2x geared motors with encoders
- 1x Inertial Measurement Unit (IMU)
- 3x LEDs (green, yellow, red)
- 3x pushbuttons (marked A, B, and C)
- 5x configurable GPIO channels

Motors, Wheels and Encoders
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The motors used on the Romi have a 120:1 gear reduction, and a no-load output speed of 150 RPM at 4.5V. The free current is 0.13 amps and the stall current is 1.25 amps. Stall torque is 25 oz-in (0.1765 N-m) but the built-in safety clutch might start slipping at lower torques.

The wheels have a diameter of 70mm (2.75"). They have a trackwidth of 141mm (5.55").

The encoders are connected directly to the motor output shaft and have 12 Counts Per Revolution (CPR). With the provided gear ratio, this nets 1440 counts per wheel revolution.

.. note:: By default, the encoders count up when the Romi moves forward.

Inertial Measurement Unit
^^^^^^^^^^^^^^^^^^^^^^^^^

The Romi includes an STMicroelectronics LSM6DS33 Inertial Measurement Unit (IMU) which contains a 3-axis gyro and a 3-axis accelerometer.

The accelerometer has selectable sensitivity of 2G, 4G, 8G, and 16G. The gyro has selectable sensitivity of 125 Degrees Per Second (DPS), 250 DPS, 500 DPS, 1000 DPS and 2000 DPS.

The Romi Web UI also provides a means to calibrate the gyro and measure its zero-offsets before use with robot code.

LEDs and Push Buttons
^^^^^^^^^^^^^^^^^^^^^

The Romi 32U4 control board has 3 push buttons and 3 LEDs that are exposed as Digital IO channels to robot code. The section on GPIO Mapping has more information on how to use the built in LEDs and buttons in robot code.

Configurable GPIO Channels
^^^^^^^^^^^^^^^^^^^^^^^^^^

The control board has 5 configurable GPIO channels (named EXT0 through EXT4) that allow a user to connect external sensors and actuators to the Romi.

.. image:: images/getting-to-know-romi/romi-external-io.png
   :alt: Romi External GPIO Channels

All 5 channels support the following modes: Digital IO, Analog In, PWM (with the exception of EXT 0, which only supports Digital IO and PWM).

The GPIO channels are exposed via a 3-pin, servo style interface, with connections for Ground, Power and Signal (with the Ground connection being closest to the edge of the board, and the signal being closest to the inside of the board).

The power connections for the GPIO channels are initially left unconnected, but can be hooked into the Romi's on-board 5V supply by using a jumper to connect the 5V pin to the power bus (as seen in the image above). Additionally, if more power than the Romi can provide is needed, the user can provide their own 5V power supply and connect it directly to power bus and ground pins.

GPIO Mapping
------------

To support all the built in peripherals on the Romi, we have provided a hard-coded mapping of WPILib channels/devices to the Romi hardware.

Digital IO
^^^^^^^^^^

+-------------+--------------------------------------+
| DIO Channel | Romi Hardware Component              |
+=============+======================================+
| DIO 0       | Button A (input only)                |
+-------------+--------------------------------------+
| DIO 1       | Button B (input), Green LED (output) |
+-------------+--------------------------------------+
| DIO 2       | Button C (input), Red LED (output)   |
+-------------+--------------------------------------+
| DIO 3       | Yellow LED (output only)             |
+-------------+--------------------------------------+
| DIO 4       | Left Encoder Quadrature Channel A    |
+-------------+--------------------------------------+
| DIO 5       | Left Encoder Quadrature Channel B    |
+-------------+--------------------------------------+
| DIO 6       | Right Encoder Quadrature Channel A   |
+-------------+--------------------------------------+
| DIO 7       | Right Encoder Quadrature Channel B   |
+-------------+--------------------------------------+

Writes to DIO 0, 4, 5, 6 and 7 will result in no-ops.

Analog Input (Default Configuration)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

+------+-------------------+
| Port | Channel           |
+======+===================+
| AIN0 | Analog 6 / Pin 4  |
+------+-------------------+
| AIN1 | Analog 2 / Pin 20 |
+------+-------------------+

PWM Output
^^^^^^^^^^

The table below shows the default pins. These are configurable (with the exception of PWM 0 and 1) via the Web UI.
+-------------+-------------------------+
| PWM Channel | Romi Hardware Component |
+=============+=========================+
| PWM 0       | Left Motor              |
+-------------+-------------------------+
| PWM 1       | Right Motor             |
+-------------+-------------------------+
| PWM 2       | Pin 21 / A3             |
+-------------+-------------------------+
| PWM 3       | Pin 22 / A4             |
+-------------+-------------------------+

.. note:: The right motor is hardwired to spin in a forward direction when forward stick movement is applied on a joystick. Thus there is no need to invert the corresponding motor controller in robot code.

GPIO Channels
^^^^^^^^^^^^^

The Romi Web UI allows the user to customize the functions of the 5 configurable GPIO channels. The UI will also provide the appropriate WPILib channel/device mappings on screen once the IO configuration is complete. More information on this can be found in the next section.
