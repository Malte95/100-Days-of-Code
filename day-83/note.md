# Today I Completed the Following Python Programming Task

## Letter Distance

## The Goal

Develop a Python function called `letter_distance(str1, str2)` that calculates the total distance between two strings of equal length.

The function receives:

* a first string (`str1`) consisting of lowercase letters
* a second string (`str2`) consisting of lowercase letters

The function should then return the sum of the shortest distances between each pair of characters.

The rules are:

* The input will only contain lowercase letters.
* Both strings will always be of equal length.
* The alphabet is treated as a circle, meaning it wraps around from 'z' to 'a'. Therefore, the distance between `"a"` and `"z"` is `1`.

## The Tests

The function successfully handles and passes the following test cases:

* `letter_distance("abc", "bcd")` should return `3`.
* `letter_distance("abc", "xyz")` should return `9`.
* `letter_distance("encrypt", "decrypt")` should return `10`.
* `letter_distance("algorithm", "codeblock")` should return `43`.
* `letter_distance("lobster", "penguin")` should return `47`.
* `letter_distance("alligator", "crocodile")` should return `55`.

These tests ensure that the function works correctly for simple shifts, large alphabetical gaps, identical prefixes, and wrapping around the edges of the circular alphabet.

## My Approach

### 1. Created an Alphabet Reference List

First, I imported Python's built-in `string` module and generated a list of all 26 lowercase English letters using `string.ascii_lowercase`. 

This gave me a reliable, zero-indexed reference list (`['a', 'b', 'c', ..., 'z']`) to look up the exact positions of characters.

### 2. Set Up a Distance Counter

Before starting any calculations, I initialized a tracking variable named `distances` and set it to `0`. 

This variable acts as a running total to collect and sum up the shortest path lengths for each character pair as the program iterates through the strings.

### 3. Iterated Synchronously Through Both Strings

Since both input strings are guaranteed to be of equal length, I used a `for` loop with `range(len(str1))`. 

This approach uses a single index variable `i` that increments from `0` up to the last position of the words. It allows the loop to look at `str1[i]` and `str2[i]` at the exact same time, aligning the character pairs perfectly.

### 4. Calculated the Direct Distance

Inside the loop body, I used the `.index()` method on my alphabet list to find the numerical positions of both current characters. 

I subtracted one position from the other. To prevent negative numbers (which happen when the character in `str1` is further ahead in the alphabet than the one in `str2`), I wrapped the subtraction inside Python's built-in `abs()` function. This safely calculated the standard, direct distance.

### 5. Accounted for the Circular Alphabet

Because the alphabet wraps around like a ring, there are always two possible ways to travel from one letter to another: moving forward directly, or moving backward "around the outside" past the 'z'/'a' boundary. 

Since a full alphabetical circle consists of 26 letters, the alternative path is always `26 - direct_distance`. I used Python's `min()` function to compare both options and pick whichever value was smaller.

### 6. Accumulated and Returned the Final Sum

After finding the absolute shortest path for the current pair, I added that value to my running total (`distances += shortest_distance`). 

Once the loop finished checking every single character index, the function executed a `return` statement to output the accumulated total sum.

## Why This Solution Works

The solution works because it correctly breaks down a complex string comparison into tiny, predictable steps. 

By utilizing synchronous index loops, it ensures no characters are skipped or mismatched. The combination of `abc.index()` and `abs()` accurately translates letters into clean mathematical distances. 

Finally, the clever use of `min(distance, 26 - distance)` perfectly mimics a circular tracking system, dynamically choosing the quickest route around the alphabet.

The general process is:

1. Generate a lowercase alphabet list for reference.
2. Initialize a counter variable for the total distance.
3. Start a loop that runs for the length of the strings.
4. Extract the matching character pair using the current index.
5. Determine the numerical alphabet indices of both letters.
6. Calculate the positive, straight-line distance between them.
7. Compute the alternative circular distance and pick the smaller one.
8. Add the shortest distance to the total sum.
9. Return the accumulated result after processing all pairs.

This approach makes the function reliable, clean, and efficient enough to pass all the required challenge tests.

