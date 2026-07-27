# Today I Completed a Python Pronic Number Challenge

Today I completed a Python challenge called **Pronic Number**.

The challenge focused on determining whether a number can be written as the product of two consecutive integers.

To solve the challenge, I worked with:

* Conditional statements
* Sets
* `for` loops
* The modulo operator
* Integer division
* Square roots
* Early `return` statements

---

# Challenge: Pronic Number

## The Goal

Develop a Python function called `is_pronic(n)` that determines whether a given number is a pronic number.

A pronic number is the product of two consecutive integers.

The general form is:

```text
n = k × (k + 1)
```

For example:

```text
6 = 2 × 3
```

The numbers `2` and `3` are consecutive integers.

Therefore:

```python
is_pronic(6)
# True
```

Another example is:

```text
12 = 3 × 4
```

Therefore:

```python
is_pronic(12)
# True
```

However, the number `15` cannot be written as the product of two consecutive nonnegative integers.

Therefore:

```python
is_pronic(15)
# False
```

## The Tests

The function must pass the following tests:

```python
is_pronic(6)
# True
```

The number `6` is pronic because:

```text
2 × 3 = 6
```

```python
is_pronic(15)
# False
```

No two consecutive nonnegative integers have a product of `15`.

```python
is_pronic(12)
# True
```

The number `12` is pronic because:

```text
3 × 4 = 12
```

```python
is_pronic(132)
# True
```

The number `132` is pronic because:

```text
11 × 12 = 132
```

```python
is_pronic(80)
# False
```

The number `80` cannot be written as the product of two consecutive nonnegative integers.

```python
is_pronic(0)
# True
```

The number `0` is pronic because:

```text
0 × 1 = 0
```

---

## My Approach

My solution first handles negative numbers and zero as special cases.

It then finds all positive divisors of `n`.

After collecting the divisors, the function checks whether one of them satisfies the pronic-number formula:

```text
number × (number + 1) = n
```

If such a number exists, the function returns `True`.

Otherwise, it returns `False`.

---

### 1. Handled Negative Numbers

I first checked whether `n` is negative:

```python
if n < 0:
    return False
```

My solution only considers products of consecutive nonnegative integers.

These products cannot be negative:

```text
0 × 1 = 0
1 × 2 = 2
2 × 3 = 6
3 × 4 = 12
```

Therefore, when `n` is negative, the function immediately returns:

```python
False
```

Using `return` ends the function immediately, so the remaining code is not executed.

---

### 2. Handled Zero as a Special Case

I then checked whether `n` is equal to zero:

```python
if n == 0:
    return True
```

Zero is a pronic number because:

```text
0 × 1 = 0
```

This condition is necessary because the divisor loop starts at `1`.

Without the special case, the value `0` would not be tested as the first number in the product.

Once the function returns `True`, the rest of the function is skipped.

Because of this, an `else` block is not required.

---

### 3. Created an Empty Set

I created an empty set called `result`:

```python
result = set()
```

The set stores all divisors found by the function.

A set is useful because it stores every value only once.

For example:

```python
numbers = set()

numbers.add(2)
numbers.add(3)
numbers.add(2)
```

The result is:

```python
{2, 3}
```

The number `2` is not stored twice.

This is especially useful when checking square numbers.

For example, when:

```text
n = 36
```

one divisor pair is:

```text
6 × 6 = 36
```

The function attempts to add `6` twice:

```python
result.add(6)
result.add(36 // 6)
```

However:

```python
36 // 6
```

is also:

```text
6
```

Because `result` is a set, the number `6` is stored only once.

---

### 4. Checked Possible Divisors up to the Square Root

I used the following loop:

```python
for i in range(1, int(n ** 0.5) + 1):
```

The expression:

```python
n ** 0.5
```

calculates the square root of `n`.

Mathematically:

```text
n⁰·⁵ = n¹⁄² = √n
```

For example:

```python
6 ** 0.5
```

is approximately:

```text
2.449
```

The `int()` function removes the decimal part:

```python
int(6 ** 0.5)
# 2
```

The function then adds `1`:

```python
int(6 ** 0.5) + 1
# 3
```

The range becomes:

```python
range(1, 3)
```

The final value of a range is not included, so this range generates:

```text
1, 2
```

Therefore, the function tests the numbers `1` and `2`.

---

### 5. Used the Square Root to Avoid Unnecessary Checks

Divisors occur in pairs.

For the number `36`, the divisor pairs are:

```text
1 × 36
2 × 18
3 × 12
4 × 9
6 × 6
```

Once the function reaches the square root of `36`, it already knows every divisor pair.

The square root is:

```text
√36 = 6
```

Testing values greater than `6` would only find the same pairs in reverse order:

```text
9 × 4
12 × 3
18 × 2
36 × 1
```

