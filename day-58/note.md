Today I completed the following Python programming tasks:

**The Goal:**

Develop a Python function called `get_pins(observed)` that returns all possible PIN variations for an observed keypad PIN.

**A valid solution must meet these requirements:**

* Support observed PINs with a length of 1 to 8 digits.
* Treat each observed digit as either itself or a horizontally/vertically adjacent keypad digit.
* Return all possible PIN variations as strings.
* Preserve leading zeros in generated PINs.
* Generate every valid combination without missing or duplicating possible PINs.

**My Approach:**

**1. Analyzed the Keypad Layout:** I first examined the keypad layout and identified which digits are horizontally or vertically adjacent to every key. Diagonal positions were excluded because they are not valid according to the task requirements.

For example:

`1` → `1, 2, 4`
`5` → `2, 4, 5, 6, 8`
`8` → `5, 7, 8, 9, 0`
`0` → `0, 8`

**2. Created a Digit-Adjacency Dictionary:** I created a Python dictionary called `adjacent` that stores every observed digit and its possible real keypad inputs. This makes it possible to quickly look up all valid alternatives for each digit in the observed PIN.

**3. Preserved PIN Values as Strings:** I kept all PIN values as strings rather than integers. This is important because PINs may begin with `0`, and converting them to numbers would remove leading zeros.

For example, `"08"` must remain `"08"` and must not become `8`.

**4. Built the Result Step by Step:** I started with a list containing one empty string:

`[""]`

This represents the starting point before any observed digits have been processed.

For every digit in the observed PIN, I created a new list of PIN combinations. Each existing partial PIN was combined with every allowed option for the current digit.

**5. Applied Nested Loops for Combination Generation:** I used nested loops to generate every possible variation:

* The outer loop processes each digit in the observed PIN.
* The first inner loop processes every PIN combination created so far.
* The second inner loop processes every allowed keypad option for the current observed digit.

This ensures that every existing partial PIN is extended with every possible next digit.

**6. Corrected the Combination Logic:** During implementation, I identified that adding only the new option would lose the previously generated part of the PIN.

For example:

`"12"` combined with `"4"` must become `"124"`.

I corrected the logic so that the previous PIN fragment and the new keypad option are joined together before being stored in the new result list.

**7. Updated the Working PIN List After Each Digit:** After all combinations for one observed digit were generated, I replaced the old list of partial PINs with the newly created list.

This allowed the function to continue building longer PIN variations until the complete observed PIN had been processed.

**8. Completed the Function Structure: The final function now:**

* Defines the keypad adjacency rules.
* Starts with an empty PIN fragment.
* Processes every observed digit one by one.
* Creates all possible PIN combinations.
* Returns the completed list of valid PIN variations.

**9. Validated the Logic With Example Inputs:** I checked the expected behavior with simple test cases.

For example:

`get_pins("8")`

should return the five possible results:

`["5", "7", "8", "9", "0"]`

For an observed PIN such as `"1357"`, the number of possible PIN variations should be:

`3 × 3 × 5 × 3 = 135`

This confirmed that the combination logic correctly handles multiple keypad alternatives across several PIN positions.

The project now includes keypad mapping, dictionary lookup, string handling, nested loops, list building, and combination generation in one working Python solution.

