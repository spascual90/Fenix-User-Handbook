# System Specification

1. 
##  Autopilot functionalities by functional modules [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=1)

##  Autopilot Manager [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=2)

Setup,

*  Active Working mode at start-up is:
*  Calibration mode if RCF flag in EEPROM is set to true.
*  Stand-by on the contrary.

Main loop,

*  Obtain Current Bearing from Compass.
*  Obtain Current Rudder position from Linear Actuator.
*  Target Rudder is evaluated depending on the Active Working Mode.
*  Linear Actuator will manage the change from Current Rudder to Target Rudder.

##  Configuration modes [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=3)

###  Calibration mode [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=4)

User has to follow IMU manufacturer procedure to calibrate. IMU selects best offsets.

###  Linear actuator mode [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=5)

User has to follow linear actuator configuration procedure. System takes best values from rudder feedback and saves to EEPROM.

##  Working modes [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=6)

###  Stand-by [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=7)

Target Rudder=Current Rudder.

Autopilot is disengaged.

Saving of Installation parameters and PID gains is allowed.

System can enter into any Calibration mode.

EMEA messages are transmitted and received.

###  Auto [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=8)

When Auto is connected, Trim and Deadband values shall take initial values \(i.e. 0, MIN\_DEATHBAND\) respectivelly.

As PID inputs take,

Setpoint \(SP\) = 0 \(Course to Steer \(CTS\) is considered the 0 reference\)

Process Variable \(PV\) = HDM-CTS \(Heading Magnetic with reference Course to Steer\)

Process Variable \(PV\) shall be an **angle** from -180 to 180

if PV&lt;=180 then PV=PV+360

if PV&gt;180 then PV=PV-360

Error = PV.

###  Deadband and Trim impact in Rudder feedback [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=9)

When Error is smaller than deadband, we can consider that ship is heading to target.

1.  When absolute \(Error\) &lt; deadband,
   1.  Refresh Autotrim value
   2.  Target Rudder = Autotrim value
2.  Else:
   1.  don't refresh Autotrim value
   2.  Target Rudder = Autotrim value + PID \(Error\)

###  Nav [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=10)

Nav Working Mode require minimum data from NMEA messages,

**Reception of Angles**

*  Bearing To next Waypoint \(BTW/BRG\)
*  Turn \(TRN\) - Difference between TRK and BRG \(only used in external compass mode\)
*  Course To Steer \(CTS\) - An average value between BRG and XTE angle. \(only used in external compass mode\)

**Turn calculation:**

In external compass mode, the value might be calculated by OpenPlotter and received as TRN NMEA data.

In internal compass mode, Turn is calculated as the difference between Compass.Heading and BTW/BRG.

###  Wind [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=11)

**TBD**

###  Tack [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=12)

Available in Auto and Wind mode. Changes CTS by 100º.

Requires user confirmation of band \(starboard/ portboard\).

Delay to allow user to prepare the maneuver.

