# Compass calibration

## Introduction

Fenix autopilot is compatible with different types of IMU devices. Each has a different calibration procedure.

* Sparkfun IMU ICM20948: This IMU has the best performance among all and is strongly recommended. For calibration, Fenix\_ICM\_20948\_Cal (Python application running on Windows/ Linux) is required.
* Pololu MinIMU9V5. Has a good performance but less precisse and slower than ICM20948. Calibration of this IMU is very simple and can be done with Fenix App (mobile phone). If you don't have computer skills is a good alternative.
* Adafruit BNO055 is discontinued by the supplier and available units have demostrate low reliability. Is not supported by Fenix versions after V3.3.

## Calibration of Sparkfun IMU ICM20948

All the steps are performed on Fenix\_ICM\_20948\_Cal.py application running and connected via Serial port (USB) to Fenix autopilot version ICM\_20948 (Sparkfun).

1. Connect Autopilot version ICM\_20948 (Sparkfun)
2. Press "Scan Serial Ports" to search for a COM port where Fenix is connected. Press "Connect".
3. "Press receive raw data from sensors". For each sensor a different procedure shall be followed to collect raw data. Raw data will be stored in files automatically.
   * G - Gyroscope: Keep sensor steady and accumulate some data (10 points should be enough). Close the graphics window.
   * A - Accelerometer: Turn sensor to different positions, keeping each steady for a few seconds. All moves shall be smooth to avoid drifting values. About 300 points should be enough.Close the graphics window.
   * M - Magnetometer: Turn sensor 360º to point at the different cardinal points. About 300 points should be enough. Close the graphics window.
4. Press "Calculate offsets". One graphics window per sensor will be opened with the raw data stored in the files. Close each window to generate the required offsets. A NMEA sentence per sensor will be stored in new files.
5. Press "Send offsets to autopilot". 3 NMEA sentences (1 per sensor) will be sent to Fenix autopilot.
6. Press "Save offsets sent to autopilot". Offsets will be permanently stored into Fenix autopilot.



## Calibration of  Pololu MinIMU9V5

All the steps are performed on Fenix App mobile application running and connected via Bluetooth to Fenix autopilot version MimIMU9V5 (Pololu).

1. Connect Fenix Autopilot to Autopilot App via Bluetooth
2. In the Autopilot App, navigate to the Compass Calibration screen and click "Start".
3. **Gyroscope and Accelerometer calibration process:** Keep device stable, horizontal with components on top for 5 seconds. Status will reflect 3G and 3A status when finished.&#x20;
4. **Magnetometer calibration process:** Initiate magnetometer calibration by moving the device in a figure-eight pattern to capture all possible orientations. The system will display "3M" once it has finished.
5. Press "Save" to store calibration values permanently into Fenix Autopilot.
