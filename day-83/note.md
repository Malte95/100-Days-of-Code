# Today I Completed the Following Python Programming Tasks

## Challenge 1: Letter Distance

### The Goal

Develop a Python function called `letter_distance(str1, str2)` that calculates the total distance between two strings of equal length.

The function receives:
* a first string (`str1`) consisting of lowercase letters
* a second string (`str2`) consisting of lowercase letters

The function should then return the sum of the shortest distances between each pair of characters.

The rules are:
* The input will only contain lowercase letters.
* Both strings will always be of equal length.
* The alphabet is treated as a circle, meaning it wraps around from 'z' to 'a'. Therefore, the distance between `"a"` and `"z"` is `1`.

### The Tests

The function successfully handles and passes the following test cases:
* `letter_distance("abc", "bcd")` should return `3`.
* `letter_distance("abc", "xyz")` should return `9`.
* `letter_distance("encrypt", "decrypt")` should return `10`.
* `letter_distance("algorithm", "codeblock")` should return `43`.
* `letter_distance("lobster", "penguin")` should return `47`.
* `letter_distance("alligator", "crocodile")` should return `55`.

These tests ensure that the function works correctly for simple shifts, large alphabetical gaps, identical prefixes, and wrapping around the edges of the circular alphabet.

### My Approach

#### 1. Created an Alphabet Reference List
First, I imported Python's built-in `string` module and generated a list of all 26 lowercase English letters using `string.ascii_lowercase`. This gave me a reliable, zero-indexed reference list (`['a', 'b', 'c', ..., 'z']`) to look up the exact positions of characters.

#### 2. Set Up a Distance Counter
Before starting any calculations, I initialized a tracking variable named `distances` and set it to `0`. This variable acts as a running total to collect and sum up the shortest path lengths for each character pair as the program iterates through the strings.

#### 3. Iterated Synchronously Through Both Strings
Since both input strings are guaranteed to be of equal length, I used a `for` loop with `range(len(str1))`. This approach uses a single index variable `i` that increments from `0` up to the last position of the words. It allows the loop to look at `str1[i]` and `str2[i]` at the exact same time, aligning the character pairs perfectly.

#### 4. Calculated the Direct Distance
Inside the loop body, I used the `.index()` method on my alphabet list to find the numerical positions of both current characters. I subtracted one position from the other. To prevent negative numbers (which happen when the character in `str1` is further ahead in the alphabet than the one in `str2`), I wrapped the subtraction inside Python's built-in `abs()` function. This safely calculated the standard, direct distance.

#### 5. Accounted for the Circular Alphabet
Because the alphabet wraps around like a ring, there are always two possible ways to travel from one letter to another: moving forward directly, or moving backward "around the outside" past the 'z'/'a' boundary. Since a full alphabetical circle consists of 26 letters, the alternative path is always `26 - direct_distance`. I used Python's `min()` function to compare both options and pick whichever value was smaller.

#### 6. Accumulated and Returned the Final Sum
After finding the absolute shortest path for the current pair, I added that value to my running total (`distances += shortest_distance`). Once the loop finished checking every single character index, the function executed a `return` statement to output the accumulated total sum.

### The Code

```python
import string

def letter_distance(str1, str2):
    abc = list(string.ascii_lowercase)
    distances = 0

    for i in range(len(str1)):
        distance = abs(abc.index(str1[i]) - abc.index(str2[i]))
        shortest_distance = min(distance, 26 - distance)
        distances += shortest_distance

    return distances
```

---

## Challenge 2: Word Blender

### The Goal

Develop a Python function called `blend_words(word1, word2)` that takes two separate strings and merges them into a new, combined word (a portmanteau).

The function receives:
* a first word string (`word1`)
* a second word string (`word2`)

The function should then return a new string containing the first half of the first word joined with the second half of the second word.

The rules are:
* Take the first half of the first word (`word1`).
* Take the second half of the second word (`word2`).
* For odd-length words, the first half must be the shorter half.

### The Tests

The function successfully handles and passes the following test cases:
* `blend_words("turtle", "toucan")` should return `"turcan"`.
* `blend_words("chipmunk", "flamingo")` should return `"chipingo"`.
* `blend_words("falcon", "pelican")` should return `"falican"`.
* `blend_words("hyena", "iguana")` should return `"hyana"`.
* `blend_words("scorpion", "gorilla")` should return `"scorilla"`.
* `blend_words("platypus", "wolverine")` should return `"platerine"`.

These tests ensure that the function handles words of equal or varying lengths, and correctly applies the boundary rules for both even and odd letter counts.

### My Approach

#### 1. Understood the Slicing Concept
To divide the words cleanly without relying on string-splitting methods like `.split()` (which look for specific characters like spaces), I decided to use Python's index slicing syntax `[:]`. This requires finding a precise numerical middle index for each word.

#### 2. Solved the Odd-Length Constraint with Floor Division
The key constraint was that for odd-length words, the first half must be the shorter one. I discovered that using Python's floor division operator (`//`) naturally fulfills this rule. Because `//` always rounds down to the nearest whole integer, a word of length 5 (like `"Apfel"`) results in a middle index of `5 // 2 = 2`. 

#### 3. Extracted the First Half
Using the calculated middle index for the first word (`middle1`), I used the slice syntax `[:middle1]`. For an odd word of length 5, this extracts characters from index 0 up to (but excluding) index 2, resulting in exactly 2 characters. This mathematically guarantees that the first half is the shorter half without requiring any complex `if-else` conditions.

#### 4. Extracted the Second Half
For the second word, I calculated its middle index (`middle2`) using the same floor division method. I then extracted the remaining part of the word using the slice syntax `[middle2:]`. This captures everything from the middle index all the way to the end of the string, ensuring that the second half takes the "longer" portion of an odd-length word.

#### 5. Combined and Returned the New Word
Finally, I joined both extracted string components using the `+` operator to create a single string (`combination`). The function concludes by returning this newly blended word back to the caller.

### The Code

```python
def blend_words(word1, word2):
    middle1 = len(word1) // 2
    middle2 = len(word2) // 2

    first_half = word1[:middle1]
    second_half = word2[middle2:]

    combination = first_half + second_half

    return combination
```

---

## Why These Solutions Work

Both solutions succeed because they break down abstract manipulation tasks into clear, logical, and mathematical steps. 

First, in **Letter Distance**, the combination of `abs()` and `min(distance, 26 - distance)` replicates a flawless tracking system for a circular ring layout. It ensures that the code always finds the true shortest path, whether it's the direct route or the shortcut past the 'z'/'a' boundary.

Second, in **Word Blender**, leveraging floor division (`//`) naturally incorporates the boundary constraint for odd-length words directly into the core math. By letting Python handle the rounding logic, the codebase remains incredibly compact, readable, and highly efficient, entirely eliminating the need for conditional checks.

The general process across both challenges was:
1. Map out the constraints and edge cases (circular wrapping and odd string lengths).
2. Translate the logical boundaries into mathematical rules using Python operators (`abs`, `min`, and `//`).
3. Apply precise index handling to extract or compare characters at specific positions.
4. Accumulate or combine the results into the expected output type.
5. Verify against a robust suite of test cases to ensure edge-case reliability.