##  PID Control [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=13)

 [![PIDforDummies pid simplified](https://vignette.wikia.nocookie.net/emacua/images/a/aa/PIDforDummies_pid_simplified.png/revision/latest/scale-to-width-down/398?cb=20180204170905)](https://vignette.wikia.nocookie.net/emacua/images/a/aa/PIDforDummies_pid_simplified.png/revision/latest?cb=20180204170905)

The **Setpoint** \(SP\) is the value that we **want** the process to be \(i.e. CTS \(Course to Steer\)\).

The PID controller looks at the setpoint and compares it with the actual value of the **Process Variable \(PV\)** \(i.e. HDM \(Heading Magnetic\)\).

**Error** is the difference between SP and PV.

Error is multiplied by all of the calculated P, I and D Control Actions. Then the resulting Error x Control Actions” are added together and sent to the **Controller Output**.

**Controller direction** is always direct \(i.e. bigger Error shall produce bigger Control Action\).

###  PID Gain [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=14)

 [![Gain](https://vignette.wikia.nocookie.net/emacua/images/5/51/Gain.jpg/revision/latest?cb=20180211192924)](https://vignette.wikia.nocookie.net/emacua/images/5/51/Gain.jpg/revision/latest?cb=20180211192924)

To configure the PID different parameters are defined,

**Kp, Ki, Kd** are the parameters that drives the P, I and D Control Actions respectivelly. The default are \[TBC\]

tbc: **PID method**: Proportional On Measurement or Proporcional On Error.

**Sample Time** determines how often the PID algorithm evaluates. The default is 200mS.

**Output limits** Are the minimum and maximum values the Controller Output can take. These equals to the maximum angle of the rudder \(Installation Parameter **Maximum rudder angle\)**.

##  PID Deadband [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=15)

 [![Seastate](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/2/29/Seastate.jpg/revision/latest?cb=20180211215252)

Deadband is defined as the angle from Average Course to maximum heading deviation caused by periodic forces \(i.e. waves\). Within deadband, actuator shall stay still at Autotrim position.

Deadband goal is to attenuate fluctuations in PID error signal. Using deadband will increase the service life of the actuator.

Is very useful for D-part of PID to avoid extreme output values for small changes \(dx/dt\) in signal.

###  User defined Deadband [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=16)

Deadband can be established by user between MIN\_DEADBAND and MAX\_DEADBAND. Autorim is applied, so Autodeadband shall still be calculated, but not applied. [![Autotrim-0](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/2/2e/Autotrim-0.jpg/revision/latest?cb=20181012193645)

###  Auto deadband [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=17)

Initial Deadband = MIN\_DEADBAND.

Deadband can be automatically calculated as the standard deviation of HDM \(t\) regression line.

Regression line shall be continuosly calculated in periods of 10 seconds.

In case Deadband is bigger than Maximum deadband value, then Deadband = MAX\_DEADBAND..

MIN\_DEADBAND = 1º

MAX\_DEADBAND=20º.

##  AutoTrim [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=18)

 [![Autotrim](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/3/32/Autotrim.jpg/revision/latest?cb=20180211192442)

The AutoTrim setting determines the rate at which the autopilot applies ‘standing helm’ to correct for trim changes caused by varying wind loads on the sails or superstructure.

Note that Autotrim applied to rudder aims to keep boat heading to Course to Steer, not to compensate derive in the route caused by wind and tides.

Consider the Controller Output\(t\) monitored continuosly in periods of 10 seconds.

Autotrim value is the average Controller Output\(t\) calculated when heading the course to steer \(i.e. when absolute \(Error\) &lt; Deathband\),

##  Installation Parameters [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=19)

Different parameters that are dependant on the autopilot installation or the boat design shall be defined.

**Centered Tiller Position**: Indicates the linear actuator position when the tiller is aligned with the hull. This is the 0º reference for Trimming function.

**Maximum rudder angle:** Limit angle of the rudder. It is used to prevent the linear actuator exceeding the rudder angle and damaging the boat. Value 0 referes to Centered Tiller Position.

This value will also be the maximum and -minimum values of the **PID Control.**

**Average Cruise Speed**: is the nominal speed of the boat. Used by the autopilot in Track mode when speed information is not received from external sources.

\(2, 20\). Default: 5.

**Installation Side:** Side of the boat where the linear actuator is installed.

Default: Startboard.

Starboard: Turn to starboard requires extension of the linear actuator from center position. By default.

*  Linear actuator target position = Controller Output

Portboard: Turn to starboard requires retraction of the linear actuator from center position.

*  Linear actuator target position = - Controller Output

**Rudder damping**: Analog error in the linear actuator feedback potenciometer may cause the linear actuator to "hunt" when trying to position. Rudder damping identify error in potenciometer signal \( equals ERROR\_FEEDBACK\).

\(0,10\). Default: 2.

**Magnetic variation**: Level of magnetic variation present at the boat's current position. Used by the autopilot when information is not received from external sources.

\(-45º;+45º\). Default: 0º.

**Heading alignment**: Installation of magnetic compass may not be aligned with boat's steering compass, or a known transit bearing.

\(-180º, 180º\); Default: 0º

**Off course alarm angle:** Angle of Off course alarm. This alarm warns if the AP is unable to maintain its course.

\(10º;30º\). Default: 20º.

##  Linear Actuator [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=20)

Parameters dependant on linear actuator used.

###  Rudder Feedback [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=21)

Linear actuator shall provide a Feedback Signal indicating its position. This feedback is an analog signal provided by a potenciometer integrated into the linear actuator.

###  Feedback Parameters [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=22)

Feedback parameters depends on the specific linear actuator used.

The minimum and maximum position is represented by a value of Position Signal between 0 and 1023. Note that minimum may not be represented by 0 and maximum by 1023.

*  **MIN\_FEEDBACK**: Value of Position Signal in the retracted position \(minimum lenght\).
*  **MAX\_FEEDBACK**: Value of Position Signal in the extended position \(maximum lenght\)

To protect linear actuator mechanism from over usage, it is not recomended to arrive to the built-in limits.

*  **LIMIT\_FEEDBACK**: //Recomended: 1% Position Signal units.

Arriving to the physical limits of the linear actuator may cause early over usage of the mechanisms. To protect linear actuator it is recomended to consider certain margin in the Position Signal before arriving to the max/min feedback.

Centered tiller position and Maximum rudder angle Installation Parameters manage this value.

*  **ERROR\_FEEDBACK**

Feedback is an analogic signal with limited precision. Signal error depends on the characteristics of the potenciometer and the additional noise in the wiring.

This error has to be considered in any evaluation of actuator position.

Recomended: 0,5% Position Signal units. Rudder damping Installation Parameter manages this value.

###  Actuator Controller [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=23)

It requires **2 separate signals** to control the motor, one is for direction \(counterclockwise or clockwise\) and another is for the speed. To control motor direction, DIR pin is connected to HIGH or LOW for different direction, whereas PWM pin is fed with PWM signal to control the motor speed

2 signals are required,

*  **SetDirection**: Extend or retract.

If previousDirection &lt;&gt; currentDirection then Delay \(DELAY\_DIRCHANGE\)

*  **SetSpeed**: Stopped or moving \(at highest speed\) in the direction established by SetDirection.

###  Actuator Parameters [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=24)

To protect linear actuator from high throughput due to change of direction, it is recomended to add a delay before changing direction.

*  **DELAY\_DIRCHANGE**: Delay after change of dir in msec. 500 msec recomended.

###  Linear actuator calibration [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=25)

Linear actuator shall be calibrated to identify specific Feedback Parameters and Actuator Parameters.

##  Compass [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=26)

All information on a chart, including your own plotting, is related to TRUE North. Thus all bearings on a chart are related to TRUE NORTH.

Compass points to MAGNETIC NORTH, which varies from True North by an error called VARIATION \(ES: Declinación magnética o variación local\).

###  Compass Variation and Deviation [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=27)

Note that magnetic compass are also subject to their own errors due to magnetic interferences of metals around; this is called DEVIATION \(ES: Desvío\). [![220px-Magnetic declination.svg](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/7/76/220px-Magnetic_declination.svg.png/revision/latest?cb=20190402153726)

For an state of the art 6DOF IMU, this error is detected and corrected on the fly. For instance, only acelerometer is used when magnetometer is not reliable.

The assumption of this specification is IMU Deviation is 0.

Compass Variation allows to transform angles referred to Magnetic North to True North and viceversa.

TRUE to MAGNETIC: ANGLEM = ANGLET + Dm

    MAGNETIC to TRUE: ANGLET = ANGLEM - Dm

Positive values of Dm means deviation to East.

Negative values of Dm means deviation to West.

###  Heading Alignment [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=28)

The IMU X axis may not be installed directly pointing to the bow. Error angle is called Heading Alignment parameter, and shall be added to IMU heading to get Compass bearing.

COMPASS BEARING = IMU HEADING + HEADING ALIGNMENT

MAGNETIC BEARING = COMPASS BEARING. \(Assumption: IMU Deviation is 0\).

TRUE BEARING = MAGNETIC BEARING + COMPASS VARIATION

Compass function only outputs MAGNETIC BEARING.

###  Tilt compensated IMU heading [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=29)

IMU can provide data in different formats. 

For the purpose of this specification, Vector Euler in Degrees is used. This value is a valid tilt compensated IMU heading.

IMU\_heading = euler.x

###  Calibration [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=30)

Initial calibration of IMU is required before permanent installation into the boat.

BNO055 manufacturer procedure and tools to calibrate and verify are described in the link below.

[https://www.youtube.com/watch?v=Bw0WuAyGsnY](https://www.youtube.com/watch?v=Bw0WuAyGsnY)

**It is very important to follow at least once the calibration, verification and saving procedure described below to get tilt compensated data.**

After successful calibration, autopilot will save the calibration data into Autopilot EEPROM. This data will be recovered each time the Autopilot is started.

Calibration, verification and saving process can be performed as many times as required.

##  Datalogger [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=31)

Data loggin capabilty in order to test the system perfomance and debugging.

Comma separated data in order to import to spreadsheet \(eg Excel\).

Serial data monitoring application can be used \(e.g. Sloeber IDE. Serial Monitor View\)

Binary data in order to provide plotter capabilities \(e.g. Sloeber IDE. Plotter\)

In order to reduce PROGMEM and system performance, Datalogging capabilities shall be switched on/off at compilator level.

##  HMI [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=32)

####  Functions [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=33)

*  Switch working mode from STAND BY to AUTO. Set CTS.
*  Increment Current Rudder by 1 Position Unit. Set STAND BY Mode.
*  Increment Current Rudder by 10 Position Unit Set STAND BY Mode.
*  Reduce Current Rudder by 1 Position Unit Set STAND BY Mode.
*  Reduce Current Rudder by 10 Position Unit Set STAND BY Mode.
*  Increment CTS by 1 Position Unit
*  Increment CTS by 10 Position Unit
*  Reduce CTS by 1 Position Unit
*  Reduce CTS by 10 Position Unit
*  Get Installation Parameters
*  Set Installation Parameters
*  Get PID gain \(inc. sample time and deadband\)
*  Set PID gain \(inc. sample time and deadband\)
*  Get Autopilot information
*  Start compass calibration

####  O. Information from Autopilot: [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=34)

*  Current Mode
*  Current Rudder Position
*  Heading Magnetic \(HDM\)
*  Course To Steer \(CTS\)
*  Deadband value
*  Trimm

####  I/O. PID Gain; [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=35)

*  Kp
*  Ki
*  Kd
*  Sample Time
*  Deadband type \(auto, min, max\)

####  I/O. Installation Parameters: [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=36)

*  Centered Tiller Position
*  Maximum rudder angle
*  Average Cruise Speed
*  Installation Side
*  Rudder Damping
*  Magnetic Variation
*  Heading Alignment
*  Off course alarm angle

####  O. Internal Compass: [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=37)

*  Calibration status

####  O. Buzzer: [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=38)

##  Functionalities by Hardware components [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=39)

 [![Hardware](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/9/9f/Hardware.jpg/revision/latest?cb=20180220222609)

###  Main Module [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=40)

Main Module provides,

*  Processing functions are implemented by ARDUINO MEGA 2560 REV3 microcontroller board.
*  Basic HMI: LCD Keypad and Buzzer
*  Advanced HMI I/F: Bluetooth
*  **\[TBC\]** .

####  ARDUINO MEGA 2560 REV3 [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=41)

[https://store.arduino.cc/arduino-mega-2560-rev3](https://store.arduino.cc/arduino-mega-2560-rev3) [![A000067 iso ](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/2/2e/A000067_iso_.jpg/revision/latest?cb=20180226210315)

####  LCD Keypad [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=42)

[https://www.prometec.net/lcd-keypad-shield/](https://www.prometec.net/lcd-keypad-shield/) [![Arduino Shield8](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/1/1e/Arduino_Shield8.png/revision/latest?cb=20180226204751)

####  Bluetooth BT-HC06 [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=43)

[https://www.prometec.net/bt-hc06/](https://www.prometec.net/bt-hc06/) [![Hc-06](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/8/8f/Hc-06.jpg/revision/latest?cb=20180226211229)

####  Buzzer [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=44)

**\[TBC\]**

###  Motor Controller [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=45)

 [![Motor controller](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/5/5b/Motor_controller.png/revision/latest?cb=20180212231643)

Linear actuator is driven by a PWM motor controller in **Sign-magnitude mode.**

Main characteristics of Cytron 13A, 5-30V Single DC Motor Controller,

*  Designed to drive high current brushed DC motor up to 13A continuously
*  Bi-directional control for 1 brushed DC motor
*  Support motor voltage ranges from 5V to 30V
*  Full NMOS H-Bridge for better efficiency and no heat sink is required.

###  Motor [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=46)

 [![Motor](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/0/0f/Motor.png/revision/latest?cb=20180212223117)

###  Actuator potenciometer [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=47)

 Position Signal is an analogic signal from a potenciometer integrated into the linear actuator. [![Potentiometer](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/5/50/Potentiometer.png/revision/latest?cb=20180206213502)

###  IMU [![](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)Edit](https://emacua.fandom.com/wiki/System_Specification?action=edit&section=48)

MCU+9DOF BNO055 Intelligent 9-axis CJMCU-055 attitude sensor module is used.

[https://learn.adafruit.com/adafruit-bno055-absolute-orientation-sensor/overview](https://learn.adafruit.com/adafruit-bno055-absolute-orientation-sensor/overview) [![IMU](data:image/gif;base64,R0lGODlhAQABAIABAAAAAP///yH5BAEAAAEALAAAAAABAAEAQAICTAEAOw%3D%3D)](https://vignette.wikia.nocookie.net/emacua/images/4/43/IMU.png/revision/latest?cb=20180212223813)

This unit provides tilt compensated heading **when properly calibrated** and installed without need to perfom complex calculations.

