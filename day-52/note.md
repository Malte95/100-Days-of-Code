Today I completed the following coding challenges:

**The Goal:**

Strengthen my understanding of Python list handling, integer division, function arguments, and nested function calls by working through two algorithm challenges: moving zeros to the end of an array and building calculations from number and operation functions.

**A valid solution must meet these requirements:**

-Preserve the order of non-zero elements while moving all zeros to the end.

-Understand the difference between modifying an existing list and returning a new list.

-Use Python integer division correctly with `//`.

-Understand how nested function calls are evaluated from the inside out.

-Recognize why functions can use optional parameters such as `operation=None`.

**My Approach:**

**1.Move Zeros Challenge:** I worked on the challenge of moving all zeros in a list to the end while preserving the order of every other value. I explored the idea of separating non-zero values from zeros and combining both groups afterward.

**2.List Comprehension Logic:** I learned how a compact list-comprehension solution works. The first list comprehension collects all elements that are not zero, while the second collects the zeros. The `+` operator then joins both lists into one new result list.

**3.List Modification Awareness:** I identified why changing a list while looping through it can create problems. Removing elements during iteration can shift indexes and cause values to be skipped, so returning a newly built list is often safer for this kind of task.

**4.Integer Division:** I learned the difference between normal division `/` and integer division `//`. For example, `5 / 3` returns a decimal value, while `5 // 3` returns `1` because it rounds down to the next whole number.

**5.Function Calculation Challenge:** I started working through a challenge where calculations are written with nested functions, such as `seven(times(five()))`. This introduced the idea that Python evaluates the innermost function first.

**6.Order of Function Calls:** I broke down how `seven(times(five()))` is processed. First, `five()` returns `5`. Then `times(5)` creates the multiplication instruction. Finally, `seven(...)` uses `7` as the left side of the calculation.

**7.Optional Function Parameters:** I explored why a number function can use a parameter such as `operation=None`. This allows the same function to work both as a simple number, such as `five()`, and as the outer part of a calculation, such as `seven(times(five()))`.

**8.Python Fundamentals Progress:** Today’s work strengthened my understanding of lists, loops, list comprehensions, return values, function parameters, nested calls, and integer division. I also practiced breaking coding problems into smaller steps instead of treating the final solution as one large problem.

