# User functions

## Change mode

### Switch working mode from STAND BY to AUTO

This function allows user to change Autopilot working mode from Stand-by to Auto alternatively.

* Executed in Stand-by mode, Autopilot will switch to Auto mode.
* Executed in Auto mode, Autopilot will switch to Stand-by mode.

### Enter into Track mode

## Rudder control

This set of functions allows user to change rudder angle.

{% hint style="info" %}
Rudder control functions are only available in Stand by mode.
{% endhint %}

{% hint style="info" %}
Behaviour will be different depenting on Autopilot installation side, startboard or portboard.
{% endhint %}

{% hint style="warning" %}
In Fenix V0.1, the value of`Installation Side` parameter is always `STARBOARD` 
{% endhint %}

### Increment Current Rudder by 1 Position Unit.

Perform a SHORT EXTENSION of the linear actuator to increase current rudder angle.

### Increment Current Rudder by 10 Position Unit.

Perform a LONG EXTENSION of the linear actuator to increase current rudder angle..

### Reduce Current Rudder by 1 Position Unit.

Perform a SHORT RETRACTION of the linear actuator to decrease current rudder angle.

### Reduce Current Rudder by 10 Position Unit.

Perform a LONG EXTENSION of the linear actuator to increase current rudder angle.

## Control Course to Steer

This set of functions allows user to change CTS angle.

{% hint style="info" %}
If executed in Stand-by mode, target CTS will be changed and will only take effect once autopilot is in Auto mode.
{% endhint %}

### Increment CTS by 1º

Increment CTS value in 1º

### Increment CTS by 10º

Increment CTS value in 10º

### Reduce CTS by 1º

Reduce CTS value in 1º

### Reduce CTS by 10º

Reduce CTS value in 10º

### Return to initial CTS

Restore CTS to initial CTS value \(CTS when switched to Auto mode\).

### Accept Autopilot action

### Reject Autopilot action

## Autopilot monitoring

### Get Autopilot information

* Current Mode
* Current Rudder Position
* Heading Magnetic \(HDM\)
* Course To Steer \(CTS\)
* Deadband value
* Trimm

## Configuration control

### Get Installation Parameters

* Centered Tiller Position
* Maximum rudder angle
* Average Cruise Speed
* Installation Side
* Rudder Damping
* Magnetic Variation
* Heading Alignment
* Off course alarm angle

### Set Installation Parameters

### Get current Autopilot gain

* Kp
* Ki
* Kd
* Sample Time
* Deadband type \(auto, min, max\)
* Deadband value

### Set new Autopilot gain

### Save current Autopilot gain

## Commissioning Functions

{% hint style="info" %}
This funcions are only available in Stand-by mode
{% endhint %}

### Start compass calibration

This function allows user to calibrate internal IMU.

To calibrate BNO055 IMU sensor follow the steps:

* [x] Gyroscope Calibration: Place the device in a single stable position to allow the gyroscope to calibrate. Keep this position for a period of few seconds until GYRO register indicates fully calibrated.



* [x] Accelerometer Calibration: Place the device in 6 different stable positions for a period of few seconds to allow the accelerometer to calibrate. Repeat until 

  the ACC register indicates fully calibrated.

{% hint style="info" %}
Make sure that there is slow movement between 2 stable positions

The 6 stable positions could be in any direction, but make sure that the device is lying at least once perpendicular to the x, y and z axis.
{% endhint %}

* [x] Magnetometer Calibration: Make some random movements \(for example: writing the number ‘8’ on air\) until the MAG register indicates fully calibrated.

{% hint style="info" %}
Magnetometer in general are susceptible to both hard-iron and soft-iron distortions, but majority of the cases are rather due to the former. And the steps mentioned below are to calibrate the magnetometer for hard-iron distortions. Nevertheless certain precautions need to be taken into account during the positioning of the sensor to avoid unnecessary magnetic influences.
{% endhint %}

* [x] Verify Magnetometer calibration: Make additional random movements to cover all different yaw, pitch and roll angles. Keep on moving until MAG register is stable.

{% hint style="warning" %}
Verify Magnetometer calibration step IS A MUST to ensure valid calibration values.
{% endhint %}

You can find below a tutorial by IMU BNO055 Manufacturer.

{% embed url="https://youtu.be/Bw0WuAyGsnY" %}



### Save compass offsets

### Start linear actuator calibration

### Save linear actuator offsets



