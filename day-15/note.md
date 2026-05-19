Today I completed the following coding challenges:

**The Goal:**

Develop a real-time monitor for an aircraft's Collision-Avoidance-System (TCAS) that detects dangerous sink rates.

A valid solution must meet these requirements:

-Monitor aircraft altitude data captured at second-by-second intervals.

-Trigger an emergency alarm (True) if the aircraft loses more than 1,000 feet within a rolling 3-second window.

-Ensure maximum memory efficiency and minimal footprint on the airborne computer, avoiding storing long flight histories.

-Return a clean boolean output (True or False) under all conditions, including initialization phases where data is still insufficient.

**My Approach:**

**1.Memory Optimization via Ring Buffer:** Instead of appending data to an unbound list and iterating over it continuously, I utilized Python’s collections.deque with a fixed maxlen=4. This ensures a strict O(1) constant memory usage, as the oldest data point is automatically discarded when a new one arrives.

**2.Sliding Window Analysis:** To accurately capture the 3-second timeframe, I designed the buffer to hold exactly 4 elements (representing Second 0, 1, 2, and 3).

**3.Boundary Condition Handling:** I implemented a safety check (len(storage) == 4) to prevent premature calculations or out-of-bounds errors before the system has gathered enough initial telemetry data.

**4.Deterministic Fallbacks:** I structured the control flow to ensure that the function explicitly falls back to Return False if the buffer is filling up or if the current descent rate remains within safe operational limits.
