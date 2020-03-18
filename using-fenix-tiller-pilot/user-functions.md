# User functions

## Change mode

### Switch working mode from STAND BY to AUTO

This function allows user to change Autopilot working mode from Stand-by to Auto alternatively.

* Executed in Stand-by mode, Autopilot will switch to Auto mode.
* Executed in Auto mode, Autopilot will switch to Stand-by mode.

![Virtuino App: Press Execution button at Main page](../.gitbook/assets/screenshot-1584266653119.jpg)

> #### Serial I/F $PEMC Code: 00
>
> Serial I/F Sentence: $PEMC,00\*37

{% hint style="info" %}
`Initial CTS` value will be set to Heading value. This is useful for later execution of [Return to initial CTS](user-functions.md#return-to-initial-cts) function.
{% endhint %}

### Enter into Track mode

#### Accept or Reject Autopilot action

Some actions require use confirmation before execution.

In Virtuino App,

* Press Execution button at Main page to Accept autopilot action

![](../.gitbook/assets/screenshot-1584266653119.jpg)

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

In Virtuino App,

* In Stand by mode, press +1 button at Main page

![](../.gitbook/assets/screenshot-1584266646684.jpg)

> Serial I/F Example: $PEMC,01,i\*xx

### Increment Current Rudder by 10 Position Unit.

Perform a LONG EXTENSION of the linear actuator to increase current rudder angle.

In Virtuino App,

* In Stand by mode, press +10 button at Main page

![Virtuino App: In Stand by mode, press +10 button at Main page](../.gitbook/assets/screenshot-1584266631637.jpg)

> Serial I/F Example: $PEMC,01,I\*xx

### Reduce Current Rudder by 1 Position Unit.

Perform a SHORT RETRACTION of the linear actuator to decrease current rudder angle.

In Virtuino App,

* In Stand by mode, press -1 button at Main page

![](../.gitbook/assets/screenshot-1584266641595.jpg)

> Serial I/F Example: $PEMC,01,r\*xx

### Reduce Current Rudder by 10 Position Unit.

Perform a LONG RETRACTION of the linear actuator to increase current rudder angle.

In Virtuino App,

* In Stand by mode, press -10 button at Main page

![](../.gitbook/assets/screenshot-1584266602456.jpg)

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

This function allows user to Increment CTS value in 1º

In Virtuino App,

* Auto or Track mode, press +1 button at Main page
* Stand-by mode, press +1 button at CTS page

![](../.gitbook/assets/screenshot-1584266816399.jpg)

> Serial I/F Example: $PEMC,02,i\*xx

### Increment CTS by 10º

This function allows user to Increment CTS value in 10º

In Virtuino App,

* Auto or Track mode, press +10 button at Main page
* Stand-by mode, press +10 button at CTS page

> Serial I/F Example: $PEMC,02,I\*xx

### Reduce CTS by 1º

This function allows user to Reduce CTS value in 1º

In Virtuino App,

* Auto or Track mode, press -1 button at Main page
* Stand-by mode, press -1 button at CTS page

> Serial I/F Example: $PEMC,02,r\*xx

### Reduce CTS by 10º

This function allows user to Reduce CTS value in 10º

In Virtuino App,

* Auto or Track mode, press -10 button at Main page
* Stand-by mode, press -10 button at CTS page

> Serial I/F Example: $PEMC,02,R\*xx

### Set CTS

This function allows user to set CTS to a defined value.

Virtuino App,

* turn center wheel to point desired target CTS at CTS page

![](../.gitbook/assets/screenshot-1584266816399.jpg)

### Return to initial CTS

This function allows user to set CTS to `Initial CTS` value.

Virtuino App,

* press Target CTS button at Main page

![](../.gitbook/assets/screenshot-1584266673484.jpg)

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

Virtuino App V0.1 provides the following information at Main page,

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
Calibration of IMU and linear actuator must be completed before first use.
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

Virtuino App V0.1 provides the following information at Gain page,

* `Centered Tiller Position`

![Gain page in Virtuino App](../.gitbook/assets/screenshot_20200215-114829.png)

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

Virtuino App V0.1 provides the following information at Gain page,

* `Current weight of P, I, D factors in the overal PID output.` 
* `Current Gain parameters: KP, KI, KD PID` 
* `Error`
* `PID Output`
* `Deadband light: On if current Heading within deadband.` 
* `Deadband value`

![Gain page in Virtuino App ](../.gitbook/assets/screenshot_20200215-114829.png)

### Set Gain Parameters

This function allows user to upload  new set of Autopilot Gain Parameters.

> **Serial I/F $PEMC Code: 06**

> Serial I/F Example: $PEMC,06,3,0.11,0.7,1000,m\*xx

{% hint style="warning" %}
Uploaded parameters are shall be saved for later use.
{% endhint %}

### Save current Gain Parameters

This function allows user to save current and Gain Parameters in the non-volatile memory for later use.

Once values are saved, will be reused immediately after Power-on Autopilot.

> **Serial I/F $PEMC Code: 11**
>
> Serial I/F Sentence: $PEMC,11,G\*5C

## Commissioning Functions

{% hint style="info" %}
These functions are only available in Stand-by mode
{% endhint %}

### Start compass calibration

This function allows user to enter into IMU calibration mode.

### Save compass offsets

This function allows user to save current IMU Calibration Off-sets in the non-volatile memory for later use. 

Once the compass is calibrated and values saved, the calibration profile will be reused to get the correct orientation data inmediately after Power-on Autopilot.

> **Serial I/F $PEMC Code: 11**
>
> Serial I/F Sentence: $PEMC,11,I\*52

### Start linear actuator calibration

This function allows user to enter/ exit linear actuator calibration mode.

> **Serial I/F $PEMC Code: 10**
>
> Serial I/F Sentence: $PEMC,10\*36

{% hint style="success" %}
Save linear actuator parameters as part of Installation Parameters.
{% endhint %}



