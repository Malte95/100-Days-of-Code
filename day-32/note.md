Today I completed the following coding challenges:

**The Goal:**
Continue developing my first Arduino-based aircraft landing gear simulator by moving from system planning toward hardware architecture, pin configuration, input handling, and non-blocking timing concepts.

A valid solution must meet these requirements:

-Define clear pin constants for all connected hardware components.

-Understand the difference between digital inputs, analog inputs, and outputs.

-Prepare the first setup() structure for initializing buttons, LEDs, servo hardware, and future display components.

-Learn how reliable button input works using INPUT_PULLUP and stable default pin states.

-Understand why millis() is preferred over delay() for realistic embedded movement control.

**My Approach:**

**1.Pin Constant Architecture:**
I learned why hardware pin numbers should be stored in named constants instead of being hardcoded throughout the program. By using variables such as buttonPin, redLedPin, servoPin, and potentiometerPin, the project becomes easier to maintain if the wiring changes later.

**2.Hardware Mapping and Naming Convention:**
I created the first hardware pin map for the landing gear simulator. The planned setup includes a button on a digital pin, multiple LED status indicators, a servo output, and a potentiometer connected to an analog input. I also learned the importance of naming pins clearly, such as using servoPin instead of just servo.

**3.Input and Output Classification:**
I classified each hardware component by its role in the system. Buttons and potentiometers act as inputs because they provide information to the Arduino, while LEDs and servos are outputs because the Arduino controls their behavior.

**4.Digital Input Stability and INPUT_PULLUP:**
I learned why a normal input pin can become unstable if it is not clearly connected to HIGH or LOW. This introduced the concept of a floating input, where the Arduino may randomly read HIGH or LOW because of electrical noise. To solve this, I learned how INPUT_PULLUP creates a stable default state.

**5.Button Logic with Pull-Up Resistors:**
I understood the inverted logic used by INPUT_PULLUP: when the button is not pressed, the Arduino reads HIGH, and when the button is pressed, it reads LOW. This is an important embedded-systems concept that will be needed for reliable button control.

**6.First setup() Planning:**
I began planning the initial Arduino setup() structure. The button will be configured using INPUT_PULLUP, the LEDs will be configured as OUTPUT, and the servo and display will later be initialized with their own libraries. I also learned that analog inputs like a potentiometer often do not need pinMode() because they are read using analogRead().

**7.Non-Blocking Timing Preparation:**
I explored the concept of replacing delay() with millis() so the landing gear can move gradually while the Arduino remains responsive. Instead of checking for one exact timestamp, I learned to compare elapsed time using currentTime - lastMoveTime >= interval.

**8.Embedded Systems Mindset:**
This step moved the project closer to real embedded-system architecture. I focused not only on writing code, but on understanding hardware behavior, signal stability, pin abstraction, timing control, and maintainable system design.
