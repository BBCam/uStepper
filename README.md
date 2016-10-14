# uStepper

The library contains support for driving the stepper, measuring temperature and reading out encoder data. Two examples are included to show the functionality of the library.
The library is supported in Arduino IDE 1.6.7, 1.6.8, 1.6.9, 1.6.10, 1.6.11, 1.6.12.

For more information, visit www.ustepper.com

## Closed loop is now implemented !
We have (for quite some time now) been working on closed loop control of the uStepper motors, and we have finally made it work ! Two modes of control has been implemented.
The first mode is the drop-in feature, which takes in step/dir/enable pulses from a 3d printer/cnc controller, and moves the motor based on these pulses, correcting for any missed steps in the process.
The second mode is for regular movement functions, such as "moveSteps()", and works just as it have always worked, with the addition of correcting, should any steps be missed.
We have supplied some standard PID parameters, however these parameters will most likely need to be custom tuned to your specific application. The parameters provided works well with our Prusa I3 3d printer, but it will vary greatly between different setups !

## Documentation
Documentation for the uStepper library can be found at the following URL:
http://ustepper.com/docs/html/index.html

To add hardware support for uStepper in the Arduino IDE (1.6.xx) do the following:
 - Open Arduino
 - Open preferences
 - Almost at the bottom there is a field stating: "Additional Boards Manager URLs" insert this url: https://raw.githubusercontent.com/uStepper/uStepper/master/package_ustepper_index.json
 - Press OK
 - Go into tools -> Boards and press "Boards Manager"
 - Go to the bottom (after it has loaded new files) select "uStepper by ON Development IVS" and press install

You have now added uStepper hardware support and should be able to select uStepper under tools -> boards.

To add the uStepper library do the following:
- Go to Sketch->Include Libraries->Manage Libraries... in the arduino IDE
- Search for "uStepper", in the top right corner of the "Library Manager" window
- Install uStepper library 
 
MAC users should be aware, that OSX does NOT include FTDI VCP drivers, needed to upload sketches to the uStepper, by default. This driver should be downloaded and installed from FTDI's website:
	
	http://www.ftdichip.com/Drivers/VCP.htm

The uStepper should NOT be connected to the USB port while installing this driver !
This is not a problem for windows/linux users, as these drivers come with the arduino installation.

## Change Log
1.0.0:

- Added PID functionality to drop-in Feature
- Added PID functionality to regular movement functions
- Added support for servo motors
- Added two new examples

0.4.5:

- Changed setup of Timer1 and Timer2, to allow for PWM generation on D3 and D8. See documentation of "pwmD3()" and "pwmD8()" functions in class "uStepper", for instructions.
- Changed setup of external interrupts for dropin feature, to be able to compile with arduino IDE 1.6.10.
- Updated board installation package to version 1.1.0, to be compliant with arduino IDE 1.6.10. Update uStepper board using package manager in Arduino IDE ("Tools->Board->Board Manager", scroll down to the uStepper board and choose update or install).

0.4.4:

- Added the attribute "used" to declarations of interrupt routines. This enables the library to be compiled in Arduino IDE 1.6.10
- Updated documentation of "uStepper::setup()"

0.4.3:

- Fixed bug where initial deceleration phase (used when changing speed setting or changing direction while motor is moving), would never be entered, causing motor to accelerate

0.4.2:
- Fixed bug with setHome() causing getAngleMoved() to return alternating values (offset by exactly 180 degrees) between resets.
- Fixed bug in runContinous(), where direction of the motor did not get updated if the function was called with the motor standing still.

0.4.1:

- Fixed bug with getAngleMoved() returning alternating values (offset by exactly 180 degrees) between resets.
- Added keywords
- Updated pin connection description for Drop-in example 

0.4.0:

- Added Drop-in feature to replace stepsticks with uStepper for error correction
- Fixed bug in stepper acceleration algorithm, making the motor spin extremely slow at certain accelerations. Also this fix reduced the motor resonance
- Implemented an IIR filter on the speed measurement, to smooth this out a bit.

0.3.0:

- Added support for speed readout
- Added support for measuring the shaft position with respect to a zero reference. (absolute within multiple revolutions)

0.2.0:

- Complete rewrite of the stepper algorithm in assembler
- Changed from fixed point to floating point variables, due to the need for more precision
- Removed the getSpeed() method, as it didn't work, and therefore it would make more sense to remove it
  and re-add it when i get the time to fix it
- Added a few doxygen comments
- Added a new method (getStepsSinceReset()), which returns all steps performed since reset of the uStepper.
  positive values corresponds to steps in clockwise direction, while negative values corresponds to steps
  in counterclockwise direction.	

0.1.0:	

- Initial release

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">uStepper</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="www.ustepper.com" property="cc:attributionName" rel="cc:attributionURL">ON Development</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
