# Serial Interface

## OpenCPN NMEA I/F

OpenCPN integrates GPS and plotter capabilities to provide user with all required means to define a route and send it to Fenix Autopilot. OpenCPN is required for Nav mode.

Fenix and OpenCPN implements NMEA I/F in both directions

###  Data sent by OpenCPN to Fenix Autopilot in ALL working modes from different sources:

* **Windvane and calculations**
* **External Compass \(only in External Compass mode\):**
* **GPS Fix**
* **Speed Log**

{% hint style="warning" %}
Feature not available in V0.1
{% endhint %}

###  Data sent by OpenCPN to Fenix Autopilot in NAV Mode:

*  **Route**
  *   Next Waypoint ID \(APB-WPT\)

{% hint style="warning" %}
Feature available with limitations in V0.1: Only APB message decoded.
{% endhint %}

####  Message: $APB - Autopilot Sentence "B"

| Field | Value | Function |
| :--- | :--- | :--- |
| 1 | V | Loran-C Blink or SNR warning. General warning flag or other navigation systems when a reliable fix is not available |
| 1 | A | A = OK or not used |
| 2 | V | Loran-C Cycle Lock warning flag |
| 2 | A | OK or not used |
| 3 | Float | Cross Track Error \(XTE\) Magnitude - Minimum distance to route |
| 4 | L | Direction to Steer - Portboard |
| 4 | R | Direction to Steer - Starboard |
| 5 | N | Cross Track Error \(XTE\) Units: Nautical miles |
| 5 | K | Cross Track Error \(XTE\) Units: Kilometers |
| 6 | V | Arrival Circle Alarm: No alarm |
| 6 | A | Arrival Circle Alarm: Arrival Circle Entered |
| 7 | V | Perpendicular Arrival Alarm: No alarm |
| 7 | A | Perpendicular Arrival Alarm: Perpendicular passed at waypoint |
| 8 | Float | Bearing Origin to Next Waypoint \(BOD\) - Angle magnitude |
| 9 | M | Bearing Origin to Next Waypoint \(BOD\) - Magnetic angle |
| 9 | T | Bearing Origin to Next Waypoint \(BOD\) - True angle |
| 10 | C--C | Destination Waypoint ID |
| 11 | Float | Bearing, present position To Next Waypoint \(BTW/BRG\) - Angle magnitude |
| 12 | M | Bearing, present position To Next Waypoint \(BTW/BRG\) - Magnetic angle |
| 12 | T | Bearing, present position To Next Waypoint \(BTW/BRG\) - True angle |
| 13 | Float | Course To Steer to Next Waypoint \(CTS\) - Angle magnitude |
| 14 | M | Course To Steer to Next Waypoint \(CTS\) - Magnetic angle |
| 14 | T | Course To Steer to Next Waypoint \(CTS\) - True angle |

Example:

$GPAPB,A,A,0.10,R,N,V,V,011,M,DEST,011,M,011,M\*3C

$GPAPB,A,A,0.10,R,N,V,V,012,M,DEST,11.50,M,9.03,M\*00

$GPAPB,A,A,0.1,R,K,V,V,0.12,M,DEST,11.50,M,9.03,M\*1B

###  Data sent from Fenix Autopilot to OpenCPN in ALL working modes:

*  **Internal compass \(in Internal Compass Mode only\):**

Message: $HDM - Heading Magnetic

| Field | Value | Function |
| :--- | :--- | :--- |
| 1 | Float x.x | Heading Degrees, magnetic |
| 2 | M | M=Magnetic |

Message: $HDT - Heading True

| Field | Value | Function |
| :--- | :--- | :--- |
| 1 | Float x.x | Heading Degrees, true |
| 2 | T | T=True |

* **Rudder position**

Message: $RSA - Rudder Sensor Angle

| Field | Value | Function |
| :--- | :--- | :--- |
| 1 | Float x.x | Starboard \(or single\) rudder sensor, "-" means Turn To Port |
| 2 | A | Status, A means data is valid |
| 3 | Float x.x | Port rudder sensor |
| 4 | A | Status, A means data is valid |

##  Serial I/F

### Checksum

In order to generate $PEMC messages to be accepted by Fenix Autopilot, a checksum code shall be annexed after \* symbol.

{% hint style="info" %}
Serial I/F examples in this User Guide represent Checksum code as `xx`. To use these examples you should substitute `xx` by the calculated Checksum value.

`Serial I/F Example: $PEMC,00*xx`

`Serial I/F Valid Sentence: $PEMC,00*37`
{% endhint %}

In this link you will find an online Checksum calculator  

{% embed url="http://www.hhhh.org/wiml/proj/nmeaxor.html" %}

{% embed url="https://youtu.be/ewZ32JuCRZA" %}



