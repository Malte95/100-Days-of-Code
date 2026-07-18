# Today I Completed the Following Python Programming Task

## Dice Odds

## The Goal

Develop a Python function called `get_odds(dice, target)` that calculates the mathematical probability of rolling a specific target sum with a given number of six-sided dice, and returns the result as a rounded string in the format `"1 in X"`.

The parameter `dice` represents the number of six-sided dice to roll (an integer between 1 and 6).

The parameter `target` is the exact sum you want to achieve with those dice. The target sum is guaranteed to be achievable with the given number of dice.

The function must return a string showing the odds. To match the challenge requirements, the denominator "X" must always be rounded to the nearest whole number, forcing a format where the numerator is always 1 (e.g., `"1 in 65"`), even if the true fraction cannot be cleanly reduced to a 1 in the numerator.

## The Tests

The function should correctly handle examples such as:

```python
get_odds(1, 5)
# "1 in 6"
```

```python
get_odds(2, 4)
# "1 in 12"
```

```python
get_odds(3, 10)
# "1 in 8"
```

```python
get_odds(4, 7)
# "1 in 65"
```

```python
get_odds(5, 26)
# "1 in 111"
```

```python
get_odds(6, 35)
# "1 in 7776"
```

## My Approach

### 1. Imported the `math` Module

I imported Python's built-in `math` module to utilize its advanced combinatorial functions.

```python
import math
```

The mathematical formula for finding the number of ways to roll a specific sum requires calculating binomial coefficients, which `math` provides efficiently.

### 2. Formulated the Mathematical Model

To find the exact number of successful combinations for rolling a target sum s with n dice, each having f sides, I implemented the inclusion-exclusion principle. 

The generalized mathematical formula is:

\[N(n, s, f) = \sum_{i=0}^{\lfloor \frac{s - n}{f} \rfloor} (-1)^i \binom{n}{i} \binom{s - i \cdot f - 1}{n - 1}\]

I assigned local variables to clearly map this equation:
```python
n = dice
s = target
f = 6
```

### 3. Calculated the Loop Obergrenze

The formula does not need to run indefinitely; it has a precise mathematical upper bound. I calculated the maximum index `i` using `math.floor()`.

```python
i = math.floor((s - n) / f)
```

This represents the maximum number of dice that could simultaneously exceed their maximum face value (6) while trying to sum up to the target.

### 4. Initialized the Success Counter

I created a tracker variable `p` to accumulate the total number of successful dice combinations.

```python
p = 0
```

### 5. Implemented a `while` Loop for the Summation

I used a `while` loop that iterates backward from our upper bound `i` down to `0`.

```python
while i >= 0:
```

This ensures every required term of the inclusion-exclusion principle is calculated.

### 6. Executed the Core Alternating Formula

Inside the loop, I calculated the combinations and added them to `p`. The term uses `(-1)**i` to alternate between adding and subtracting, which dynamically corrects for overlapping combinations.

```python
p += (-1)**i * math.comb(n, i) * math.comb(s - i * f - 1, n - 1)
i -= 1
```

I used `math.comb()` to handle the binomial coefficients \(\binom{n}{i}\) and \(\binom{s - i \cdot f - 1}{n - 1}\). 

### 7. Evaluated Total Combinations

The total number of possible outcomes when rolling n six-sided dice is calculated by raising the number of sides to the power of the number of dice:

```python
f**n
```

For example, with 3 dice, the total combinations are 6³ = 216.

### 8. Handled Impossible Edge Cases

To prevent issues with impossible scenarios where the probability might be zero, I added an explicit safeguard.

```python
if p == 0:
    return "0 in 1"
```

This prevents a `ZeroDivisionError` in the next phase of the calculation.

### 9. Transformed and Rounded to the "1 in X" Format

Since the challenge requires forcing a `"1 in X"` format (even for mathematically un-reducible fractions like 5/324), I divided the total combinations by our successful combinations and applied the `round()` function.

```python
elif p > 0:
    rounded_integer = round((f**n)/p)
```

For instance, when rolling 4 dice for a target of 7, the exact probability is 5/324. Dividing 324 / 5 yields 64.8. Rounding 64.8 brings it to the nearest whole integer: `65`.

### 10. Returned the Formatted Output String

Finally, I embedded the rounded value into an f-string to match the exact output template requested by the challenge.

```python
return f"1 in {rounded_integer}"
```

This completes the function, cleanly producing outputs like `"1 in 65"` and `"1 in 111"`, satisfying all the strict test assertions.

## Final Solution Code

```python
import math

def get_odds(dice, target):
    n = dice
    s = target
    f = 6
    i = math.floor((s - n) / f)
    p = 0

    while i >= 0:
        p += (-1)**i * math.comb(n, i) * math.comb(s - i * f - 1, n - 1)
        i -= 1
    
    if p == 0:
        return "0 in 1"
    elif p > 0:
        rounded_integer = round((f**n)/p)
        return f"1 in {rounded_integer}"
```

