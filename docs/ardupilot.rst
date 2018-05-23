Ardupilot
===============

.. contents::

This section documents any CUAir specific uses of or changes to Ardupilot

Tuning
----------------

Rolling Takeoff
^^^^^^^^^^^^^^^

Before attempting to set parameters, determine landing gear style and stall speed of the aircraft. For information on specific takeoff and landing parameters, see http://ardupilot.org/plane/docs/flight-features.html For complete parameter list, see http://ardupilot.org/plane/docs/parameters.html

If plane is a taildragger (like Bixler)::

	TKOFF_TDRAG_ELEV, 	100
	TKOFF_TDRAG_SPD1,	<just below TKOFF_ROTATE_SPD>
	TKOFF_ROTATE_SPD, 	<110-130% of stall speed>
	TKOFF_THR_SLEW,		<minimum of 20>
	TKOFF_FLAP_PCNT,	0
	TECS_PITCH_MAX,		20
	GROUND_STEER_ALT,	5


If plane has tricylce landing gear::

	TKOFF_TDRAG_ELEV, 	0
	TKOFF_TDRAG_SPD1,	0
	TKOFF_ROTATE_SPD, 	<110-130% of stall speed>
	TKOFF_THR_SLEW,		<minimum of 20>
	TKOFF_FLAP_PCNT,	50
	TECS_PITCH_MAX,		22
	GROUND_STEER_ALT,	5
	

To tune ground steering, test in mode FBWA. 

Landing
^^^^^^^^

If plane is a taildragger (like Bixler)::

	LAND_FLARE_ALT, 	0
	LAND_FLARE_SEC,		1.2
	LAND_PITCH_CD, 		<slightly above natural pitch of aircraft - 500 for Bix>
	TECS_LAND_ARSPD,	<above stall speed - 8 for Bix>
	TECS_LAND_SPDWGT,	1


If plane has tricylce landing gear::

	LAND_FLARE_ALT, 	0
	LAND_FLARE_SEC,		2
	LAND_PITCH_CD, 		500
	TECS_LAND_ARSPD,	<above stall speed>
	TECS_LAND_SPDWGT,	1
	

To ensure a smooth descent, LAND_PF_ARSPD (a pre-flare descent parameter) must be set to a higher value than TECS_LAND_ARSPD. 
Additional note: the parameter settings as they appear here were determined to be appropriate for a general airframe in these two landing gear types. If setting parameters for non-standard airframe, further consideration is required. 
	
	
Failsafe
---------

The competition rules specify the following rules for failsafe:

	* After 30 seconds: Return to Launch
	* After 3 minutes: Terminate flight

These events are required to occur upon loss of the primary communications link, which for CUAir 2015-16 is the transmitter. The first requirement is accomplished through the standard failsafe, the second is accomplished through the advanced failsafe.

Standard Failsafe
^^^^^^^^^^^^^^^^^

The competition rules require that the plane executes an RTL after 30 seconds of lost primary communications link. For CUAir 2015-16, this is the transmitter. The included parameters include an additional failsafe that cause the plane to CIRCLE after 2 seconds of lost transmitter signal ONLY if it was in a manual control mode when the transmitter loss ocurred, then RTL in 30 seconds.

Throttle Failsafe Setup
########################

The standard failsafe uses the throttle input channel of the transmitter to determine if it has lost transmitter signal. If the receiver loses connection to the transmitter, it will begin outputting the lowest throttle stick value. To make throttle failsafe work, we need to ensure that what the receiver thinks that the lowest throttle stick value is is lower than the actual low throttle stick on the transmitter. This way, if the transmitter fails the receiver will output a value lower than it ever would if the transmitter was on, and Ardupilot will take that as a signal to initiate the failsafe.

`Read this document <http://ardupilot.org/plane/docs/apms-failsafe-function.html>`_ for more information and generic setup instructions.

Setup instructions:

