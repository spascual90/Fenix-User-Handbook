# User functions

## Change mode

### Switch working mode from STAND BY to AUTO

This function allows user to change Autopilot working mode from Stand-by to Auto alternatively.

* Executed in Stand-by mode, Autopilot will switch to Auto mode.
* Executed in Auto mode, Autopilot will switch to Stand-by mode.

{% hint style="info" %}
`Initial CTS` value will be set to Heading value. This is useful for later execution of [Return to initial CTS](user-functions.md#return-to-initial-cts) function.
{% endhint %}

![Virtuino App: Press Execution button at Main page](../.gitbook/assets/screenshot-1584266653119.jpg)

> #### Serial I/F $PEMC Code: 00
>
> Serial I/F Sentence: $PEMC,00\*37

### Enter into Track mode

#### Accept or Reject Autopilot action

Some actions require use confirmation before execution.

![Virtuino App: Press Execution button at Main page to Accept autopilot action](../.gitbook/assets/screenshot-1584266653119.jpg)

## Rudder control

This set of functions allows user to change rudder angle.

{% hint style="info" %}
Rudder control functions are only available in Stand by mode.
{% endhint %}

{% hint style="info" %}
Behaviour will be different depenting on the value of installation parameter`Installation Side` , startboard \(`S`\) or portboard \(`P`\).
{% endhint %}

{% hint style="warning" %}
In Fenix V0.1, the value of installation parameter`Installation Side` is always startboard \(`S`\)
{% endhint %}

> #### Serial I/F $PEMC Code: 01
>
> Serial I/F Sentence example: $PEMC,01,r\*68

### Increment Current Rudder by 1 Position Unit.

Perform a SHORT EXTENSION of the linear actuator to increase current rudder angle.

![Virtuino App: In Stand by mode, press +1 button at Main page](../.gitbook/assets/screenshot-1584266646684.jpg)

> Serial I/F Example: $PEMC,01,i\*xx

### Increment Current Rudder by 10 Position Unit.

Perform a LONG EXTENSION of the linear actuator to increase current rudder angle.

![Virtuino App: In Stand by mode, press +10 button at Main page](../.gitbook/assets/screenshot-1584266631637.jpg)

> Serial I/F Example: $PEMC,01,I\*xx

### Reduce Current Rudder by 1 Position Unit.

Perform a SHORT RETRACTION of the linear actuator to decrease current rudder angle.

![Virtuino App: In Stand by mode, press -1 button at Main page](../.gitbook/assets/screenshot-1584266641595.jpg)

> Serial I/F Example: $PEMC,01,r\*xx

### Reduce Current Rudder by 10 Position Unit.

Perform a LONG RETRACTION of the linear actuator to increase current rudder angle.

![Virtuino App: In Stand by mode, press -10 button at Main page](../.gitbook/assets/screenshot-1584266602456.jpg)

> Serial I/F Example: $PEMC,01,R\*xx

## Control Course to Steer

This set of functions allows user to change CTS angle.

{% hint style="info" %}
If executed in Stand-by mode, Target CTS will be changed and will only take effect once autopilot is in Auto mode.
{% endhint %}

> #### Serial I/F $PEMC Code: 02
>
> Serial I/F Sentence example: $PEMC,02,i\*70

### Increment CTS by 1º

Increment CTS value in 1º

> Serial I/F Example: $PEMC,02,i\*xx

### Increment CTS by 10º

Increment CTS value in 10º

> Serial I/F Example: $PEMC,02,I\*xx

### Reduce CTS by 1º

Reduce CTS value in 1º

> Serial I/F Example: $PEMC,02,r\*xx

### Reduce CTS by 10º

Reduce CTS value in 10º

> Serial I/F Example: $PEMC,02,R\*xx

### Set CTS

Set CTS to a defined value.

![Virtuino App: turn center weel to point target CTS at CTS page](../.gitbook/assets/screenshot-1584266816399.jpg)

### Return to initial CTS

Restore CTS to `Initial CTS` value.

![Virtuino App: press Target CTS button at Main page](../.gitbook/assets/screenshot-1584266673484.jpg)

## Autopilot monitoring

Autopilot operational status is defined by the following set of parameters,

* `Current Mode: Stand-by (S); Auto (A); Track (T)`
* `Current Rudder Position`
* `Heading Magnetic (HDM)`
* `Course To Steer (CTS) (Magnetic)`
* `Deadband value`
* `Trimm`

{% hint style="info" %}
`Fenix V0.1 limitations:`

`Trimm` is not used.
{% endhint %}

### Get Autopilot information

This function allows user to relinquish Autopilot current operational status.

> **Serial I/F $PEMC Code: 08**
>
> Serial I/F Sentence: $PEMC,08,A\*52

Virtuino App V0.1 provides the following information,

* `Current Mode:` 
  * `Green light off: Stand-by (S)`
  * `Green light on: Auto (A) or Track (T)`
* `Current Rudder Position`
* `HDG: Heading Magnetic (HDM)`
* `Course To Steer (CTS) (Magnetic)`

![Main page in Virtuino App](../.gitbook/assets/screenshot-1584266602456.jpg)

## Configuration control

{% hint style="warning" %}
Virtuino App provides limited funtionalities to manage autopilot configurations in Virtuino for Fenix App v0.1. 
{% endhint %}

{% hint style="info" %}
Calibration of IMU and linear actuator must be performed before first use.
{% endhint %}

{% hint style="info" %}
Autopilot provides initial default settings, however Installation and Gain Parameters might require customization to specific boat and installation conditions.
{% endhint %}

## Installation Parameters

Installation Parameters are,

* `Centered Tiller Position`
* `Maximum rudder angle`
* `Average Cruise Speed`
* `Installation Side: Starboard (S) or Portboard (P)`
* `Rudder Damping`
* `Magnetic Variation`
* `Heading Alignment`
* `Off course alarm angle`

### Get Installation Parameters

This function allows user to relinquish Autopilot current installation parameters.

> **Serial I/F $PEMC Code: 08**
>
> Serial I/F Sentence: $PEMC,08,I\*5A

![Gain page in Virtuino App](../.gitbook/assets/screenshot_20200215-114829.png)

* Centered Tiller Position
* Maximum rudder angle
* Average Cruise Speed
* Installation Side
* Rudder Damping
* Magnetic Variation
* Heading Alignment
* Off course alarm angle

### Set Installation Parameters

This function allows user to upload  a new set of Installation Parameters.

{% hint style="warning" %}
Uploaded parameters shall be saved for later use.
{% endhint %}

{% hint style="info" %}
Fenix V0.1 limitations: 

`Installation Side` cannot be changed. Always set to Starboard \(`S`\).

`Average Cruise Speed` is not used.
{% endhint %}



## Gain Parameters

Gain Parameters are,

* `Kp`
* `Ki`
* `Kd`
* `Sample Time`
* `Deadband type: Auto (A) , min (m), max (M)`

### Get current Gain Parameters

This function allows user to relinquish Autopilot current Autopilot Gain Parameters.

> **Serial I/F $PEMC Code: 08**
>
> Serial I/F Sentence: $PEMC,08,G\*54

Virtuino App V0.1 provides the following information,

* Current weight of P, I, D factors in the overal PID output. 
* Current Gain parameters: KP, KI, KD PID 
* Error
* PID Output
* Deadband light: On if current Heading within deadband. 
* Deadband value

![Gain page in Virtuino App ](../.gitbook/assets/screenshot_20200215-114829.png)

### Set Gain Parameters

This function allows user to upload  a new set of Autopilot Gain Parameters.

{% hint style="warning" %}
Uploaded parameters are shall be saved for later use.
{% endhint %}

## Save current Parameters

This function allows user to save current Installation Parameters and Gain Parameters in the non-volatile memory for later use. Linear actuator calibration parameters will also be saved.

Once values are saved, will be reused immediately after Power-on Autopilot.

## Commissioning Functions

{% hint style="info" %}
These functions are only available in Stand-by mode
{% endhint %}

### Start compass calibration

This function allows user to calibrate internal IMU.

### Save compass offsets

This function allows user to save current IMU Calibration Off-sets in the non-volatile memory for later use. 

Once the compass is calibrated and values saved, the calibration profile will be reused to get the correct orientation data immediately after Power-on Autopilot.

### Start linear actuator calibration

### Save linear actuator offsets



