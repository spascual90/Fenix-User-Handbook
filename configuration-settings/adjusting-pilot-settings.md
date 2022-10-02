# Adjusting Pilot Settings

## Introduction

The tiller pilot has hardcoded settings to provide stable performance for most boats.

However, you can fine tune many of the autopilot features to match your personal preferences, and the type of boat and steering system.

{% hint style="info" %}
You should carry out an initial sea trial before adjusting any of the parameters.
{% endhint %}

You might need to adjust the tiller pilot settings if:

* the pilot does not maintain a selected heading
* the rudder activity is too high or the course keeping is not tight enough
* you wish to change the Off Course alarm angle&#x20;

The [Set Installation Parameters](../using-fenix-tiller-pilot/user-functions.md#set-installation-parameters) function allows you to adjust the following parameters from their factory default settings:

* `Centered Tiller Position`
* `Maximum rudder angle`
* `Installation Side`
* `Rudder Damping`
* `Magnetic Variation`
* `Heading Alignment`
* `Off course alarm angle`

The [Set Gain Parameters](../using-fenix-tiller-pilot/user-functions.md#set-gain-parameters) function allows you to adjust the following parameters from their factory default settings:

* `Kp`
* `Ki`
* `Kd`
* `Deadband type`

{% hint style="info" %}
`Average Cruise Speed and Sample Time are not available in Fenix V0.1`
{% endhint %}

## Setting Parameters

The following steps have to be executed in sequence to change any setting value.

All settings can be changed using the Serial I/F.

{% hint style="info" %}
Here you can find a [guide on Serial I/F communications](../using-fenix-tiller-pilot/untitled.md#checksum)
{% endhint %}

#### To change Installation Parameters&#x20;

{% hint style="info" %}
Installation parameters can be set in Stand-by mode only.
{% endhint %}

1. [get current setting values](../using-fenix-tiller-pilot/user-functions.md#get-installation-parameters)
2. [set new setting values](../using-fenix-tiller-pilot/user-functions.md#set-installation-parameters)
3. [save settings](../using-fenix-tiller-pilot/user-functions.md#save-current-installation-parameters)

#### To change Gain Parameters

1. [get current setting values](../using-fenix-tiller-pilot/user-functions.md#get-current-gain-parameters)
2. [set new setting values](../using-fenix-tiller-pilot/user-functions.md#set-gain-parameters)
3. [save settings](../using-fenix-tiller-pilot/user-functions.md#save-current-gain-parameters)

## Installation Parameters

### Centered Tiller Position

Indicates the linear actuator position when the tiller is aligned with the hull.

### Maximum rudder angle

Limit maximum angle of the rudder. It is used to prevent the linear actuator exceeding the rudder angle and damaging the boat. Value 0 reference to Centered Tiller Position.

{% hint style="info" %}
This value will also be the maximum value of the PID Control output**.**
{% endhint %}

### Installation Side

Side of the boat where the linear actuator is installed.

* [x] S - Starboard
* [ ] P - Portboard

{% hint style="warning" %}
Fenix V0.1 limitation: `Installation Side`is always STARBOARD (`S`)
{% endhint %}

### Rudder Damping

Error in the linear actuator feedback potenciometer may cause the linear actuator to "hunt" when trying to fix a position. Rudder damping identify accepted maximum error in potenciometer signal.

(0 to any positive value). Default: 5º

### Magnetic Variation

Level of magnetic variation present at the boat's current position.

Compass Variation allows to transform angles referred to Magnetic North to True North and viceversa.

Positive values means variation to East.

Negative values of means variation to West.

(-45º;+45º). Default: 0º.

{% hint style="warning" %}
Fenix V0.1 limitation: Since external compass feature is not implemented, this parameter is always used by the Autopilot, even when information is received from external sources.
{% endhint %}

### Heading Alignment

Installation of Autopilot internal IMU (electronic magnetic compass) may not be aligned with boat's steering compass, or a known transit bearing.

(-180º, 180º); Default: 0º

### Off course alarm angle

Angle of Off course alarm. This alarm warns if the Autopilot is unable to maintain its course.

(10º;30º). Default: 20º.

## Gain Parameters

### Kp Ki Kd

These 3 parameters define the behaviour of the Autopilot in Auto and Track modes.

Behaviour and tunning of these parameters are defined in this video.

{% embed url="https://youtu.be/drYO60z6_h4" %}



### Deadband

Deadband is defined as the angle from Average Course to maximum heading deviation caused by periodic forces (i.e. waves). Within deadband, actuator shall stay still.

Deadband goal is to attenuate fluctuations in linear actuator position. Using deadband will increase the service life of the actuator.

{% hint style="info" %}
Is very useful for D-part of PID to avoid extreme output values for small changes (dx/dt) in signal.
{% endhint %}

User can select different Deadband options:

* [x] MIN\_DEADBAND: Fixed to minº
* [x] MAX\_DEADBAND: Fixed to MAXº
* [x] AUTO DEADBAND : Based on sea state, autopilot will adapt deadband angle between min and MAX. This value will be recalculated periodically.

{% hint style="info" %}
If gain parameters are saved, Gain type will be saved and applied per default in the next Autopilot power-on.
{% endhint %}
