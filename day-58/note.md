Today I completed the following Python programming tasks:

## 1. Keypad PIN Variations

### The Goal

Develop a Python function called `get_pins(observed)` that returns all possible PIN variations for an observed keypad PIN.

A valid solution must meet these requirements:

* Support observed PINs with a length of 1 to 8 digits.
* Treat each observed digit as either itself or a horizontally or vertically adjacent keypad digit.
* Return all possible PIN variations as strings.
* Preserve leading zeros in generated PINs.
* Generate every valid combination without missing or duplicating possible PINs.

### My Approach

1. **Analyzed the Keypad Layout**
   I examined the keypad layout and identified which digits are horizontally or vertically adjacent to every key. Diagonal positions were excluded because they are not valid according to the task requirements.

   For example:

   * `1` → `1, 2, 4`
   * `5` → `2, 4, 5, 6, 8`
   * `8` → `5, 7, 8, 9, 0`
   * `0` → `0, 8`

2. **Created a Digit-Adjacency Dictionary**
   I created a Python dictionary called `adjacent` that stores every observed digit and its possible keypad inputs. This makes it possible to quickly look up all valid alternatives for each digit in the observed PIN.

3. **Preserved PIN Values as Strings**
   I kept all PIN values as strings rather than integers. This is important because PINs may begin with `0`, and converting them to numbers would remove leading zeros.

   For example, `"08"` must remain `"08"` and must not become `8`.

4. **Built the Result Step by Step**
   I started with a list containing one empty string:

   `[""]`

   This represents the starting point before any observed digits have been processed.

   For every digit in the observed PIN, I created a new list of PIN combinations. Each existing partial PIN was combined with every allowed option for the current digit.

5. **Applied Nested Loops for Combination Generation**
   I used nested loops to generate every possible variation:

   * The outer loop processes each digit in the observed PIN.
   * The first inner loop processes every PIN combination created so far.
   * The second inner loop processes every allowed keypad option for the current observed digit.

   This ensures that every existing partial PIN is extended with every possible next digit.

6. **Corrected the Combination Logic**
   During implementation, I identified that adding only the new option would lose the previously generated part of the PIN.

   For example:

   `"12"` combined with `"4"` must become `"124"`.

   I corrected the logic so that the previous PIN fragment and the new keypad option are joined together before being stored in the new result list.

7. **Updated the Working PIN List After Each Digit**
   After all combinations for one observed digit were generated, I replaced the old list of partial PINs with the newly created list.

   This allowed the function to continue building longer PIN variations until the complete observed PIN had been processed.

8. **Validated the Logic With Example Inputs**
   I checked the expected behavior with simple test cases.

   For example:

   `get_pins("8")`

   should return the five possible results:

   `["5", "7", "8", "9", "0"]`

   For an observed PIN such as `"1357"`, the number of possible PIN variations should be:

   `3 × 3 × 5 × 3 = 135`

   This confirmed that the combination logic correctly handles multiple keypad alternatives across several PIN positions.

---

## 2. Lucky Number Calculator

### The Goal

Develop a Python function called `get_lucky_number(name)` that calculates a lucky number from a person's first and last name.

The function must:

* Separate the first and last name.
* Count vowels and consonants in each name.
* Find the smaller and larger vowel counts.
* Find the smaller and larger consonant counts.
* Multiply the smaller vowel count, smaller consonant count, and the length of the shorter name.
* Multiply the larger vowel count, larger consonant count, and the length of the longer name.
* Subtract the smaller value from the larger value.
* Return `13` if the final result is `0`.

### My Approach

1. **Converted and Split the Name**
   I first converted the full name to lowercase so that uppercase and lowercase letters would be treated equally.

   I then used `split()` to separate the input into a first name and a last name.

2. **Created Separate Counters for Both Names**
   I created individual variables to count:

   * Vowels in the first name
   * Consonants in the first name
   * Vowels in the last name
   * Consonants in the last name

   This was important because the two names needed to be analyzed separately before comparing their values.

3. **Defined the Vowels**
   I stored the vowels in a string:

   `aeiou`

   For each letter, I checked whether it was contained in this vowel collection. If it was, I increased the vowel count. If it was not, I increased the consonant count.

4. **Used Separate Loops for First and Last Name**
   I used one loop to process the first name and another loop to process the last name.

   This allowed me to count vowels and consonants independently for each part of the full name.

5. **Identified the Shorter and Longer Name**
   I compared the lengths of the first and last name using an `if-else` statement.

   The shorter name was stored as `small_name`, and the longer name was stored as `large_name`. Their lengths were later used in the final multiplication.

6. **Compared the Vowel Counts**
   I compared the vowel count of the first name with the vowel count of the last name.

   Based on the comparison, I stored the smaller value as `small_vowel` and the larger value as `large_vowel`.

7. **Compared the Consonant Counts**
   I repeated the same process for consonants.

   I compared the consonant counts from both names and stored the smaller value as `small_consonant` and the larger value as `large_consonant`.

8. **Calculated the Two Required Values**
   I calculated the smaller value by multiplying:

   `small vowel count × small consonant count × length of the shorter name`

   I calculated the larger value by multiplying:

   `large vowel count × large consonant count × length of the longer name`

9. **Calculated the Lucky Number**
   I subtracted the smaller value from the larger value to calculate the lucky number.

   Finally, I checked whether the result was `0`. According to the task requirements, the function returns `13` instead whenever the calculated lucky number is zero.

10. **Completed the Challenge**
    The final function successfully solves the challenge. It uses string methods, loops, conditionals, counters, comparisons, arithmetic operations, and a special-case return value.

This work helped me practice processing strings, using `split()` and `lower()`, counting characters with loops, comparing values with conditional statements, and building complete Python functions step by step.


