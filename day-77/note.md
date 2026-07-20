# Today I Completed Two Python Programming Challenges

Today, I completed two Python programming challenges:

1. **Golden Ratio**
2. **Tally Counter**

Both challenges helped me practise working with functions, conditions, string methods, mathematical calculations, and return values.

---

# Challenge 1: Golden Ratio

## The Goal

The goal of this challenge was to develop a Python function called:

```python
is_golden_ratio(a, b)
```

The function determines whether the ratio between two numbers approximately matches the golden ratio.

The golden ratio used in this challenge is:

```python
1.618
```

Because the calculated ratio does not need to equal `1.618` exactly, the function allows a tolerance of:

```python
0.01
```

The function receives two numbers, `a` and `b`, and returns:

* `True` if their ratio is within `0.01` of `1.618`
* `False` if the ratio is outside the allowed tolerance

The larger number must always be divided by the smaller number. This ensures that the ratio is greater than or equal to `1`, regardless of the order in which the arguments are provided.

For example:

```python
is_golden_ratio(8, 13)
```

Since `13` is larger than `8`, the ratio is:

```python
13 / 8
```

This equals:

```python
1.625
```

The difference between `1.625` and `1.618` is:

```python
0.007
```

Since `0.007` is smaller than the allowed tolerance of `0.01`, the function returns:

```python
True
```

## The Tests

The function needed to pass the following tests:

```python
is_golden_ratio(21, 34)
# True

is_golden_ratio(15, 20)
# False

is_golden_ratio(8, 13)
# True

is_golden_ratio(10, 16)
# False

is_golden_ratio(1618, 1000)
# True

is_golden_ratio(88, 55)
# False
```

All six tests passed.

## My Approach

### 1. Checking for Invalid Values

First, I checked whether either number was less than or equal to zero.

```python
if a <= 0 or b <= 0:
    return False
```

A value of zero could cause division by zero.

Negative values are also unsuitable for this challenge because the golden ratio represents a positive relationship between two positive values.

If either value is invalid, the function immediately returns `False`.

Using `return` ends the function, so the remaining calculations are only performed when both numbers are positive.

### 2. Determining the Larger Number

The ratio must be calculated by dividing the larger number by the smaller number.

I first checked whether `a` was larger than `b`.

```python
if a > b:
    ratio = a / b
```

If `a` is not larger, `b` is divided by `a`.

```python
else:
    ratio = b / a
```

This ensures that the order of the arguments does not affect the result.

For example:

```python
is_golden_ratio(8, 13)
```

and:

```python
is_golden_ratio(13, 8)
```

both calculate:

```python
13 / 8
```

The ratio is therefore always calculated as:

```text
larger number / smaller number
```

### 3. Calculating the Absolute Difference

After calculating the ratio, I measured its distance from the golden ratio.

```python
tolerance = abs(ratio - 1.618)
```

The `abs()` function returns the absolute value of a number.

This is important because the calculated ratio could be slightly higher or slightly lower than `1.618`.

For example:

```python
1.625 - 1.618
```

returns:

```python
0.007
```

However:

```python
1.600 - 1.618
```

returns:

```python
-0.018
```

Without `abs()`, the negative result could incorrectly pass the comparison because a negative number is smaller than `0.01`.

Using `abs()` changes:

```python
-0.018
```

into:

```python
0.018
```

The function therefore measures the distance from the golden ratio in both directions.

### 4. Comparing the Difference With the Tolerance

The allowed tolerance is `0.01`.

I checked whether the absolute difference was less than or equal to this value.

```python
if tolerance <= 0.01:
    return True
```

If the difference is no more than `0.01`, the ratio is considered close enough to the golden ratio.

Otherwise, the function returns:

```python
False
```

The use of `<=` means that a difference of exactly `0.01` would also be accepted.

## Example: 21 and 34

The function receives:

```python
is_golden_ratio(21, 34)
```

Both numbers are positive, so the function continues.

Since `34` is larger than `21`, the ratio is:

```python
34 / 21
```

