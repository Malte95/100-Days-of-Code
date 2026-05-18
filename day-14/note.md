Today I completed the following coding challenges:

**The Goal:**

Given a Bingo column letter, return its valid number range as an array (list) of integers.

A valid solution must meet these requirements:

-Map each letter of the traditional word "BINGO" to its specific 15-number range, covering numbers 1 to 75 in total.

-Handle input case-insensitivity to ensure both lowercase and uppercase letters produce identical results.

-Generate a sequential, complete sequence of numbers for the requested column.

-Ensure strict error handling and safety compliance by returning an empty array if an invalid character or string is provided.

**My Approach:**

**1.String Normalization:** To eliminate bugs from mixed-case user inputs, I utilized Python's built-in .upper() method to convert the input character to uppercase before running any conditional logic.

**2.Conditional Mapping:** I implemented a clean if-elif control flow structure to separate the distinct mathematical boundaries for each individual Bingo column (B, I, N, G, O).

**3.Sequence Generation:** I leveraged Python's built-in range() function to generate the sequential integers dynamically. I set the upper bound to +1 of the target maximum (e.g., range(1, 16) for 1-15) because Python ranges are exclusive of the stop value.

**4.Type Conversion:** I wrapped the generated range objects inside the list() constructor to explicitly transform the sequence into a standard, fully mutable Python array structure ready for the caller.

--

**The Goal:**

Build and analyze fundamental electronic circuits using an Arduino Starter Kit to understand the practical differences between series and parallel configurations.

A valid solution must meet these requirements:

-Construct a functional series circuit using two push-buttons where both must be pressed simultaneously to complete the circuit and light up the LED.

-Reconfigure the components into a parallel circuit where pressing either of the two push-buttons independently completes the circuit and lights up the LED.

-Implement proper hardware protection by integrating a 220-ohm current-limiting resistor to prevent the LED from burning out.

-Understand how hardware-based connections mimic logical AND (series) and OR (parallel) operations without relying on complex microcontroller code.

**My Approach:**

**1.Component Integration:** I utilized a standard breadboard from the Arduino Starter Kit to arrange two push-buttons, one LED, and a 220-ohm resistor, drawing power directly from the Arduino's 5V and GND pins.

**2.Series Configuration (AND Logic):** I wired the two push-buttons sequentially in a single path. This forced the electrical current to pass through the first switch and then the second switch, meaning the LED only activates when both buttons are closed at the same time. 

**3.Parallel Configuration (OR Logic):** I rewired the circuit to split the incoming current into two separate, independent paths across both push-buttons before converging back at the LED. This allows the current to flow if at least one path is cleared by pressing either button.

**4.Hardware Safety:** I placed a 220-ohm resistor in series with the LED in both configurations. This successfully limited the current flowing through the diode, protecting it from overcurrent damage while keeping the brightness optimal.

