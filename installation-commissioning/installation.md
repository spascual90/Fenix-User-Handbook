# Calibration of compass and actuator. Set up of Interfaces

## Introduction

This chapter explains how to calibrate your tiller pilot IMU and linear actuator.

{% hint style="warning" %}
These activities shall be performed through Bluetooth and Serial I/F and before installing Autopilot to the boat,
{% endhint %}

#### Connect Autopilot to different systems

* Connect Autopilot to Laptop/PC via serial terminal. Check PC/ Laptop Support Tools for help.
* Connect Autopilot to Fenix App via Bluetooth
* Connect Autopilot to a 12V source (battery or alternative) for linear actuator calibration

## Compass calibration

{% hint style="info" %}
**Prerequisites:** Depending on the IMU device used, calibration procedure can change.

**Sparkfun IMU ICM20948:** This IMU has the best performance among all and is strongly recommended. For calibration, Fenix\_ICM\_20948\_Cal (Python application running on Windows/ Linux) is required.

**Discontinued IMU after Fenix V3.3:**

_**BNO055 IMU Internal Sensor Fusion**_ nothing specific to be taken into account.

_**BNO055 IMU External Sensor Fusion**_ calibrates dynamically and do not require calibration.

_**Pololu MinIMU9V5**_
{% endhint %}

Fenix autopilot is compatible with Sparkfun IMU ICM20948: This IMU has the best performance among all. For calibration, Fenix\_ICM\_20948\_Cal (Python application running on Windows/ Linux) is required.

## Calibration of Sparkfun IMU ICM20948

All the steps are performed on [Fenix\_ICM\_20948\_Cal.py](../annexes/fenix_icm_20948.md) application running and connected via Serial port (USB) to Fenix autopilot version ICM\_20948 (Sparkfun).

1. Connect Autopilot version ICM\_20948 (Sparkfun)
2. Press "Scan Serial Ports" to search for a COM port where Fenix is connected. Press "Connect".
3. "Press receive raw data from sensors". For each sensor a different procedure shall be followed to collect raw data. Raw data will be stored in files automatically.
   * G - Gyroscope: Keep sensor steady and accumulate some data (10 points should be enough). Close the graphics window.
   * A - Accelerometer: Turn sensor to different positions, keeping each steady for a few seconds. All moves shall be smooth to avoid drifting values. About 300 points should be enough.Close the graphics window.
   * M - Magnetometer: Turn sensor 360º to point at the different cardinal points. About 300 points should be enough. Close the graphics window.
4. Press "Calculate offsets". One graphics window per sensor will be opened with the raw data stored in the files. Close each window to generate the required offsets. A NMEA sentence per sensor will be stored in new files.
5. Press "Send offsets to autopilot". 3 NMEA sentences (1 per sensor) will be sent to Fenix autopilot.
6. Press "Save offsets sent to autopilot". Offsets will be permanently stored into Fenix autopilot.

## Calibration of Linear Actuator

1. From Virtuino App, enter Linear actuator screen and press Start Calibration.

![](<../.gitbook/assets/linear calib.jpg>)

1. Press "Right Arrow" button extend linear actuator up to the extension of the linear actuator which makes rudder angle to 35 degrees (35 degrees to turn starboard).
2. Press "Left Arrow" button to retract linear actuator up to the retraction of the linear actuator which makes rudder angle to -35 degrees (35 degrees to turn portboard).
3. Press "Save" button to save linear actuator offsets
4. Exit calibration screen pressing "Tick" button.

## Configuration of OpenPlotter

### Configuration of Pypilot (Optional to use as external IMU)

Pypilot installed and calibrated

Select Only compass

Select Tab connections and create connection to Signal K as proposed.

Open Signal K server

Select Plugin Config

Enable plugin "Convert Signal K to NMEA0183". Enabled: YES

### Configuration of a new Serial I/F to Fenix Autopilot

Connect Fenix autopilot to an USB port

Open Serial application

* Serial Devices: /dev/ttyOP\_fenix
* data:NMEA0183

Apply Remember device

In the Connections tab, 2 serial connection are displayed, First from Device Fenix Autopilot and second from OpenCPN:

* Device /dev/ ttyACM0 alias /dev/: ttyOP\_fenix data:NMEA0183&#x20;
* Device /dev/ ttyACM0 alias /dev/: data:NMEA0183 Connection: OpenCPN bauds 960

## Configuration of OpenCPN within Openplotter

Set up additional data connections:

* Signal K (set up by default)
  * Priority: 4
* Serial I/O Protocol:&#x20;
  * NMEA 0183&#x20;
  * port: /dev/ttyACM0&#x20;
  * 4800 baud
  * Priority: 7
  * Select "Exit as autopilot or NMEA repeater"
  * Talker ID: EC
  * APB precision: x.xx.
  * Input filter: Accept only sentences: APHDM, APRSA, IIVWR, GP
  * Output filter: Transmit sentences: IIHDM, ECAPB, IIVWR
* Network I/O Protocol: TCP (Optional, to use Pypilot as external IMU).
  * Address: localhost
  * port: 10110
  * Select Exit as autopilot or NMEA repeater.
  * Talker ID: EC
  * APB precision: x.xx.&#x20;
  * Input filter: HDM, VWR
  * Output filter: Transmit sentences: IIHDM, IIVWR

