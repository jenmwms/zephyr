..up_squared gpio_counter:

UP Squared
##########

Overview
********
This sample provides an example of how to configure GPIO input and output to
the UP Squared board.

The sample enables a pin as GPIO input (active high) that triggers the increment
of a counter (range is 0 to size of counter_pins[]). The counter increments for
each change from 0 to 1 on HAT Pin 16. The value of the counter is represented
on GPIO output (active high) as a 4-bit value
(bin 0, 1, 2, 3 -> HAT Pin 35, 37, 38, 40).


+------------+-----+-----+-----+-----+-----+
| Bit (bin)  | n/a |   3 |   2 |   1 |   0 |
+------------+-----+-----+-----+-----+-----+
| HAT Pin    |  16 |  40 |  39 |  37 |  35 |
+------------+-----+-----+-----+-----+-----+
| BIOS Pin   |  19 |  38 |  27 |  15 |  14 |
+------------+-----+-----+-----+-----+-----+
| Direction  |  IN | OUT | OUT | OUT | OUT |
+------------+-----+-----+-----+-----+-----+
| Active     |   H |   H |   H |   H |   H |
+------------+-----+-----+-----+-----+-----+


Requirements
************

The application requires an UP Squared board connected to the PC through USB
for serial console. The BIOS settings must be updated as specified in the
source code comments for HAT Configurations (see table above).


References
**********

- https://docs.zephyrproject.org/latest/boards/x86/up_squared/doc/index.html


Building and Running
********************

Build the sample in the following way:
.. zephyr-app-commands::
    :zephyr-app: samples/boards/up_squared/gpio_counter
    :board: up_squared
    :goals: build

Prepare the boot device (USB storage drive) as described for the UP Squared.
Insert the USB boot device containing the prepared software binary of the
sample. The board will boot then enter GRUB boot loader unless BIOS option is
selected. Enter the BIOS configuration menu, modify the required HAT
configurations (above) and then select to save the BIOS settings and reset.

The board will reboot and then enter GRUB boot loader. Select to boot Zephyr and
the board will start to execute the sample. Apply input to trigger the increment
of the value of the counter.

.. code-block:: console

   $ minicom -D <tty_device> -b 115200

Replace :code:`<tty_device>` with the port where the UP Squared board
can be found. For example, under Linux, :code:`/dev/ttyUSB0`.
The ``-b`` option sets baud rate.
