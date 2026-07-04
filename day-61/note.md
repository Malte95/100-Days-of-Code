# Kaprekar's Routine

## The Goal

Develop a Python function called `kaprekar(n)` that returns the number of times Kaprekar's routine must be applied to a four-digit number until it reaches `6174`.

Kaprekar's routine works as follows:

1. Arrange the digits in descending order to create the largest possible number.
2. Arrange the digits in ascending order to create the smallest possible number.
3. Subtract the smaller number from the larger number.
4. Repeat the process with the new result.
5. Count how many steps are needed to reach `6174`.

For example:

```python
kaprekar(1234)
```

should return:

```python
3
```

This is because the routine works like this:

```python
4321 - 1234 = 3087
8730 - 0378 = 8352
8532 - 2358 = 6174
```

## My Approach

### Created a Counter Variable

I started by creating a variable called `count` with the value `0`.

This variable keeps track of how many times the Kaprekar routine is applied.

Each time the digits are rearranged and subtracted, the counter increases by `1`.

### Used a While Loop

I used a `while` loop to repeat the routine until the number reaches `6174`.

The loop continues as long as the current value of `n` is not equal to `6174`.

This was necessary because the number of required steps depends on the starting number.

### Converted the Number Into a String

Inside the loop, I converted the current number into a string.

This allowed me to work with the individual digits of the number.

For example:

```python
1234
```

becomes:

```python
"1234"
```

### Preserved Leading Zeros With `zfill(4)`

I used:

```python
str(n).zfill(4)
```

to make sure that every number is treated as a four-digit value.

This is important because some intermediate results may contain fewer than four digits.

For example:

```python
999
```

must be treated as:

```python
"0999"
```

Without the leading zero, the ascending and descending digit arrangements would not be calculated correctly.

### Sorted the Digits in Descending Order

I used Python's `sorted()` function with `reverse=True` to arrange the digits from largest to smallest.

For example:

```python
sorted("1234", reverse=True)
```

creates:

```python
["4", "3", "2", "1"]
```

This represents the largest possible number:

```python
4321
```

### Sorted the Digits in Ascending Order

I also used `sorted()` without `reverse=True` to arrange the digits from smallest to largest.

For example:

```python
sorted("1234")
```

creates:

```python
["1", "2", "3", "4"]
```

This represents the smallest possible number:

```python
1234
```

### Joined the Sorted Digits Back Into Strings

The `sorted()` function returns lists of individual characters.

To create complete numbers again, I used:

```python
"".join(...)
```

For example:

```python
["4", "3", "2", "1"]
```

becomes:

```python
"4321"
```

and:

```python
["1", "2", "3", "4"]
```

becomes:

```python
"1234"
```

### Converted the Strings Back Into Integers

After joining the digits, I converted both values into integers.

This was necessary because subtraction cannot be performed directly with strings.

For example:

```python
int("4321") - int("1234")
```

returns:

```python
3087
```

### Updated the Number for the Next Loop

After calculating the subtraction result, I stored the result back in `n`.

This makes the newly calculated number the starting point for the next Kaprekar step.

For example:

```python
1234 → 3087
```

Then the next loop starts with `3087`.

### Increased the Counter After Each Step

After each subtraction, I increased `count` by `1`.

This ensures that the function returns the total number of Kaprekar steps needed to reach `6174`.

### Returned the Final Count

Once the loop reaches `6174`, the function stops and returns `count`.

For the input:

```python
kaprekar(1234)
```

the function returns:

```python
3
```

## Completed the Challenge

The final function successfully applies Kaprekar's routine repeatedly until reaching `6174` and returns the number of required steps.

This work helped me practice `while` loops, counters, string conversion, leading zeros with `zfill()`, sorting characters with `sorted()`, joining lists with `join()`, converting strings into integers, subtraction, and updating values inside a loop.
