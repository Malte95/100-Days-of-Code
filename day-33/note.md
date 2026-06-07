Today I completed the following coding challenges:

**The Goal:**

Move my Arduino landing gear simulator from pure planning into the first real embedded code structure by implementing pin configuration, analog sensor reading, speed mapping, button handling, and the foundation of a finite state machine.

A valid solution must meet these requirements:

-Define all hardware pins as reusable constants.

-Configure digital inputs and outputs correctly inside `setup()`.

-Read analog potentiometer values and convert them into simulated aircraft speed.

-Detect a single button press reliably using edge detection.

-Prepare a state-machine architecture for landing gear movement and safety logic.

**My Approach:**

**1.Hardware Pin Abstraction:**
I defined named constants for all connected components, including the button, LEDs, servo, and potentiometer. This makes the code easier to maintain because pin numbers can be changed in one place instead of being hardcoded throughout the program.

**2.Setup Configuration:**
I created the first real `setup()` structure. The button is configured with `INPUT_PULLUP`, while the red, yellow, and green LEDs are configured as outputs. This introduced the difference between hardware configuration and runtime reading.

**3.Analog Sensor Mapping:**
I learned why the potentiometer does not normally need `pinMode()`: it is read through `analogRead()` on an analog input. I then mapped the raw potentiometer range from `0–1023` into a simulated airspeed range of `0–250 knots` using `map()`.

**4.Finite State Machine Foundation:**
I introduced an `enum GearState` with multiple landing gear states: `GEAR_RETRACTED`, `GEAR_EXTENDING`, `GEAR_EXTENDED`, `GEAR_RETRACTING`, and `GEAR_FAULT`. This creates the foundation for a realistic embedded state machine instead of simple binary gear logic.

**5.Non-Blocking Movement Variables:**
I added timing and motion variables such as `stepSize`, `moveInterval`, `lastMoveTime`, `gearAngle`, and `gearTargetAngle`. These prepare the system for smooth non-blocking gear movement using `millis()` instead of `delay()`.

**6.Button Edge Detection:**
I implemented the first version of button press detection using `buttonState` and `lastButtonState`. By checking for a transition from `HIGH` to `LOW`, the system can detect one intentional button press instead of repeatedly triggering while the button is held down.

**7.Safety Logic Preparation:**
I connected the potentiometer-derived `speedKnots` value to the future landing gear safety system. This prepares the simulator for rules such as blocking gear retraction when the aircraft speed is below a defined threshold.

**8.Embedded Systems Progress:**
Today’s work marked the transition from theory into actual Arduino architecture. I now have the first working foundation for an event-driven embedded landing gear controller with hardware abstraction, state management, analog input processing, and reliable button handling.

