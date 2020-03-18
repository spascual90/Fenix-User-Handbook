# Commissioning

## Commissioning Process

Before first use of Fenix Autopilot, user shall go through the complete Commissioning process.

1. Calibrate compass
2. Calibrate linear actuator
3. Adjust Installation Parameters

{% hint style="info" %}
This funcions are only available in Stand-by mode
{% endhint %}

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



### Save linear actuator offsets