1. Set the low point of the throttle on the transmitter (Should be Channel 3, but check on Mission Planner's Radio Calibration page) to extend below -100%

	* If this is not possible, set it to its lowest possible value

2. Bind the transmitter with the receiver

	* For the ezUHF receiver, follow the instructions in the "binding" section `here <http://www.immersionrc.com/downloads/manuals/EzUHFManual_EN_v1.0.pdf>`_ 

3. Set the low point of the throttle back to its original value. If you ever need to bind the transmitter again for any reason, you will need to repeat the setup process

	* If it was not possible to set the throttle beyond -100%, then at this step set it to a higher value such as -90%. If this is necessary, DO NOT turn on the plane's throttle until you finish these instructions completely, or the throttle will activate while the stick is down

4. Do the radio calibration in mission planner to tell Ardupilot what the new range of the throttle is. Once this is done, record the low point of the throttle stick while the transmitter is on. Afterwards, turn the transmitter off and ensure that that value drops.

	* If it does not drop, it is possible that the failsafe levels of the receiver need to be set. Set the transmitter back to the low point, then while the receiver is on and the throttle is down, hold the button on the back of the transmitter. Then repeat from step 3

5. Set the THR_FS_VALUE to a value between the throttle down point and the transmitter off point you recorded in step 4. A value somewhere in the middle is good - not too close to either endpoint to account for some variation.
6. Set THR_FAILSAFE to 1 to enable the failsafe
7. Ensure the other parameters are set as below

Standard Failsafe Configuration
################################

For the standard failsafe to function as described, complete the above setup instructions then set the parameters as shown below.::

	THR_FS_VALUE, 		<SEE ABOVE - in range 925-1100>
	THR_FAILSAFE,		1
	FS_SHORT_ACTN, 		0
	FS_SHORT_TIMEOUT,	2
	FS_LONG_ACTN,		1
	FS_LONG_TIMEOUT,	30
	FS_BATT_VOLTAGE,	0
	FS_BATT_MAH,		0
	FS_GCS_ENABL,		0


Advanced Failsafe
^^^^^^^^^^^^^^^^^

**Disabling the failsafe**
##########################

To disable the failsafe, set AFS_ENABLE to 0. This **MUST** before done within 3 minutes of transmitter communications loss.

**AERODYNAMIC TERMINATION IS UNRECOVERABLE - ONCE TERMINATION BEGINS 3 MINUTES AFTER TRANSMITTER LOSS, IT CANNOT BE ABORTED.**

Advanced Failsafe Configuration
################################

***Important:*** If these parameters are set as above, the plane **will** terminate after 3 minutes of lost transmitter signal. Make absolutely sure you know what you are doing when use this failsafe system. Aerodynamic termination WILL result in a crash and is UNRECOVERABLE once activated.

This is the failsafe system that causes flight termination after 3 minutes of transmitter loss. This system works through the throttle failsafe as shown above, so the throttle failsafe needs to be set up correctly for this to work. The AFS parameters should be set as follows to comply with competition rules::

	AFS_WP_COMMS, 		0
	AFS_WP_GPS_LOSS,	0
	AFS_TERM_ACTION, 	42
	AFS_AMSL_ERR_GPS, 	100
	AFS_QNH_PRESSURE, 	0
	AFS_ENABLE, 		1
	AFS_MAX_GPS_LOSS, 	0
	AFS_MAX_COM_LOSS, 	0
	AFS_GEOFENCE, 		0
	AFS_RC,      		1
	AFS_RC_MAN_ONLY,	0
	AFS_DUAL_LOSS,		0
	AFS_RC_FAIL_TIME, 	180


The AFS_TERM_ACTION parameter is the final safeguard between terminating the plane and doing nothing when the flight termination condition is met. It should **never** be 42 unless you are absolutely sure you want the plane to terminate when the transmitter link has been lost for 3 minutes. For test flights, it should always be at 0 - the only time it should be 42 is during competition.
	
See the `AFS documentation <http://ardupilot.org/plane/docs/advanced-failsafe-configuration.html>`_ and the `AFS parameter list <http://ardupilot.org/plane/docs/parameters.html#afs-parameters>`_ for more information.
