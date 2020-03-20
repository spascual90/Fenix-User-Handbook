# Commissioning

## Commissioning Process

This chapter explains how to commission your tiller pilot after installation. This consists of a number of simple functional tests followed by a short sea trial.

Before first use of Fenix Autopilot, user shall go through the complete Commissioning process.

## Before Autopilot installation

These activities shall be performed through Serial I/F and before installing Autopilot into boat,

#### Connect Autopilot to PC/Laptop

* Install serial terminal 
* Connect Autopilot to Laptop/PC
* Connect Autopilot to a 12V source \(battery or alternative\)

### Start compass calibration

1. [Enter into Compass calibration mode](../using-fenix-tiller-pilot/user-functions.md#start-compass-calibration) using Serial I/F.
2. To calibrate BNO055 IMU sensor follow the steps:
   1. Gyroscope Calibration: Place the device in a single stable position to allow the gyroscope to calibrate. Keep this position for a period of few seconds until GYRO register indicates fully calibrated.
   2. Accelerometer Calibration: Place the device in 6 different stable positions for a period of few seconds to allow the accelerometer to calibrate. Repeat until 
   3. the ACC register indicates fully calibrated.
   4. Magnetometer Calibration: Make some random movements \(for example: writing the number ‘8’ on air\) until the MAG register indicates fully calibrated.
3. Verify Calibration: Autopilot will automatically exit Calibration mode after a reasonable time after calibration of each sensor. User shall make additional random movements to cover all different yaw, pitch and roll angles. Make smooth and fast movements. Make movements until MAG register is stable.

Calibration Verification result,

* [x] Calibration OK: [save Compass calibration](../using-fenix-tiller-pilot/user-functions.md#save-compass-offsets) values
* [ ] Calibration KO: repeat Compass calibration process

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

### Start linear actuator calibration

1. [Enter into linear actuator calibration mode](../using-fenix-tiller-pilot/user-functions.md#start-compass-calibration)
2. Extend linear actuator
3. Retract linear actuator
4. [Exit calibration mode](../using-fenix-tiller-pilot/user-functions.md#start-linear-actuator-calibration)
5. Save linear actuator offsets

## After Autopilot installation

### Functional tests

#### Switch on

1. Switch on the main power breaker.

2. The autopilot should beep and display the pilot number \(ST1000 or ST2000\). 

3. Within 2 seconds, the display should show a flashing ‘C’ followed by the compass heading \(for example, C 234\). 

This shows the autopilot is active. Note: If the tiller pilot does not beep or display the compass heading, please refer to the Fault Finding section \(see page 26\).

#### Operating sense

The operating sense defines the direction the tiller pilot will apply helm when a course change key is pressed or the boat goes off course. To check the operating sense:

1. Place the pushrod end over the tiller pin.

2. Press +10.

3. The helm should move to produce a turn to starboard

If the helm produces a turn to port, refer to the following instructions on reversing the operating sense.

#### Reversing the operating sense

{% hint style="danger" %}
Feature not available in Fenix V0.1.
{% endhint %}

### Check Interfaces

#### Checking the Serial I/F

#### Checking the Virtuino App interface

#### Checking the OpenCPN interface

{% hint style="warning" %}
To be completed
{% endhint %}

### Initial sea trial

### 

