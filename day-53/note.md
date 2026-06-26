Today I completed the following coding challenge:

**The Goal:**

Strengthen my understanding of Python strings, nested loops, list handling, return values, and case-insensitive comparisons by working through a challenge that finds the first character in a string that does not repeat.

A valid solution must meet these requirements:

-Return the first character that appears only once in the string.

-Preserve the original order of the characters.

-Return an empty string when every character repeats.

-Treat upper- and lowercase letters as the same during comparison.

-Return the character in its original case.

**My Approach:**

**1.First Non-Repeating Character Challenge:** I worked on a challenge where the goal was to find the first character in a string that only appears once. For example, in `"stress"`, the correct result is `"t"` because it is the first character that does not repeat.

**2.Outer Loop for Each Character:** I used an outer `for` loop to go through the string one character at a time. This allowed me to test every character in its original order.

**3.Inner Loop for Counting Matches:** For each character from the outer loop, I used a second loop to go through the entire string again. Whenever the current character matched another character, I added it to a temporary list.

**4.List Length as a Counter:** I used the length of the temporary list to determine how many times the current character appeared. If the list had a length of `1`, that meant the character only occurred once.

**5.Returning the Correct Value:** I learned that the function should return the character itself, not the list containing the character. Returning a list such as `['t']` is different from returning the string `"t"`.

**6.Return Placement:** I identified why `return ""` must be placed after the outer loop. Returning an empty string too early would stop the function after checking only the first repeating character instead of checking the rest of the string.

**7.Case-Insensitive Comparison:** I explored using `s.lower()` to create a lowercase version of the input string. This makes it possible to treat `"T"` and `"t"` as the same character while still returning the original version from the input string.

**8.Python Fundamentals Progress:** Today’s work strengthened my understanding of strings, nested loops, temporary lists, list length checks, conditional statements, return values, indentation, and case-insensitive comparisons. I also practiced breaking one problem into smaller checks instead of trying to solve everything at once.

