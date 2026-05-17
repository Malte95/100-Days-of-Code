Today I completed the following coding challenges:

**The Goal:**

Given a MongoDB ID string, return its creation time as an ISO 8601 formatted string.

A valid solution must meet these requirements:

-Parse a 24-character hexadecimal string where the first 8 characters represent a Unix timestamp in seconds.

-Convert the extracted base-16 integer into a standard decimal Unix timestamp.

-Transform the timestamp into a precise ISO 8601 date-time string.

-Ensure strict formatting compliance, including timezone awareness (UTC) and explicit millisecond resolution (e.g., "YYYY-MM-DDTHH:MM:SS.mmmZ").

**My Approach:**

**1.String Slicing:** Since only the first 8 characters contain the timestamp data, I utilized Python's slicing mechanics ([:8]) to efficiently isolate the hex substring from the rest of the MongoDB ID.

**2.Base Conversion:** I converted the isolated hexadecimal string into a base-10 decimal integer by leveraging Python's built-in int() function with an explicit base-16 argument.

**3.Timezone-Aware Parsing:** To prevent local system time discrepancies, I used datetime.datetime.fromtimestamp() combined with datetime.timezone.utc to instantiate a precise, timezone-aware datetime object.

**4.Enforced Formatting:** I utilized the .isoformat() method with the timespec='milliseconds' parameter to guarantee that trailing zeros for milliseconds are never omitted, replacing the standard timezone offset with the strict 'Z' character to match the required MongoDB specification.

___

**The Goal:**

Given a list of simulated flight data strings from an aircraft data logger, filter out corrupted entries, parse the valid metrics, and return a statistical summary.

A valid solution must meet these requirements:

-Process a list of strings where valid entries follow a strict "TEMPERATURE;ALTITUDE" format.

-Identify and isolate corrupted data, including empty strings, missing delimiters, or non-numeric values.

-Calculate the maximum altitude recorded across all valid entries as an integer.

-Calculate the average temperature across all valid entries, rounded to a single decimal place.

-Return the final metrics structured inside a clean Python dictionary.

**My Approach:**

**1.Data Sanitization Loop:** I implemented an initial validation pass using a for loop to filter out empty strings and missing delimiters via if not element or element.find(";") == -1, ensuring only properly delimited strings advanced to processing.

**2.String Partitioning & Type Casting:** For the validated entries, I used the .split(";") method to separate the metrics, converting the temperature substring into a float and the altitude substring into an int.

**3.Dynamic Maximum Tracking:** I initialized a tracking variable outside the processing loop and used a conditional statement (if convert_int > max_height) to continuously evaluate and update the peak altitude record.

**4.Statistical Aggregation:** I accumulated the valid temperatures using the += operator and dynamically computed the final average by dividing the total sum by the size of the sanitized dataset (len(valid_element)), finalizing the value with Python's round() function.
