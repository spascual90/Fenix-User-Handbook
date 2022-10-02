# Serial Interface

## Introduction

Fenix Autopilot can be connected to a Laptop/PC via USB port. This provides access to all user functions available to calibrate compass and linear actuator. Also provides full capabilities to customize installation settings and pilot gain.

## Requirements



* Serial Terminal shall be installed to Laptop/PC to communicate with Autopilot to use Serial Interface (eg. Arduino IDE, Putty)
* [Checksum calculator](untitled.md#checksum)
* [$PMEC Message specification](untitled.md#usdpemc-message) in this Guide.



### Checksum

In order to generate $PEMC messages to be accepted by Fenix Autopilot, a checksum code shall be annexed after \* symbol.

{% hint style="info" %}
Serial I/F examples in this User Guide represent Checksum code as `xx`. To use these examples you should substitute `xx` by the calculated Checksum value.

`Serial I/F Example: $PEMC,00*xx`

`Serial I/F Valid Sentence: $PEMC,00*37`
{% endhint %}

In this link you will find an online Checksum calculator &#x20;

{% embed url="http://www.hhhh.org/wiml/proj/nmeaxor.html" %}

{% embed url="https://youtu.be/ewZ32JuCRZA" %}

#### Set messages: 04 and 06

To keep same value of a parameter while changing others, omit any value while keeping the commas in place.

{% hint style="info" %}
To set Ki value while keeping Kp and Kd: $PEMC,06,,0.3,,,m\*xx
{% endhint %}

{% hint style="warning" %}
Fenix V0.1 bug: Message 06, always include `m, M or A` deadband value or system will change to `M`.
{% endhint %}



### $PEMC Message

| Field | Value | Function                                      | Additional Field                                                                                                                                                                                                               | Sentence                                                                         |
| ----- | ----- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------- |
| 1     | 00    | Switch working mode from STAND BY to AUTO     | N/A                                                                                                                                                                                                                            | $PEMC,00\*37                                                                     |
| 1     | 01    | Change Current Rudder                         | [2: Change rate](untitled.md#additional-field-change-rate)                                                                                                                                                                     | $PEMC,01,r\*68                                                                   |
| 1     | 02    | Change CTS (Current Target Steering)          | [2: Change rate](untitled.md#additional-field-change-rate)                                                                                                                                                                     | $PEMC,02,i\*70                                                                   |
| 1     | 03    | Get Installation Parameters                   | [2: Installation Parameters](untitled.md#additional-field-installation-parameters)                                                                                                                                             | $PEMC,03,2,45,5,S,2,-3.2,-32.9,10\*xx                                            |
| 1     | 04    | Set Installation Parameters                   | [2: Installation Parameters](untitled.md#additional-field-installation-parameters)                                                                                                                                             | $PEMC,04,2,40,4,S,3,4.1,33.9,9\*xx                                               |
| 1     | 05    | Get PID gain (incl. sample time and deadband) | [2: PID Gain](untitled.md#additional-field-pid-gain)                                                                                                                                                                           | $PEMC,05,2,0.01,0.5,100,A\*xx                                                    |
| 1     | 06    | Set PID gain (inc. sample time and deadband)  | [2: PID Gain](untitled.md#additional-field-pid-gain)                                                                                                                                                                           | $PEMC,06,3,0.11,0.7,100,m\*xx                                                    |
| 1     | 07    | Get Autopilot information                     | [2: APinfo](untitled.md#additional-field-apinfo)                                                                                                                                                                               | $PEMC,07,S,12,35.60,30.02,2,-0.50\*65                                            |
| 1     | 08    | Request information                           | <p>2: 'I' Request Installation Parameters (message $PEMC,03)</p><p>2: 'G' Request Gain (message $PEMC,05)</p><p>2: 'A' Request Autopilot info. (message $PEMC,07)</p>                                                          | <p>$PEMC,08,I*5A</p><p>$PEMC,08,G*54</p><p>$PEMC,08,A*52</p>                     |
| 1     | 09    | Enter/ Exit into IMU Calibration mode         | N/A                                                                                                                                                                                                                            | $PEMC,09\*3E                                                                     |
| 1     | 10    | Enter/ Exit Feedback Calibration mode         | N/A                                                                                                                                                                                                                            | $PEMC,10\*36                                                                     |
| 1     | 11    | Save values                                   | <p>2: 'I' Save Installation and current Feedback Parameters</p><p>2: 'G' Save current PID Gain parameters</p><p>2: 'C' Save current IMU Offsets</p><p>2: 'R' Restore Inst.Param, Feedback and PID Gain to hardcoded values</p> | <p>$PEMC,11,I*52</p><p>$PEMC,11,G*5C</p><p>$PEMC,11,C*58</p><p>$PEMC,11,R*49</p> |
| 1     | 12    | IMU Cal.Mode values                           | Cal.Mode values                                                                                                                                                                                                                | $PEMC,12,                                                                        |

#### &#x20;Additional Field: Change rate [![](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M1IFMsiQH0N5uEseRXb%2Fuploads%2FacmjKiNZvOmCvT3sdMR1%2Ffile.gif?alt=media)](https://emacua.fandom.com/wiki/System\_Interfaces?action=edit\&section=9)

| Field | Value | Function                              | Additional Field |
| ----- | ----- | ------------------------------------- | ---------------- |
| n     | 'i'   | Increment Current by 1 Position Unit  | N/A              |
| n     | 'I'   | Increment Current by 10 Position Unit | N/A              |
| n     | 'r'   | Reduce Current by 1 Position Unit     | N/A              |
| n     | 'R'   | Reduce Current by 10 Position Uni     | N/A              |

#### &#x20;Additional Field: Installation Parameters [![](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M1IFMsiQH0N5uEseRXb%2Fuploads%2FfOfMRFSx9Pu5ReJekINY%2Ffile.gif?alt=media)](https://emacua.fandom.com/wiki/System\_Interfaces?action=edit\&section=10)

| Field | Value        | Function                     | Additional Field |
| ----- | ------------ | ---------------------------- | ---------------- |
| n     | Integer      | Centered Tiller Position     | N/A              |
| n+1   | Positive Int | Maximum rudder angle         | N/A              |
| n+2   | Positive Int | Average Cruise Speed         | N/A              |
| n+3   | 'S'          | Installation Side: Starboard | N/A              |
| n+3   | 'P'          | Installation Side: Portboard | N/A              |
| n+4   | Positive Int | Rudder Damping               | N/A              |
| n+5   | Float        | Magnetic Variation           | N/A              |
| n+6   | Float        | Heading Alignment            | N/A              |
| n+7   | Positive Int | Off course alarm angle       | N/A              |

#### &#x20;Additional Field: PID Gain [![](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M1IFMsiQH0N5uEseRXb%2Fuploads%2Fq2R7cAPb2cDKJIdSPnwG%2Ffile.gif?alt=media)](https://emacua.fandom.com/wiki/System\_Interfaces?action=edit\&section=11)

| Field | Value         | Function           | Additional Field |
| ----- | ------------- | ------------------ | ---------------- |
| n     | Float         | Kp                 | N/A              |
| n+1   | Float         | Ki                 | N/A              |
| n+2   | Float         | Kd                 | N/A              |
| n+3   | unsigned long | Sample Time (mSec) | N/A              |
| n+4   | 'm'           | Deadband: Min      | N/A              |
| n+4   | 'M'           | Deadband: Max      | N/A              |
| n+4   | 'A'           | Deadband: Auto     | N/A              |

#### &#x20;Additional Field: APinfo [![](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M1IFMsiQH0N5uEseRXb%2Fuploads%2FC0vHPcXOrfRFakN9kyMY%2Ffile.gif?alt=media)](https://emacua.fandom.com/wiki/System\_Interfaces?action=edit\&section=12)

| Field | Value        | Function                               | Additional Field |
| ----- | ------------ | -------------------------------------- | ---------------- |
| n     | 'S'          | STAND-BY Mode                          | N/A              |
| n     | 'A'          | AUTO Mode                              | N/A              |
| n     | 'T'          | TRACK Mode                             | N/A              |
| n     | 'C'          | Calibration Mode (IMU or Feedback)     | N/A              |
| n+1   | Integer      | Current Rudder                         | N/A              |
| n+2   | Float        | Heading Magnetic (HDM) - Magnitude (M) | N/A              |
| n+3   | Float        | Course To Steer (CTS) - Magnitude (M)  | N/A              |
| n+4   | Positive int | Deadband value                         | N/A              |
| n+5   | Float        | Trimming value                         | N/A              |

#### Additional Field: IMU Cal. values [![](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M1IFMsiQH0N5uEseRXb%2Fuploads%2Fq3Nzt2jzMSVFIUKTf19q%2Ffile.gif?alt=media)](https://emacua.fandom.com/wiki/System\_Interfaces?action=edit\&section=12)

| Field | Value           | Function                                                     | Additional Field |
| ----- | --------------- | ------------------------------------------------------------ | ---------------- |
| n     | '-'             | Calib. Not started                                           | N/A              |
| n     | 'O'             | Calib. Ongoing                                               | N/A              |
| n     | 'R'             | Recalibrated                                                 | N/A              |
| n     | 'N'             | Not calibrated                                               | N/A              |
| n     | 'C'             | Check ongoing                                                | N/A              |
| n+1   | 1:OK/ 0:NOK     | Sys status. Ony valid when Calib is ongoing                  | N/A              |
| n+2   | 1:OK/ 0:NOK     | Gyro status. Ony valid when Calib is ongoing                 | N/A              |
| n+3   | 1:OK/ 0:NOK     | Accel status. Ony valid when Calib is ongoing                | N/A              |
| n+4   | 1:OK/ 0:NOK     | Magn status. Ony valid when Calib is ongoing                 | N/A              |
| n+5   | Int (0, 360)    | <p>X euler angle. </p><p>Ony valid when Check is ongoing</p> | N/A              |
| n+6   | Int (-180, 180) | <p>Y euler angle.</p><p>Ony valid when Check is ongoing</p>  | N/A              |
| n+7   | Int (0, 90)     | <p>Z euler angle.</p><p>Ony valid when Check is ongoing</p>  | N/A              |
|       |                 |                                                              |                  |
|       |                 |                                                              |                  |

#### Additional Field: IMU Cal. values [![](https://firebasestorage.googleapis.com/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F-M1IFMsiQH0N5uEseRXb%2Fuploads%2Fxziw9SatxmPw0FJi7bue%2Ffile.gif?alt=media)](https://emacua.fandom.com/wiki/System\_Interfaces?action=edit\&section=12)

| Field | Value | Function           | Additional Field |
| ----- | ----- | ------------------ | ---------------- |
| n     | '-'   | Calib. Not started | N/A              |
| n     |       |                    |                  |

## OpenCPN NMEA I/F

OpenCPN integrates GPS and plotter capabilities to provide user with all required means to define a route and send it to Fenix Autopilot. OpenCPN is required for Nav mode.

Fenix and OpenCPN implements NMEA I/F in both directions

### Data sent by OpenCPN to Fenix Autopilot in ALL working modes from different sources:

* **External Compass (only in External Compass mode):**

> Message: $HDM - Heading Magnetic

{% hint style="warning" %}
Features below are not available in V2.x
{% endhint %}

* **Windvane and calculations**
* **GPS Fix**
* **Speed Log**

### Data sent by OpenCPN to Fenix Autopilot in NAV Mode:

#### Message: $APB - Autopilot Sentence "B"&#x20;

* **Route**
  * Waypoint ID
  * Course To Steer to Next Waypoint (CTS) - Magnetic angle
  * Cross Track Error (XTE)
  * Arrival Circle Alarm
  * Perpendicular Circle Alarm

{% hint style="warning" %}
Feature available with limitations in V0.1: Only APB message decoded.
{% endhint %}

### Data sent from Fenix Autopilot to OpenCPN in ALL working modes:

#### **Internal compass (in Internal Compass Mode only):**

> Message: $HDM - Heading Magnetic
>
> Message: $HDT - Heading True

#### **Rudder position**

> Message: $RSA - Rudder Sensor Angle