Therefore, the function only needs to test possible divisors up to the square root of `n`.

This makes the divisor search more efficient than checking every number between `1` and `n`.

---

### 6. Used the Modulo Operator to Find Divisors

Inside the loop, I used:

```python
if n % i == 0:
```

The modulo operator `%` returns the remainder of a division.

For example:

```python
6 % 2
# 0
```

The number `6` can be divided evenly by `2`, so the remainder is zero.

Therefore, `2` is a divisor of `6`.

Another example is:

```python
6 % 4
# 2
```

The division leaves a remainder of `2`.

Therefore, `4` is not a divisor of `6`.

The condition:

```python
n % i == 0
```

is true only when `i` divides `n` without a remainder.

---

### 7. Added Both Divisors of Each Pair

When the function finds a divisor, it adds two values:

```python
result.add(i)
result.add(n // i)
```

The first value is the divisor being tested:

```python
i
```

The second value is its partner divisor:

```python
n // i
```

For example, when:

```text
n = 6
i = 1
```

the function adds:

```python
result.add(1)
result.add(6 // 1)
```

The partner divisor is:

```python
6 // 1
# 6
```

The set now contains:

```python
{1, 6}
```

During the next iteration:

```text
i = 2
```

The function adds:

```python
result.add(2)
result.add(6 // 2)
```

The partner divisor is:

```python
6 // 2
# 3
```

The completed set contains:

```python
{1, 2, 3, 6}
```

---

### 8. Used Integer Division for the Partner Divisor

The operator:

```python
//
```

performs integer division.

It returns a whole-number result.

For example:

```python
6 // 2
# 3
```

Because the modulo condition has already confirmed that `i` is a divisor, the division does not have a remainder.

Therefore, `n // i` gives the corresponding partner divisor.

For example:

```text
12 ÷ 3 = 4
```

In Python:

```python
12 // 3
# 4
```

The divisor pair is therefore:

```text
3 and 4
```

---

### 9. Checked Every Divisor

After collecting the divisors, I used another loop:

```python
for number in result:
```

This loop visits every number stored in the set.

For `n = 6`, the set contains:

```python
{1, 2, 3, 6}
```

The loop checks these values one at a time.

The order of a set is not guaranteed, but the order does not matter in this solution.

The function only needs to find at least one number that satisfies the required condition.

---

### 10. Checked the Pronic-Number Formula

Inside the second loop, I used:

```python
if number * (number + 1) == n:
```

This checks whether `number` and the next integer produce `n`.

For example, when:

```text
number = 2
```

the expression becomes:

```python
2 * (2 + 1)
```

This simplifies to:

```text
2 × 3 = 6
```

If:

```text
n = 6
```

the condition is true.

The function then returns:

```python
True
```

---

### 11. Returned `True` When a Match Was Found

When a divisor satisfies the formula, the function executes:

```python
return True
```

The function stops immediately after finding a valid pair.

It does not need to check the remaining divisors.

For example, for `n = 132`, the number `11` satisfies:

```text
11 × 12 = 132
```

As soon as the function checks `11`, it returns `True`.

---

### 12. Returned `False` After the Entire Loop

If none of the divisors satisfies the pronic-number formula, the function returns:

```python
return False
```

This statement must be placed outside the loop.

The following version would be incorrect:

```python
for number in result:
    if number * (number + 1) == n:
        return True
    else:
        return False
```

This would return `False` immediately after the first unsuccessful check.

For example, when checking `6`, the first tested value could be `1`:

```text
1 × 2 = 2
```

Because `2` is not equal to `6`, the incorrect version would immediately return `False`.

It would never get the opportunity to test:

```text
2 × 3 = 6
```

Therefore, `return False` is placed after the loop:

```python
for number in result:
    if number * (number + 1) == n:
        return True

return False
```

This means:

1. Check every possible number.
2. Return `True` immediately if a match is found.
3. Return `False` only when the complete loop finishes without a match.

---

## The Final Function

```python
def is_pronic(n):
    if n < 0:
        return False

    if n == 0:
        return True

    result = set()

    for i in range(1, int(n ** 0.5) + 1):
        if n % i == 0:
            result.add(i)
            result.add(n // i)

    for number in result:
        if number * (number + 1) == n:
            return True

    return False
```

---

## How the Function Processes `6`

The function is called like this:

```python
is_pronic(6)
```

First, it checks:

```python
6 < 0
```

This is false.

It then checks:

```python
6 == 0
```

This is also false.

The function creates an empty set:

```python
result = set()
```

The loop range is calculated:

```python
int(6 ** 0.5) + 1
```

The square root of `6` is approximately:

```text
2.449
```

After applying `int()`:

```text
2
```

After adding `1`:

```text
3
```

