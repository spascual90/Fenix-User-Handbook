# Installation

## Installation Process

This chapter explains how to install your tiller pilot&#x20;

## Before Autopilot installation

These activities shall be performed through Serial I/F and before installing Autopilot into boat,

#### Connect Autopilot to PC/Laptop

* Install serial terminal&#x20;
* Connect Autopilot to Laptop/PC
* Connect Autopilot to a 12V source (battery or alternative)

### Compass calibration

1. In Virtuino App, enter into Compass calibration screen and press Start Calibration button,

![](<../.gitbook/assets/compass calib.jpg>)

1. From Virtuino App, enter into Compass calibration mode.
2. To calibrate BNO055 IMU sensor follow the steps:
   1. Gyroscope Calibration: Place the device in a single stable position to allow the gyroscope to calibrate. Keep this position for a period of few seconds until GYRO register indicates fully calibrated.
   2. Accelerometer Calibration: Place the device in 6 different stable positions for a period of few seconds to allow the accelerometer to calibrate. Repeat until&#x20;
   3. the ACC register indicates fully calibrated.
   4. Magnetometer Calibration: Make some random movements (for example: writing the number ‘8’ on air) until the MAG register indicates fully calibrated.
3. Verify Calibration: Autopilot will automatically exit Calibration mode after a reasonable time after calibration of each sensor. User shall make additional random movements to cover all different yaw, pitch and roll angles. Make smooth and fast movements. Make movements until MAG register is stable.

Calibration Verification result,

* [x] Calibration OK: Press "Save" button to store Compass calibration values for later use.
* [ ] Calibration KO: repeat Compass calibration process.

Once the compass is calibrated and values saved, the calibration profile will be reused to get the correct orientation data immediately after Power-on Autopilot.

{% hint style="info" %}
Make sure that there is slow movement between 2 stable positions

The 6 stable positions could be in any direction, but make sure that the device is lying at least once perpendicular to the x, y and z axis.
{% endhint %}

{% hint style="info" %}
Magnetometer in general are susceptible to both hard-iron and soft-iron distortions, but majority of the cases are rather due to the former. And the steps mentioned below are to calibrate the magnetometer for hard-iron distortions. Nevertheless certain precautions need to be taken into account during the positioning of the sensor to avoid unnecessary magnetic influences.
{% endhint %}

You can find below a Video tutorial by IMU BNO055 Manufacturer.

{% embed url="https://youtu.be/Bw0WuAyGsnY" %}

### Linear actuator calibration

1. From Virtuino App, enter Linear actuator screen and press Start Calibration.

![](<../.gitbook/assets/linear calib.jpg>)

1. Press "Right Arrow" button extend linear actuator up to the complete extension of the linear actuator.
2. Press "Left Arrow" button to retract linear actuator up to the complete retraction of the linear actuator.
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

