# User functions

## Change mode

### Switch working mode from STAND BY to AUTO

This function allows user to change Autopilot working mode from Stand-by to Auto or to disactivate Autopilot from any working mode:

* Executed in Stand-by mode, Autopilot will switch to Auto mode.
* Executed in Auto or Track mode, Autopilot will switch to Stand-by mode.

In Virtuino App,

* In Stand-by mode, press the Start/ Stop button at Main Page. Autopilot will enter into Auto mode.

![](../.gitbook/assets/Screenshot_20210106-204359_Virtuino\[1].jpg)

* Autopilot will fix the course to steer (CTS) to current heading (HDG) value and Status Led will turn on.
* Autopilot will start moving the linear actuator to keep the boat course to CTS value.

![](../.gitbook/assets/Screenshot_20210106-205145_Virtuino\[1].jpg)

* In Auto mode, press Start/ Stop button again to switch back to Stand-by mode. Autopilot will stop moving linear actuator.

> #### Serial I/F $PEMC Code: 00
>
> Serial I/F Sentence: $PEMC,00\*37

## Rudder control

This set of functions allows user to change rudder angle.

{% hint style="info" %}
Rudder control functions are only available in Stand by mode.
{% endhint %}

{% hint style="info" %}
Behaviour will be different depenting on the value of installation parameter`Installation Side` , startboard (`S`) or portboard (`P`).
{% endhint %}

{% hint style="warning" %}
In Fenix V2.0, the value of installation parameter`Installation Side` is always startboard (`S`)
{% endhint %}

> #### Serial I/F $PEMC Code: 01
>
> Serial I/F Sentence example: $PEMC,01,r\*68

### Increment Current Rudder by 1 Position Unit.

Perform a SHORT EXTENSION of the linear actuator to increase current rudder angle.

In Virtuino App,

* In Stand by mode, press +1 button at Main page

![](../.gitbook/assets/Screenshot_20210107-174513_Virtuino\[1].jpg)

> Serial I/F Example: $PEMC,01,i\*xx

### Increment Current Rudder by 10 Position Unit.

Perform a LONG EXTENSION of the linear actuator to increase current rudder angle.

In Virtuino App,

* In Stand by mode, press +10 button at Main page

> Serial I/F Example: $PEMC,01,I\*xx

### Reduce Current Rudder by 1 Position Unit.

Perform a SHORT RETRACTION of the linear actuator to decrease current rudder angle.

In Virtuino App,

* In Stand by mode, press -1 button at Main page

> Serial I/F Example: $PEMC,01,r\*xx

### Reduce Current Rudder by 10 Position Unit.

Perform a LONG RETRACTION of the linear actuator to increase current rudder angle.

In Virtuino App,

* In Stand by mode, press -10 button at Main page

> Serial I/F Example: $PEMC,01,R\*xx

## Control Course to Steer

This set of functions allows user to change Target CTS angle.

> #### Serial I/F $PEMC Code: 02
>
> Serial I/F Sentence example: $PEMC,02,i\*70

### Tacking Starboard

This function allows user to select a 100º turn to starboard, which is the standard value for tacking. This turn requires a second user confirmation to avoid big turns are performed by mistake.

In Virtuino App,

* In Auto mode,

![](../.gitbook/assets/Screenshot_20210109-191725_Virtuino.jpg)

* &#x20;press Tack-Starboard button at CTS page. Next CTS value will be updated, pending user confirmation.

![](../.gitbook/assets/Screenshot_20210109-191734_Virtuino.jpg)



