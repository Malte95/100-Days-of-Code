Today I completed the following embedded systems development tasks:

**The Goal:**

Continue improving the landing gear simulator by preparing the airspeed subsystem for hardware integration and implementing a visual warning system for blocked landing gear retraction commands.

A valid solution must meet these requirements:

-Refactor airspeed handling into a dedicated function.

-Provide clean and efficient airspeed debugging output.

-Implement a warning system when gear retraction is blocked due to insufficient airspeed.

-Provide visual feedback without entering a fault state.

-Maintain the existing state machine architecture and non-blocking design.

**My Approach:**

**1.Refactored Airspeed Handling:**
I extracted the airspeed processing logic from `readInputs()` into a dedicated `updateAirspeed()` function. This improves separation of responsibilities and makes the code easier to maintain as additional airspeed-related features are added in the future.

**2.Prepared Potentiometer Integration:**
The new airspeed function now reads the potentiometer value using `analogRead()`, converts it into a simulated airspeed value using `map()`, and stores the result in `speedKnots`. This prepares the project for the next hardware integration phase.

**3.Improved Debugging Output:**
To prevent the Serial Monitor from being flooded with repeated values, I introduced a `lastSpeedKnots` variable and implemented change detection. Airspeed values are now only printed when the speed actually changes, making debugging significantly cleaner and more useful.

**4.Reviewed Landing Gear Safety Logic:**
I revisited the speed-based landing gear protection system and clarified the intended behavior:

* Gear extension is always allowed.
* Gear retraction is only allowed when airspeed exceeds the minimum threshold.
* Retraction attempts at insufficient speed are blocked.

This ensures the simulator behaves according to the intended operational rules.

**5.Designed a Dedicated Warning System:**
Instead of treating a blocked retraction command as a system fault, I implemented a dedicated warning mechanism. This distinguishes operational restrictions from actual failures and keeps the fault-management system reserved for genuine system problems.

**6.Added Warning State Variables:**
I introduced the variables required to support temporary warning indications, including:

* Warning activation flag
* Warning timer
* Warning blink timer
* LED blink state tracking

These variables provide the foundation for time-based warning behavior without blocking the main loop.

**7.Implemented Non-Blocking Warning Timing:**
The warning system uses `millis()`-based timing to automatically clear the warning after a configurable duration. This preserves the project's non-blocking architecture and allows the controller to remain responsive while warnings are active.

**8.Created Visual Retract-Blocked Indication:**
I implemented a new LED behavior for blocked retraction attempts:

* Green LED remains on to indicate the gear is still extended.
* Yellow LED blinks to indicate a warning condition.
* Red LED remains off.

This provides immediate visual feedback while accurately representing the actual landing gear state.

**9.Expanded Embedded System Architecture:**
The project now contains separate mechanisms for:

* Normal operation
* Gear movement indication
* Fault handling
* Fault recovery
* Airspeed monitoring
* Operational warnings

This represents another step toward a more realistic embedded control system where operational restrictions and system failures are handled independently.

**10.Preparation for Future Hardware Testing:**
All software components required for airspeed monitoring and blocked-retraction warnings are now in place. The next step will be to reconnect the potentiometer, validate the speed calculations on hardware, and test the complete warning system under real operating conditions.

