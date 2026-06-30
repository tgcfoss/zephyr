.. zephyr:code-sample:: max31826
   :name: MAX31826 1-Wire Temperature Sensor
   :relevant-api: sensor_interface w1_sensor

   Get ambient temperature data from a MAX31826 sensor (polling mode). Based on
   the DS18B20 sensor sample.

Overview
********

This sample shows how to use the Zephyr :ref:`sensor` API driver for the
`MAX31826`_ 1-Wire temperature sensor.

.. _MAX31826:
   https://www.analog.com/en/products/MAX31826.html

The sample periodically reads temperature data from the
first available MAX31826 device discovered in the system. The sample checks the
sensor in polling mode (without interrupt trigger).

Building and Running
********************

The devicetree must have an enabled node with ``compatible = "maxim,max31826";``.
See below for examples and common configurations.

If the sensor is not built into your board, start by wiring the sensor pins
as shown in the Figure Hardware Configuration of the `MAX31826 datasheet`_ at
page 11.

.. _MAX31826 datasheet:
   https://www.analog.com/media/en/technical-documentation/data-sheets/MAX31826.pdf

Boards with a built-in MAX31826 or a board-specific overlay
===========================================================

Your board may have a MAX31826 node configured in its devicetree by default,
or a board specific overlay file with a MAX31826 node is available.
Make sure this node has ``status = "okay";``, then build and run with:

.. zephyr-app-commands::
   :zephyr-app: samples/sensor/max31826
   :goals: build flash
   :board: nucleo_g0b1re

MAX31826 via Arduino Serial pins
================================

Make sure that you have an external circuit to provide an open-drain interface
for the 1-Wire bus.
Once you have wired the sensor and the serial peripheral on the Arduino header
to the 1-Wire bus, build and flash with:

.. zephyr-app-commands::
   :zephyr-app: samples/sensor/max31826
   :goals: build flash
   :gen-args: -DDTC_OVERLAY_FILE=arduino_serial.overlay

The devicetree overlay :zephyr_file:`samples/sensor/max31826/arduino_serial.overlay`
should work on any board with a properly configured Arduino pin-compatible Serial
peripheral.

Sample Output
=============

The sample prints output to the serial console. MAX31826 device driver messages
are also logged. Refer to your board's documentation for information on
connecting to its serial console.

Here is example output for the default application settings, assuming that only
one MAX31826 sensor is connected to the standard Arduino Serial pins:

.. code-block:: none

   *** Booting Zephyr OS build ***
   Found device "max31826", getting sensor data

   Temp: 25.040000
   Temp: 25.030000