* To start the turn, [activate Next CTS ](user-functions.md#activate-next-course-to-steer-cts)pressing SET CTS button.

![](../.gitbook/assets/Screenshot_20210109-191746_Virtuino.jpg)

### Tacking Portboard

This function allows user to turn 100º to portboard, which is the standard value for tacking.

In Virtuino App,

* In Auto mode, press Tack-Portboard button at CTS page.
* Next CTS value will be updated, pending user confirmation.
* To start the turn, [activate Next CTS ](user-functions.md#activate-next-course-to-steer-cts)pressing SET CTS button.

### Increment CTS by 10º

This function allows user to Increment CTS value in 10º

In Virtuino App at Main panel,

* In Auto mode, &#x20;

![](../.gitbook/assets/Screenshot_20210109-192951_Virtuino.jpg)

* press +10 button. CTS will be increased by 10.

![](../.gitbook/assets/Screenshot_20210109-192958_Virtuino.jpg)

&#x20;

> Serial I/F Example: $PEMC,02,I\*xx

### Increment CTS by 1º

This function allows user to Increment CTS value in 1º

In Virtuino App, follow steps described previously

> Serial I/F Example: $PEMC,02,i\*xx

### Reduce CTS by 1º

This function allows user to Reduce CTS value in 1º

In Virtuino App,In Virtuino App, follow steps described previously

> Serial I/F Example: $PEMC,02,r\*xx

### Reduce CTS by 10º

This function allows user to Reduce CTS value in 10º

In Virtuino App, In Virtuino App, follow steps described previously

> Serial I/F Example: $PEMC,02,R\*xx

### Set Next Course To Steer (CTS)

This function allows user to set Next CTS to a defined value.

In Virtuino App,

* In Auto Mode at CTS panel,

![](../.gitbook/assets/Screenshot_20210109-195127_Virtuino.jpg)

* turn center wheel to point desired Target CTS

![](../.gitbook/assets/Screenshot_20210109-194954_Virtuino.jpg)

* When center wheel is released, Next CTS will be fixed, pending user confirmation.
* To [activate Next CTS ](user-functions.md#activate-next-course-to-steer-cts)press SET CTS button.

![](../.gitbook/assets/Screenshot_20210109-195141_Virtuino.jpg)



![](../.gitbook/assets/Screenshot_20210109-195433_Virtuino.jpg)

### Activate Next Course to Steer (CTS)

This function allows user to change CTS value to Next CTS.&#x20;

#### Activate Next CTS

In Virtuino App,

* at Main panel, in Auto mode&#x20;

![](../.gitbook/assets/Screenshot_20210109-202133_Virtuino.jpg)

* press SET button. CTS value will be set to NEXT CTS value.

![](../.gitbook/assets/Screenshot_20210109-202141_Virtuino.jpg)

![](../.gitbook/assets/Screenshot_20210109-202150_Virtuino.jpg)

Alternative, at CTS panel in Auto mode,

![](../.gitbook/assets/Screenshot_20210109-202236_Virtuino.jpg)

* Press SET CTS button and CTS value will be set to NEXT CTS value

![](../.gitbook/assets/Screenshot_20210109-202242_Virtuino.jpg)

![](../.gitbook/assets/Screenshot_20210109-202249_Virtuino.jpg)

#### Start Track Mode

In Virtuino App,

* When Track is available, TRACK AVAILABLE message is displayed,
* Press TRACK AVAILABLE button at Main page.
* Autopilot will enter into Track mode.

![](<../.gitbook/assets/accept track.jpg>)

## Autopilot monitoring

Autopilot operational status is defined by the following set of parameters,

* `Current Mode: Stand-by (S); Auto (A); Track (T)`
* `Current Rudder Position`
* `Heading Magnetic (HDM)`
* `Course To Steer (CTS) (Magnetic)`
* `Deadband value`

### Get Autopilot information

This function allows user to relinquish Autopilot current operational status.

> **Serial I/F $PEMC Code: 08**
>
> Serial I/F Sentence: $PEMC,08,A\*52

Virtuino App V1.0 provides the following information at Main page,

* `Current Mode:`&#x20;
  * `Green light off: Stand-by (S)`
  * `Green light on: Auto (A) or Track (T)`
* `Rudder Position`
* `HDG: Heading True`
* `Course To Steer (CTS) (True)`
* `Next Course To Steer (CTS) (True)`
* `Track Mode status`
* `Information, Warning and Error messages`

![](../.gitbook/assets/out_course.png)

## Configuration control

{% hint style="info" %}
Most of the funtionalities to manage autopilot configurations are available as of Virtuino Fenix App 5.0.
{% endhint %}

{% hint style="info" %}
Calibration of IMU and linear actuator must be completed before first use.
{% endhint %}

{% hint style="info" %}
Autopilot provides initial default settings, however Installation and Gain Parameters might require customization to specific boat and installation conditions.
{% endhint %}

## Installation Parameters

Installation Parameters are,

* `Centered Tiller Position`
* `Maximum rudder angle`
* `Average Cruise Speed`&#x20;
* `Installation Side: Starboard (S) or Portboard (P)` (always set to Starboard)
* `Rudder Damping`  &#x20;
* `Magnetic Variation`
* `Heading Alignment`
* `Off course alarm angle`

### Set Heading Alignment

When Earth Magnetic North and IMU compass detected North are not aligned due to magnetic disturbances around IMU, this function allows user to adjust Autopilot compass HDG value.

In Virtuino App,

* In Stand by mode,
* Take a **reference of current boat True Heading** using an external known ground reference or an external compass (with this method remember to add Magnetic Variation value).
* In CTS panel,&#x20;
* Set NEXT CTS to referenced boat Heading value (eg. 190 deg).

![](../.gitbook/assets/Screenshot_20251228-195400.png)

* press SET HDG.ALIG button and Compass Calibration Pannel will be displayed

![](../.gitbook/assets/Screenshot_20251228-195334.png)

* Press HDG ALIGNMENT Button and the system will calculate the appropriate value of `Heading Alignment` to match the targeted True Heading (eg. 190 deg).

Autopilot True Heading value will be now pointing to the targeted True Heading value.

* Press the associated Save Button to retain the value for future use.

{% hint style="warning" %}
Virtuino App will not save this value. Press Save Button to retain the Heading Alignment value.
{% endhint %}

### Get and Set Installation Parameters using Virtuino App.

Virtuino App V5.X provides the following information at PID Calibration pannel,

* `Average Speed Over Ground`

![](../.gitbook/assets/Screenshot_20251228-201509_2.png)

Virtuino App V5.X provides the following information at Compass Calibration pannel,

* `Heading Alignment`
* `Magnetic Variation`

<figure><img src="../.gitbook/assets/Screenshot_20251228-202914[1].png" alt="" width="270"><figcaption></figcaption></figure>

Virtuino App V5.X provides the following information at Linear Actuator Calibration pannel,

* `Centered Tiller Position`
* `Maximum rudder angle`  (Always set to 35 deg)
* `Rudder dampling` (Calculated automatically through linear actuator calibration process)

<figure><img src="../.gitbook/assets/Screenshot_20251228-202859[1].png" alt="" width="270"><figcaption></figcaption></figure>

### Save current Installation Parameters

This function allows user to save current Installation Parameters and Linear actuator off-sets in the non-volatile memory for later use.

In each of the Pannels where Installation Parameters are displayed, there is an associated Save Button to save the actual values.&#x20;

When more than one Save button is displayed, use the button beside the associated installation parameters.&#x20;

Once values are saved, will be reused immediately after Power-on Autopilot.

{% hint style="info" %}
Remember to save values for later use
{% endhint %}

### Get, Set and Save Installation Parameters using Serial I/F

This function allows user to relinquish Autopilot current installation parameters.

> **Serial I/F $PEMC Code: 08**
>
> Serial I/F Sentence: $PEMC,08,I\*5A

This function allows user to upload  a new set of Installation Parameters.

> **Serial I/F $PEMC Code: 04**
>
> Serial I/F Example: $PEMC,04,2,40,4,S,3,4.1,33.9,9\*xx

This function allows user to save current values of Installation Parameters.&#x20;

> **Serial I/F $PEMC Code: 11**
>
> Serial I/F Sentence: $PEMC,11,I\*52

{% hint style="info" %}
Remember to save values for later use
{% endhint %}

{% hint style="warning" %}
Fenix V4.0 limitations:&#x20;

`Installation Side` cannot be changed. Always set to Starboard (`S`).
{% endhint %}

## Gain Parameters

Gain Parameters are,

* `Kp`
* `Ki`
* `Kd`
* `Sample Time`  (hardcoded at 100ms)
* `Deadband type: Auto (A) , min (m), max (M)`&#x20;

### Get, Set current Gain Parameters using Virtuino App

Virtuino App V5.0 provides the following information at PID Calibration pannel,

* `Current Gain parameters: KP, KI, KD PID`&#x20;

![](<../.gitbook/assets/Screenshot_20251228-201509 (1).png>)

Virtuino App V5.0 provides the following information at Configuration pannel,

* `Deadband`

<figure><img src="../.gitbook/assets/Screenshot_20251228-192200.png" alt="" width="270"><figcaption></figcaption></figure>

### Get, Set and Save current Gain Parameters using Serial I/F

This function allows user to relinquish Autopilot current Autopilot Gain Parameters.

> **Serial I/F $PEMC Code: 08**
>
> Serial I/F Sentence: $PEMC,08,G\*54

This function allows user to upload  new set of Autopilot Gain Parameters.

> **Serial I/F $PEMC Code: 06**

> Serial I/F Example: $PEMC,06,3,0.11,0.7,1000,m\*xx

{% hint style="info" %}
Remember to save values for later use
{% endhint %}

This function allows user to save current Gain Parameters in the non-volatile memory for later use.

Once values are saved, will be reused immediately after Power-on Autopilot.

> **Serial I/F $PEMC Code: 11**
>
> Serial I/F Sentence: $PEMC,11,G\*5C&#x20;

## Commissioning Functions

{% hint style="info" %}
These functions are only available in Stand-by mode
{% endhint %}

### Start compass calibration

This function allows user to calibrate the internal compass (IMU).

* In Virtuino App, Stand-by mode,
* Access to Compass Calibration through Configuration panel,

![](<../.gitbook/assets/Screenshot_20210109-205045_Virtuino (1).jpg>)

![](../.gitbook/assets/Screenshot_20210109-205059_Virtuino.jpg)

* Press Start Button to launch the calibration process,

![](../.gitbook/assets/Screenshot_20210109-205106_Virtuino.jpg)

* Along calibration, the status of the different sensors will be displayed. Status 3 will represent a sensor fully calibrated.

![](../.gitbook/assets/Screenshot_20210109-205114_Virtuino.jpg)

Follow the calibration procedure described in the screen until all sensors are fully calibrated (All green).

![](../.gitbook/assets/Screenshot_20210109-205217_Virtuino.jpg)

You will have additional time to check X, Y, Z axes and bearing values. Once the time has expired, Save and Exit Buttons will be enabled again.

* Press Save Button.

{% hint style="success" %}
Once the compass is calibrated and values saved, the calibration profile will be reused to get the correct orientation data inmediately after Power-on Autopilot.

If you are satified with the result of the calibration process, press Save Button to be used by the autopilot every time it is powered on.
{% endhint %}

> **Serial I/F $PEMC Code:**&#x20;
>
> **09 (Start IMU Calibration Mode)**
>
> > Serial I/F Sentence: $PEMC,09\*3E

> **11 (Save IMU Calibration Values)**
>
> Serial I/F Sentence: $PEMC,11,I\*52

### Enter/Exit linear actuator calibration mode

This function allows user to enter/ exit linear actuator calibration mode.

In Virtuino App, Stand-by mode,

* From Configuation Panel enter into Linear Actuator Calibration Panel,

![](../.gitbook/assets/Screenshot_20210109-205045_Virtuino.jpg)

![](../.gitbook/assets/Screenshot_20210109-214510_Virtuino.jpg)

* Press Start Button to launch the calibration process,

![](../.gitbook/assets/Screenshot_20210109-214517_Virtuino.jpg)

* Press Extend Button to extend the linear actuator as many times as required until the extension is complete.
* Press Retract Button to retract the linear actuator as many times as required until the retraction is complete.

![](../.gitbook/assets/Screenshot_20210109-214559_Virtuino.jpg)

{% hint style="success" %}
Press the Save Button to save linear actuator off-sets for later use
{% endhint %}

> **Serial I/F $PEMC Code: 10**
>
> Serial I/F Sentence: $PEMC,10\*36

