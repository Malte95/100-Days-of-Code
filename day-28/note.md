Today I completed the following coding challenges:

**The Goal:**

Expand the flight performance calculator into a route-based fuel and cost analysis tool by adding predefined flight routes, automatic distance selection, and fuel cost estimation.

A valid solution must meet these requirements:

-Introduce a route selection system with predefined origin, destination, and distance data.

-Replace manual distance input with automatic route-based distance retrieval.

-Calculate total fuel cost based on estimated fuel consumption and user-defined fuel price.

-Validate both aircraft and route selections before running the flight calculation.

**My Approach:**

**1.Route Database Implementation:**
I introduced a new routes dictionary containing predefined flight routes with origin, destination, and distance values. This allows the program to work with realistic route scenarios instead of relying on manually entered distances.

**2.Route-Based Distance Automation:**
Instead of asking the user to enter the flight distance manually, the program now retrieves the distance directly from the selected route. This reduces input errors and makes the calculation workflow more structured.

**3.Dual Selection Validation:**
I expanded the validation system so the program now checks both the selected aircraft and the selected route before continuing. Invalid aircraft or route choices are stopped early with clear error messages.

**4.Fuel Cost Calculation:**
I added a new economic calculation layer using fuel_price_per_liter. After calculating fuel consumption, the program now multiplies the result by the entered fuel price to estimate total fuel cost.

**5.Enhanced Flight Report Output:**
The final report now includes route information, route distance, flight time, range utilization, wind conditions, estimated fuel consumption, and total fuel cost. This makes the output more complete and turns the calculator into a more realistic flight planning support tool.
