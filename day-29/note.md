Today I completed the following coding challenges:

**The Goal:**

Refactor the route-based aircraft fuel calculator into a cleaner modular program and begin transforming it from a console application into a graphical desktop interface using CustomTkinter.

A valid solution must meet these requirements:

-Separate calculation logic into reusable helper functions.

-Move the main execution flow into a dedicated `main()` function.

-Preserve aircraft, route, wind, range, flight-time, and fuel-cost calculations.

-Begin building a GUI foundation for the fuel calculator using CustomTkinter.

**My Approach:**

**1.Modular Function Refactoring:**
I separated key calculations into dedicated helper functions: `calculate_range_utilization()`, `calculate_flight_time()`, and `get_range_status()`. This makes the program easier to read, test, and expand.

**2.Main Program Encapsulation:**
I moved the console workflow into a `main()` function and call it inside a `try/except` block. This creates a cleaner execution structure and separates setup, logic, and error handling more clearly.

**3.Cleaner Wind Direction Handling:**
I normalized the wind-direction input immediately using `.lower()`. This reduces repeated string conversion and makes the validation logic cleaner.

**4.Logic Preservation During Refactoring:**
Even after restructuring the code, I preserved the existing features: aircraft selection, route selection, range utilization, flight-time calculation, wind effect, fuel consumption, fuel cost, and operational warnings.

**5.CustomTkinter GUI Foundation:**
I started a new graphical version of the Aircraft Fuel Calculator using CustomTkinter. I created the main app window, added a title, introduced an aircraft dropdown, and added the first weight input field. This establishes the base structure for turning the console-based calculator into a full desktop application.