This equals approximately:

```python
1.619047619
```

The absolute difference from the golden ratio is:

```python
abs(1.619047619 - 1.618)
```

This is approximately:

```python
0.001047619
```

Since this value is smaller than `0.01`, the function returns:

```python
True
```

## Example: 15 and 20

The function receives:

```python
is_golden_ratio(15, 20)
```

Since `20` is larger than `15`, the ratio is:

```python
20 / 15
```

This equals approximately:

```python
1.333
```

The absolute difference from the golden ratio is approximately:

```python
abs(1.333 - 1.618)
```

which equals:

```python
0.285
```

Since this is greater than the allowed tolerance of `0.01`, the function returns:

```python
False
```

## Example: 8 and 13

The function receives:

```python
is_golden_ratio(8, 13)
```

Since `13` is larger than `8`, the ratio is:

```python
13 / 8
```

This equals:

```python
1.625
```

The absolute difference is:

```python
abs(1.625 - 1.618)
```

which equals:

```python
0.007
```

Since `0.007` is within the allowed tolerance, the function returns:

```python
True
```

## Example: 10 and 16

The ratio is:

```python
16 / 10
```

which equals:

```python
1.6
```

The absolute difference from `1.618` is:

```python
abs(1.6 - 1.618)
```

which equals:

```python
0.018
```

Since `0.018` is greater than `0.01`, the function returns:

```python
False
```

## The Final Function

```python
def is_golden_ratio(a, b):
    if a <= 0 or b <= 0:
        return False

    if a > b:
        ratio = a / b
    else:
        ratio = b / a

    tolerance = abs(ratio - 1.618)

    if tolerance <= 0.01:
        return True
    else:
        return False
```

## Why This Solution Works

The function first ensures that both numbers are positive.

It then determines which number is larger and divides the larger number by the smaller number. This makes the function independent of the order in which the arguments are provided.

Next, it calculates the absolute difference between the resulting ratio and `1.618`.

The general process is:

1. Check whether both numbers are positive.
2. Determine which number is larger.
3. Divide the larger number by the smaller number.
4. Calculate the absolute difference from `1.618`.
5. Compare the difference with the tolerance of `0.01`.
6. Return `True` if the difference is within the tolerance.
7. Return `False` if the difference is too large.

Using the absolute value ensures that ratios slightly above and slightly below `1.618` are treated equally.

For example:

```python
abs(1.625 - 1.618)
# 0.007
```

and:

```python
abs(1.610 - 1.618)
# 0.008
```

Both values are within the allowed tolerance of `0.01`.

The function therefore correctly determines whether the ratio between two positive numbers approximates the golden ratio.

---

# Challenge 2: Tally Counter

## The Goal

The goal of the second challenge was to develop a function called:

```python
get_tally_count(s)
```

The function receives a string containing tally marks and returns the total count represented by those marks.

Each pipe character:

```text
|
```

represents one count.

Every fifth mark is written as a forward slash:

```text
/
```

This completes a group of five tally marks:

```text
||||/
```

Groups are separated by spaces.

For example:

```text
||||/ |||
```

contains one complete group of five followed by three additional marks.

The total is therefore:

```text
5 + 3 = 8
```

## The Tests

The function needed to pass the following tests:

```python
get_tally_count("||||")
# 4

get_tally_count("||||/")
# 5

get_tally_count("||||/ |||")
# 8

get_tally_count("||||/ ||||/ ||||/ ||")
# 17

get_tally_count("||||/ ||||/ ||||/ ||||/ ||||/ ||||/ ||||/ ||||/ |")
# 41
```

All five tests passed.

## Understanding the Tally Marks

The most important part of the challenge was understanding what the forward slash represents.

A complete group looks like this:

```text
||||/
```

It contains:

* four pipe characters
* one forward slash

The forward slash does not represent five additional marks. It represents the fifth individual mark in the group.

Therefore:

```text
||||/
```

has a total value of:

```text
4 + 1 = 5
```

Both `|` and `/` must therefore be counted as one mark each.