The range is:

```python
range(1, 3)
```

It generates:

```text
1, 2
```

### First iteration

```text
i = 1
```

The condition is:

```python
6 % 1 == 0
```

This is true.

The function adds:

```python
result.add(1)
result.add(6 // 1)
```

The set becomes:

```python
{1, 6}
```

### Second iteration

```text
i = 2
```

The condition is:

```python
6 % 2 == 0
```

This is true.

The function adds:

```python
result.add(2)
result.add(6 // 2)
```

The set now contains:

```python
{1, 2, 3, 6}
```

The second loop checks the values in the set.

When:

```text
number = 1
```

the calculation is:

```text
1 × 2 = 2
```

This is not equal to `6`.

When:

```text
number = 2
```

the calculation is:

```text
2 × 3 = 6
```

The condition is true, so the function returns:

```python
True
```

Therefore:

```python
is_pronic(6)
# True
```

---

## How the Function Processes `15`

The divisors of `15` are:

```python
{1, 3, 5, 15}
```

The function checks:

```text
1 × 2 = 2
3 × 4 = 12
5 × 6 = 30
15 × 16 = 240
```

None of these products is equal to `15`.

The loop finishes without finding a match.

Therefore, the function returns:

```python
False
```

So:

```python
is_pronic(15)
# False
```

---

## How the Function Processes `12`

The divisors of `12` are:

```python
{1, 2, 3, 4, 6, 12}
```

The function eventually checks:

```text
3 × 4 = 12
```

The condition is true.

Therefore:

```python
is_pronic(12)
# True
```

---

## How the Function Processes `132`

The divisors include:

```text
1, 2, 3, 4, 6, 11, 12, 22, 33, 44, 66, 132
```

The function checks whether any divisor multiplied by its successor produces `132`.

When:

```text
number = 11
```

the calculation is:

```text
11 × 12 = 132
```

The condition is true.

Therefore:

```python
is_pronic(132)
# True
```

---

## How the Function Processes `80`

The divisors of `80` include:

```text
1, 2, 4, 5, 8, 10, 16, 20, 40, 80
```

Some relevant products are:

```text
8 × 9 = 72
10 × 11 = 110
```

There is no integer `number` for which:

```text
number × (number + 1) = 80
```

Therefore:

```python
is_pronic(80)
# False
```

---

## How the Function Processes `0`

The function is called with:

```python
is_pronic(0)
```

The first condition is:

```python
0 < 0
```

This is false.

The next condition is:

```python
0 == 0
```

This is true.

The function immediately returns:

```python
True
```

This matches the mathematical calculation:

```text
0 × 1 = 0
```

Therefore:

```python
is_pronic(0)
# True
```

---

## Why This Solution Works

A pronic number must have the form:

```text
k × (k + 1)
```

If `n` is pronic, then `k` must be a divisor of `n`.

For example:

```text
132 = 11 × 12
```

The number `11` is therefore a divisor of `132`.

My function first finds every positive divisor of `n`.

It then checks whether any divisor can act as the first number in a pair of consecutive integers.

The general process is:

1. Reject negative numbers.
2. Return `True` for zero.
3. Create an empty set for the divisors.
4. Check possible divisors up to the square root of `n`.
5. Use `%` to determine whether a number is a divisor.
6. Add both numbers from each divisor pair.
7. Visit every collected divisor.
8. Calculate `number * (number + 1)`.
9. Return `True` when the product equals `n`.
10. Return `False` if no valid number is found.

---

## Possible Simpler Approach

The task can also be solved without first creating a complete set of divisors.

Because the function only needs to find a number satisfying:

```text
number × (number + 1) = n
```

it could test possible values directly:

```python
def is_pronic(n):
    if n < 0:
        return False

    for number in range(int(n ** 0.5) + 1):
        if number * (number + 1) == n:
            return True

    return False
```

This version requires less memory because it does not store all divisors.

However, my original solution is still valid.

It also helped me practise how divisor pairs, sets, modulo operations, integer division, and square roots work.

---

# Conclusion

This challenge required both mathematical reasoning and Python programming.

The mathematical part was recognizing that a pronic number is created by multiplying two consecutive integers:

```text
n = k × (k + 1)
```

The programming part involved:

```text
- Handling special cases
- Finding divisors
- Using the modulo operator
- Using integer division
- Storing unique values in a set
- Limiting a search with the square root
- Checking values with a for loop
- Returning a Boolean result
```

The special cases ensure that negative numbers return `False` and zero returns `True`.

The first loop efficiently finds the divisors of `n`.

The second loop checks whether one of these divisors and its successor produce the original number.

This challenge helped me improve my understanding of sets, divisor pairs, square roots, conditional statements, loops, integer division, the modulo operator, and the correct placement of `return` statements.