### $PEMC Message

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Function</th>
      <th style="text-align:left">Additional Field</th>
      <th style="text-align:left">Sentence</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">00</td>
      <td style="text-align:left">Switch working mode from STAND BY to AUTO</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">$PEMC,00*37</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">01</td>
      <td style="text-align:left">Change Current Rudder</td>
      <td style="text-align:left"><a href="untitled.md#additional-field-change-rate">2: Change rate</a>
      </td>
      <td style="text-align:left">$PEMC,01,r*68</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">02</td>
      <td style="text-align:left">Change CTS (Current Target Steering)</td>
      <td style="text-align:left"><a href="untitled.md#additional-field-change-rate">2: Change rate</a>
      </td>
      <td style="text-align:left">$PEMC,02,i*70</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">03</td>
      <td style="text-align:left">Get Installation Parameters</td>
      <td style="text-align:left"><a href="untitled.md#additional-field-installation-parameters">2: Installation Parameters</a>
      </td>
      <td style="text-align:left">$PEMC,03,2,45,5,S,2,-3.2,-32.9,10*xx</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">04</td>
      <td style="text-align:left">Set Installation Parameters</td>
      <td style="text-align:left"><a href="untitled.md#additional-field-installation-parameters">2: Installation Parameters</a>
      </td>
      <td style="text-align:left">$PEMC,04,2,40,4,S,3,4.1,33.9,9*xx</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">05</td>
      <td style="text-align:left">Get PID gain (incl. sample time and deadband)</td>
      <td style="text-align:left"><a href="untitled.md#additional-field-pid-gain">2: PID Gain</a>
      </td>
      <td style="text-align:left">$PEMC,05,2,0.01,0.5,1000,A*xx</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">06</td>
      <td style="text-align:left">Set PID gain (inc. sample time and deadband)</td>
      <td style="text-align:left"><a href="untitled.md#additional-field-pid-gain">2: PID Gain</a>
      </td>
      <td style="text-align:left">$PEMC,06,3,0.11,0.7,1000,m*xx</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">07</td>
      <td style="text-align:left">Get Autopilot information</td>
      <td style="text-align:left"><a href="untitled.md#additional-field-apinfo">2: APinfo</a>
      </td>
      <td style="text-align:left">$PEMC,07,S,12,35.60,30.02,2,-0.50*65</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">08</td>
      <td style="text-align:left">Request information</td>
      <td style="text-align:left">
        <p>2: &apos;I&apos; Request Installation Parameters (message $PEMC,03)</p>
        <p>2: &apos;G&apos; Request Gain (message $PEMC,05)</p>
        <p>2: &apos;A&apos; Request Autopilot info. (message $PEMC,07)</p>
      </td>
      <td style="text-align:left">
        <p>$PEMC,08,I*5A</p>
        <p>$PEMC,08,G*54</p>
        <p>$PEMC,08,A*52</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">09</td>
      <td style="text-align:left">Enter/ Exit into IMU Calibration mode</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">$PEMC,09*3E</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">10</td>
      <td style="text-align:left">Enter/ Exit Feedback Calibration mode</td>
      <td style="text-align:left">N/A</td>
      <td style="text-align:left">$PEMC,10*36</td>
    </tr>
    <tr>
      <td style="text-align:left">1</td>
      <td style="text-align:left">11</td>
      <td style="text-align:left">Save values</td>
      <td style="text-align:left">
        <p>2: &apos;I&apos; Save Installation and current Feedback Parameters</p>
        <p>2: &apos;G&apos; Save current PID Gain parameters</p>
        <p>3: &apos;C&apos; Save current IMU Offsets</p>
        <p>4: &apos;R&apos; Restore Inst.Param, Feedback and PID Gain to hardcoded
          values</p>
      </td>
      <td style="text-align:left">
        <p>$PEMC,11,I*52</p>
        <p>$PEMC,11,G*5C</p>
        <p>$PEMC,11,C*58</p>
        <p>$PEMC,11,R*49</p>
      </td>
    </tr>
  </tbody>
</table>###  Additional Field: Change rate [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://emacua.fandom.com/wiki/System_Interfaces?action=edit&section=9)

| Field | Value | Function | Additional Field |
| :--- | :--- | :--- | :--- |
| n | 'i' | Increment Current by 1 Position Unit | N/A |
| n | 'I' | Increment Current by 10 Position Unit | N/A |
| n | 'r' | Reduce Current by 1 Position Unit | N/A |
| n | 'R' | Reduce Current by 10 Position Uni | N/A |

###  Additional Field: Installation Parameters [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://emacua.fandom.com/wiki/System_Interfaces?action=edit&section=10)

| Field | Value | Function | Additional Field |
| :--- | :--- | :--- | :--- |
| n | Integer | Centered Tiller Position | N/A |
| n+1 | Positive Int | Maximum rudder angle | N/A |
| n+2 | Positive Int | Average Cruise Speed | N/A |
| n+3 | 'S' | Installation Side: Starboard | N/A |
| n+3 | 'P' | Installation Side: Portboard | N/A |
| n+4 | Positive Int | Rudder Damping | N/A |
| n+5 | Float | Magnetic Variation | N/A |
| n+6 | Float | Heading Alignment | N/A |
| n+7 | Positive Int | Off course alarm angle | N/A |

###  Additional Field: PID Gain [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://emacua.fandom.com/wiki/System_Interfaces?action=edit&section=11)

| Field | Value | Function | Additional Field |
| :--- | :--- | :--- | :--- |
| n | Float | Kp | N/A |
| n+1 | Float | Ki | N/A |
| n+2 | Float | Kd | N/A |
| n+3 | unsigned long | Sample Time \(mSec\) | N/A |
| n+4 | 'm' | Deadband: Min | N/A |
| n+4 | 'M' | Deadband: Max | N/A |
| n+4 | 'A' | Deadband: Auto | N/A |

###  Additional Field: APinfo [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://emacua.fandom.com/wiki/System_Interfaces?action=edit&section=12)

| Field | Value | Function | Additional Field |
| :--- | :--- | :--- | :--- |
| n | 'S' | STAND-BY Mode | N/A |
| n | 'A' | AUTO Mode | N/A |
| n | 'T' | TRACK Mode | N/A |
| n+1 | Integer | Current Rudder | N/A |
| n+2 | Float | Heading Magnetic \(HDM\) - Magnitude \(M\) | N/A |
| n+3 | Float | Course To Steer \(CTS\) - Magnitude \(M\) | N/A |
| n+4 | Positive int | Deadband value | N/A |
| n+5 | Float | Trimming value | N/A |