Spaces only separate the groups and do not contribute to the total.

## My First Idea

My first approach was to count the pipes and forward slashes separately.

I used the string method:

```python
.count()
```

to determine how many times each character appeared.

At first, I considered multiplying the number of forward slashes by five.

However, that would produce an incorrect result.

For example, the group:

```text
||||/
```

contains four pipes and one slash.

Multiplying the slash by five would calculate:

```text
4 + 5 = 9
```

The correct total is only:

```text
5
```

The slash represents the fifth mark, so it must be counted as one.

## Counting the Pipe Characters

I counted how many pipe characters appeared in the string.

```python
num_pipes = s.count("|")
```

For example:

```text
||||/ |||
```

contains seven pipe characters.

## Counting the Forward Slashes

I then counted how many forward slash characters appeared.

```python
num_slashes = s.count("/")
```

The same example contains one forward slash.

## Calculating the Total

Since every pipe and every forward slash represents one mark, the total can be calculated by adding both counts.

```python
return num_pipes + num_slashes
```

For the example:

```text
||||/ |||
```

the calculation is:

```text
7 pipes + 1 slash = 8
```

The spaces do not need to be removed manually because `.count()` searches only for the specified characters.

## Example: Four Marks

The function receives:

```python
get_tally_count("||||")
```

The string contains:

* four pipes
* no forward slashes

The total is:

```text
4 + 0 = 4
```

The function returns:

```python
4
```

## Example: One Complete Group

The function receives:

```python
get_tally_count("||||/")
```

The string contains:

* four pipes
* one forward slash

The total is:

```text
4 + 1 = 5
```

The function returns:

```python
5
```

## Example: One Group and Three Additional Marks

The function receives:

```python
get_tally_count("||||/ |||")
```

The string contains:

* seven pipes
* one forward slash

The total is:

```text
7 + 1 = 8
```

The function returns:

```python
8
```

## Example: Three Groups and Two Additional Marks

The function receives:

```python
get_tally_count("||||/ ||||/ ||||/ ||")
```

The string contains:

* fourteen pipes
* three forward slashes

The total is:

```text
14 + 3 = 17
```

The function returns:

```python
17
```

## The Final Function

```python
def get_tally_count(s):
    num_pipes = s.count("|")
    num_slashes = s.count("/")

    return num_pipes + num_slashes
```

## Why This Solution Works

The function counts every pipe and every forward slash in the string.

Both characters represent one tally mark, so their counts can be added together.

Spaces do not need any special handling because they are not included in either `.count()` operation.

The general process is:

1. Count all pipe characters.
2. Count all forward slash characters.
3. Add both counts.
4. Return the result.

The solution is short, readable, and directly reflects the rules of the challenge.

Although `.count()` scans the string once for each character, this is not a problem for the expected input sizes. The solution remains efficient and easy to understand.

Its time complexity is:

```text
O(n)
```

Even though the string is scanned twice, the total amount of work still grows linearly with the length of the string.

The function also uses only a constant amount of additional memory:

```text
O(1)
```

This makes the solution both simple and efficient.

---

# What I Practised

These two challenges covered different areas of Python programming.

The Golden Ratio challenge helped me practise:

* validating function arguments
* preventing division by zero
* comparing numbers
* calculating ratios
* working with floating-point values
* using `abs()`
* applying a tolerance
* returning Boolean values

The Tally Counter challenge helped me practise:

* working with strings
* understanding character-based input
* using `.count()`
* distinguishing meaningful characters from separators
* translating a visual counting system into a numerical result
* analysing the efficiency of a solution

Both challenges showed that understanding the problem correctly is just as important as writing the code.

In the Tally Counter challenge, the key insight was recognising that `/` represents only the fifth individual mark rather than five additional marks.

In the Golden Ratio challenge, the key insight was using the absolute difference so that ratios both above and below `1.618` could be compared correctly.

Completing both challenges gave me more experience with breaking a problem into smaller steps and turning those steps into clear Python functions.


