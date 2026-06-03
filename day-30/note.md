Today I completed the following coding challenges:

**The Goal:**

Transform the aircraft fuel calculator from a console-based program into a functional CustomTkinter desktop GUI with aircraft selection, route selection, wind input, fuel price input, and live result output.

A valid solution must meet these requirements:

-Replace terminal-based user input with graphical input fields and dropdown menus.

-Connect aircraft and route data directly to GUI selection components.

-Preserve the existing fuel calculation logic inside the new interface.

-Display fuel consumption and fuel cost directly inside the application window.

**My Approach:**

**1.Full GUI Migration:**
I moved the project from a command-line workflow into a CustomTkinter desktop interface. Instead of using input() and print(), the user now interacts with labels, entry fields, dropdown menus, and a calculate button.

**2.String-Based Data Mapping:**
I refactored the aircraft and route dictionaries from numeric keys to readable string keys such as "A320" and "Hamburg-Finkenwerder → Toulouse". This allows the dropdown values to connect directly to the stored aircraft and route data.

**3.Graphical Input System:**
I added GUI input fields for aircraft weight, wind strength, fuel price, route selection, and wind direction. This creates a more intuitive and user-friendly workflow compared to manual terminal input.

**4.Event-Driven Calculation Handler:**
I implemented a handle_calculation() function connected to the Calculate button. This function reads values from the GUI, validates numeric input, selects the correct aircraft and route data, calculates fuel consumption, and updates the result label.

**5.In-App Result Display:**
Instead of printing the result to the terminal, the application now displays fuel consumption and total fuel cost directly in the GUI. This completes the first fully functional desktop version of the Aircraft Fuel Calculator.
