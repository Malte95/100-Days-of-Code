Today I completed the following coding challenges:

**The Goal:**

Expand the flight performance calculator into a more advanced aircraft analysis tool by adding takeoff weight limits, cruise-speed data, and estimated flight-time calculation.

A valid solution must meet these requirements:

-Extend aircraft profiles with maximum takeoff weight and cruise speed values.

-Calculate estimated flight time based on distance and aircraft cruise speed.

-Detect when the entered aircraft weight exceeds the selected aircraft’s maximum takeoff weight.

-Improve the final report with more detailed aircraft and flight performance data.

**My Approach:**

**1.Aircraft Data Model Expansion:**
I upgraded each aircraft profile by adding max_takeoff_weight and cruise_speed. This makes the aircraft database more realistic and allows the program to evaluate more than just fuel consumption and range.

**2.Flight Time Calculation:**
I introduced a new flight_time variable using the selected aircraft’s cruise speed. The program now estimates how long the flight will take based on the entered distance.

**3.Maximum Takeoff Weight Validation:**
I added a new operational warning system that checks whether the entered weight exceeds the aircraft’s maximum takeoff weight. If the value is too high, the program displays a warning before continuing with the calculation.

**4.Improved Performance Reporting:**
I expanded the final output report to include cruise speed, flight time, range utilization, aircraft weight, wind conditions, and fuel consumption. This makes the result more structured, informative, and closer to a real flight performance summary.

**5.Cleaner Calculation Function:**
I removed the unused range_utilization parameter from calculate_fuel(). The fuel function now only receives the values it actually needs, which improves code clarity and keeps the calculation engine cleaner.
