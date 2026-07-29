# Today I Completed the Following Python Programming Task

## Contrast Rating 2

## The Goal

Develop a Python function called `get_contrast_rating(l1, l2, is_large_text)` that receives two relative luminance values and a Boolean value indicating whether the text is large.

The function should calculate the contrast ratio between the two luminance values and return the corresponding WCAG contrast rating.

The possible ratings are:

```text
AAA
AA
Fail
```

The first luminance value, `l1`, always represents the lighter color.

The second luminance value, `l2`, represents the darker color.

To calculate the contrast ratio, `0.05` must first be added to both luminance values.

The general calculation is:

```text
contrast ratio = (lighter luminance + 0.05) ÷ (darker luminance + 0.05)
```

In Python, this calculation can be written as:

```python
contrast_ratio = (l1 + 0.05) / (l2 + 0.05)
```

The rating depends on both the calculated contrast ratio and the text size.

| Rating   | Normal Text | Large Text |
| -------- | ----------: | ---------: |
| `"AAA"`  |        7.0+ |       4.5+ |
| `"AA"`   |        4.5+ |       3.0+ |
| `"Fail"` |   Below 4.5 |  Below 3.0 |

For normal text:

```text
AAA: contrast ratio of at least 7.0
AA: contrast ratio of at least 4.5
Fail: contrast ratio below 4.5
```

For large text:

```text
AAA: contrast ratio of at least 4.5
AA: contrast ratio of at least 3.0
Fail: contrast ratio below 3.0
```

Large text has lower contrast requirements because larger characters are generally easier to read.

## The Tests

The first test uses the maximum possible luminance difference:

```python
get_contrast_rating(1.0, 0.0, False)
# "AAA"
```

The calculation is:

```text
(1.0 + 0.05) ÷ (0.0 + 0.05)
```

After adding `0.05`:

```text
1.05 ÷ 0.05
```

The result is:

```text
21.0
```

Because the text is normal text, the function uses the normal-text thresholds.

A contrast ratio of `21.0` is greater than `7.0`, so the result is:

```text
AAA
```

Another normal-text example is:

```python
get_contrast_rating(0.9015, 0.1364, False)
# "AA"
```

The calculation is:

```text
(0.9015 + 0.05) ÷ (0.1364 + 0.05)
```

This becomes:

```text
0.9515 ÷ 0.1864
```

The contrast ratio is approximately:

```text
5.1046
```

The value is below `7.0`, so it does not receive an `"AAA"` rating.

However, it is greater than `4.5`, so the result is:

```text
AA
```

The next normal-text example is:

```python
get_contrast_rating(0.8965, 0.1628, False)
# "Fail"
```

The calculation is:

```text
(0.8965 + 0.05) ÷ (0.1628 + 0.05)
```

This becomes:

```text
0.9465 ÷ 0.2128
```

The result is approximately:

```text
4.4478
```

This value is slightly below the minimum normal-text requirement of `4.5`.

Therefore, the result is:

```text
Fail
```

The function must also process large text.

For example:

```python
get_contrast_rating(0.7469, 0.0957, True)
# "AAA"
```

The calculation is:

```text
(0.7469 + 0.05) ÷ (0.0957 + 0.05)
```

This becomes:

```text
0.7969 ÷ 0.1457
```

The result is approximately:

```text
5.4695
```

For large text, an `"AAA"` rating requires a contrast ratio of at least `4.5`.

Because `5.4695` is greater than `4.5`, the function returns:

```text
AAA
```

Another large-text example is:

```python
get_contrast_rating(0.7489, 0.2018, True)
# "AA"
```

The calculation is:

```text
(0.7489 + 0.05) ÷ (0.2018 + 0.05)
```

This becomes:

```text
0.7989 ÷ 0.2518
```

The result is approximately:

```text
3.1728
```

This value is below the large-text `"AAA"` threshold of `4.5`.

However, it is greater than the `"AA"` threshold of `3.0`.

Therefore, the result is:

```text
AA
```

The final test is:

```python
get_contrast_rating(0.6571, 0.1974, True)
# "Fail"
```

The calculation is:

```text
(0.6571 + 0.05) ÷ (0.1974 + 0.05)
```

This becomes:

```text
0.7071 ÷ 0.2474
```

The result is approximately:

```text
2.8581
```

For large text, the minimum passing contrast ratio is `3.0`.

Because `2.8581` is below `3.0`, the function returns:

```text
Fail
```

## My Approach

### 1. Added `0.05` to the First Luminance Value

The contrast ratio formula requires adding `0.05` to both luminance values.

I first added `0.05` to `l1`:

```python
l1 += 0.05
```

The `+=` operator adds a value to an existing variable and stores the result in the same variable.

This statement is equivalent to:

```python
l1 = l1 + 0.05
```

For example, when:

```text
l1 = 1.0
```

the operation becomes:

```text
1.0 + 0.05 = 1.05
```

The new value of `l1` is:

```text
1.05
```

Another example is:

```text
l1 = 0.9015
```

After adding `0.05`:

```text
0.9015 + 0.05 = 0.9515
```

Therefore, `l1` becomes:

```text
0.9515
```

### 2. Added `0.05` to the Second Luminance Value

I performed the same operation on `l2`:

```python
l2 += 0.05
```

This is equivalent to:

```python
l2 = l2 + 0.05
```

For example, when:

```text
l2 = 0.0
```

the updated value is:

```text
0.0 + 0.05 = 0.05
```

When:

```text
l2 = 0.1364
```

the updated value is:

```text
0.1364 + 0.05 = 0.1864
```

Adding `0.05` also prevents the function from dividing by zero when the darker luminance value is `0.0`.

Without the addition, this calculation would be invalid:

```text
1.0 ÷ 0.0
```

Python would raise a `ZeroDivisionError`.

After adding `0.05`, the calculation becomes:

```text
1.05 ÷ 0.05
```

This produces the valid contrast ratio:

```text
21.0
```

### 3. Calculated the Contrast Ratio

After updating both luminance values, I divided the lighter value by the darker value:

```python
quotient = l1 / l2
```

The task states that the lighter luminance value will always be the first argument.

Therefore, `l1` can be used as the numerator and `l2` as the denominator.

It is not necessary to determine which value is larger by using `max()` or `min()`.

For example:

```python
get_contrast_rating(1.0, 0.0, False)
```

After adding `0.05`, the values are:

```text
l1 = 1.05
l2 = 0.05
```

The division is:

```text
1.05 ÷ 0.05 = 21.0
```

Therefore:

```text
quotient = 21.0
```

For another example:

```python
get_contrast_rating(0.7489, 0.2018, True)
```

The updated values are:

```text
l1 = 0.7989
l2 = 0.2518
```

The calculation is:

```text
0.7989 ÷ 0.2518 ≈ 3.1728
```

Therefore:

```text
quotient ≈ 3.1728
```

The variable name `quotient` describes the result of a division.

It contains the contrast ratio that will be compared with the rating thresholds.

### 4. Checked Whether the Text Is Large

The third argument is called `is_large_text`.

It contains a Boolean value:

```text
True
```

or:

```text
False
```

When `is_large_text` is `True`, the function must use the thresholds for large text.

When it is `False`, the function must use the thresholds for normal text.

I checked the value with:

```python
if is_large_text:
```

This condition is entered when `is_large_text` is `True`.

For example:

```python
get_contrast_rating(0.7469, 0.0957, True)
```

The third argument is:

```text
True
```

Therefore, the function enters the following block:

```python
if is_large_text:
```

However, in this call:

```python
get_contrast_rating(1.0, 0.0, False)
```

the third argument is:

```text
False
```

The `if` block is skipped, and the function continues to the `else` block for normal text.

### 5. Checked the `"AAA"` Requirement for Large Text

Inside the large-text block, I first checked whether the contrast ratio is at least `4.5`:

```python
if quotient >= 4.5:
```

The `>=` operator means:

```text
greater than or equal to
```

This is important because a contrast ratio of exactly `4.5` should also receive an `"AAA"` rating for large text.

For example:

```text
5.4695 >= 4.5
```

is:

```text
True
```

Therefore, the function returns:

```python
return "AAA"
```

The `return` statement immediately ends the function and sends the result back to the caller.

For example:

```python
rating = get_contrast_rating(0.7469, 0.0957, True)
```

The value stored in `rating` is:

```text
AAA
```

### 6. Checked the `"AA"` Requirement for Large Text

If the contrast ratio is below `4.5`, the first large-text condition is `False`.

The function then checks whether the ratio is at least `3.0`:

```python
elif quotient >= 3.0:
```

The word `elif` means:

```text
else if
```

This condition is only checked when the previous condition was `False`.

For example, consider this contrast ratio:

```text
3.1728
```

The first condition is:

```text
3.1728 >= 4.5
```

This is:

```text
False
```

The next condition is:

```text
3.1728 >= 3.0
```

This is:

```text
True
```

Therefore, the function returns:

```python
return "AA"
```

### 7. Returned `"Fail"` for Large Text Below `3.0`

When the contrast ratio is below both `4.5` and `3.0`, neither passing condition is satisfied.

The function reaches:

```python
else:
    return "Fail"
```

For example:

```text
quotient = 2.8581
```

The first comparison is:

```text
2.8581 >= 4.5
```

This is:

```text
False
```

The second comparison is:

```text
2.8581 >= 3.0
```

This is also:

```text
False
```

Therefore, the function returns:

```text
Fail
```

### 8. Used the Normal-Text Thresholds Otherwise

When `is_large_text` is `False`, the function enters the outer `else` block:

```python
else:
```

This block contains the requirements for normal text.

Normal text has stricter contrast requirements than large text.

The thresholds are:

```text
AAA: 7.0
AA: 4.5
Fail: below 4.5
```

### 9. Checked the `"AAA"` Requirement for Normal Text

For normal text, I first checked whether the contrast ratio is at least `7.0`:

```python
if quotient >= 7.0:
```

For example:

```text
quotient = 21.0
```

The comparison becomes:

```text
21.0 >= 7.0
```

This is:

```text
True
```

Therefore, the function returns:

```python
return "AAA"
```

A contrast ratio of exactly `7.0` would also pass because the comparison uses `>=` instead of only `>`.

### 10. Checked the `"AA"` Requirement for Normal Text

If the normal-text contrast ratio is below `7.0`, the function checks whether it is at least `4.5`:

```python
elif quotient >= 4.5:
```

For example:

```text
quotient = 5.1046
```

The `"AAA"` comparison is:

```text
5.1046 >= 7.0
```

This is:

```text
False
```

The `"AA"` comparison is:

```text
5.1046 >= 4.5
```

This is:

```text
True
```

Therefore, the function returns:

```text
AA
```

### 11. Returned `"Fail"` for Normal Text Below `4.5`

When the normal-text contrast ratio is below `4.5`, it does not meet either passing threshold.

The function reaches:

```python
else:
    return "Fail"
```

For example:

```text
quotient = 4.4478
```

The first comparison is:

```text
4.4478 >= 7.0
```

This is:

```text
False
```

The second comparison is:

```text
4.4478 >= 4.5
```

This is also:

```text
False
```

Therefore, the result is:

```text
Fail
```

## The Final Function

```python
def get_contrast_rating(l1, l2, is_large_text):
    l1 += 0.05
    l2 += 0.05

    quotient = l1 / l2

    if is_large_text:
        if quotient >= 4.5:
            return "AAA"
        elif quotient >= 3.0:
            return "AA"
        else:
            return "Fail"

    else:
        if quotient >= 7.0:
            return "AAA"
        elif quotient >= 4.5:
            return "AA"
        else:
            return "Fail"
```

## How the Function Processes Normal Text With an `"AAA"` Rating

The function is called with:

```python
get_contrast_rating(1.0, 0.0, False)
```

The arguments are assigned to the parameters:

```text
l1 = 1.0
l2 = 0.0
is_large_text = False
```

The function adds `0.05` to `l1`:

```text
1.0 + 0.05 = 1.05
```

It then adds `0.05` to `l2`:

```text
0.0 + 0.05 = 0.05
```

The updated values are:

```text
l1 = 1.05
l2 = 0.05
```

The function calculates the quotient:

```text
1.05 ÷ 0.05 = 21.0
```

Therefore:

```text
quotient = 21.0
```

The next condition is:

```python
if is_large_text:
```

Because `is_large_text` is `False`, the function skips the large-text block.

It enters the normal-text `else` block.

The first normal-text condition checks:

```python
if quotient >= 7.0:
```

This becomes:

```text
21.0 >= 7.0
```

The condition is:

```text
True
```

The function returns:

```python
"AAA"
```

## How the Function Processes Normal Text With an `"AA"` Rating

The function is called with:

```python
get_contrast_rating(0.9015, 0.1364, False)
```

The arguments are:

```text
l1 = 0.9015
l2 = 0.1364
is_large_text = False
```

After adding `0.05`, the values become:

```text
l1 = 0.9515
l2 = 0.1864
```

The quotient is:

```text
0.9515 ÷ 0.1864 ≈ 5.1046
```

Because `is_large_text` is `False`, the function uses the normal-text conditions.

The first comparison is:

```text
5.1046 >= 7.0
```

This is:

```text
False
```

The second comparison is:

```text
5.1046 >= 4.5
```

This is:

```text
True
```

The function returns:

```python
"AA"
```

## How the Function Processes Normal Text That Fails

The function is called with:

```python
get_contrast_rating(0.8965, 0.1628, False)
```

After adding `0.05`, the values are:

```text
l1 = 0.9465
l2 = 0.2128
```

The quotient is approximately:

```text
4.4478
```

The function uses the normal-text thresholds.

The first condition checks:

```text
4.4478 >= 7.0
```

This is:

```text
False
```

The second condition checks:

```text
4.4478 >= 4.5
```

This is also:

```text
False
```

The function reaches the final `else` block and returns:

```python
"Fail"
```

## How the Function Processes Large Text With an `"AAA"` Rating

The function is called with:

```python
get_contrast_rating(0.7469, 0.0957, True)
```

The arguments are:

```text
l1 = 0.7469
l2 = 0.0957
is_large_text = True
```

After adding `0.05`, the values become:

```text
l1 = 0.7969
l2 = 0.1457
```

The quotient is approximately:

```text
5.4695
```

Because `is_large_text` is `True`, the function enters the large-text block.

The first large-text comparison is:

```text
5.4695 >= 4.5
```

This is:

```text
True
```

The function immediately returns:

```python
"AAA"
```

## How the Function Processes Large Text With an `"AA"` Rating

The function is called with:

```python
get_contrast_rating(0.7489, 0.2018, True)
```

After adding `0.05`, the values are:

```text
l1 = 0.7989
l2 = 0.2518
```

The contrast ratio is approximately:

```text
3.1728
```

The function first checks:

```text
3.1728 >= 4.5
```

This is:

```text
False
```

It then checks:

```text
3.1728 >= 3.0
```

This is:

```text
True
```

Therefore, the function returns:

```python
"AA"
```

## How the Function Processes Large Text That Fails

The function is called with:

```python
get_contrast_rating(0.6571, 0.1974, True)
```

After adding `0.05`, the values become:

```text
l1 = 0.7071
l2 = 0.2474
```

The contrast ratio is approximately:

```text
2.8581
```

The first large-text comparison is:

```text
2.8581 >= 4.5
```

This is:

```text
False
```

The second comparison is:

```text
2.8581 >= 3.0
```

This is also:

```text
False
```

The function reaches the `else` block and returns:

```python
"Fail"
```

## Additional Tests

The function can be tested using `assert` statements:

```python
assert get_contrast_rating(1.0, 0.0, False) == "AAA"
assert get_contrast_rating(0.9015, 0.1364, False) == "AA"
assert get_contrast_rating(0.8965, 0.1628, False) == "Fail"

assert get_contrast_rating(0.7469, 0.0957, True) == "AAA"
assert get_contrast_rating(0.7489, 0.2018, True) == "AA"
assert get_contrast_rating(0.6571, 0.1974, True) == "Fail"
```

The exact threshold values can also be tested.

For normal text, a contrast ratio of exactly `7.0` should return `"AAA"`.

Because the function adds `0.05` before dividing, suitable luminance values can be selected to produce that ratio.

For example:

```python
assert get_contrast_rating(0.65, 0.05, False) == "AAA"
```

The calculation is:

```text
(0.65 + 0.05) ÷ (0.05 + 0.05)
```

This becomes:

```text
0.70 ÷ 0.10 = 7.0
```

Therefore, the result is:

```text
AAA
```

A normal-text ratio of exactly `4.5` should return `"AA"`:

```python
assert get_contrast_rating(0.40, 0.05, False) == "AA"
```

The calculation is:

```text
(0.40 + 0.05) ÷ (0.05 + 0.05)
```

This becomes:

```text
0.45 ÷ 0.10 = 4.5
```

For large text, the same contrast ratio of `4.5` should return `"AAA"`:

```python
assert get_contrast_rating(0.40, 0.05, True) == "AAA"
```

A large-text ratio of exactly `3.0` should return `"AA"`:

```python
assert get_contrast_rating(0.25, 0.05, True) == "AA"
```

The calculation is:

```text
(0.25 + 0.05) ÷ (0.05 + 0.05)
```

This becomes:

```text
0.30 ÷ 0.10 = 3.0
```

These tests confirm that the `>=` comparisons correctly include the boundary values.

## A More Compact Alternative

The function can also be written by assigning the thresholds before performing the comparisons:

```python
def get_contrast_rating(l1, l2, is_large_text):
    contrast_ratio = (l1 + 0.05) / (l2 + 0.05)

    aaa_threshold = 4.5 if is_large_text else 7.0
    aa_threshold = 3.0 if is_large_text else 4.5

    if contrast_ratio >= aaa_threshold:
        return "AAA"

    if contrast_ratio >= aa_threshold:
        return "AA"

    return "Fail"
```

This version avoids writing two separate groups of rating conditions.

The expression:

```python
4.5 if is_large_text else 7.0
```

is a conditional expression.

It means:

```text
Use 4.5 when is_large_text is True.
Otherwise, use 7.0.
```

Similarly:

```python
3.0 if is_large_text else 4.5
```

means:

```text
Use 3.0 when is_large_text is True.
Otherwise, use 4.5.
```

However, the original solution is also correct.

Its separate branches make it easy to see which thresholds belong to large text and which thresholds belong to normal text.

## Why This Solution Works

The function first adds `0.05` to both relative luminance values.

It then divides the adjusted lighter luminance value by the adjusted darker luminance value.

Because the task guarantees that the lighter value is always the first argument, the function can directly calculate:

```python
l1 / l2
```

after updating both variables.

The Boolean argument `is_large_text` determines which set of WCAG thresholds must be used.

When `is_large_text` is `True`, the function uses:

```text
AAA: 4.5 or higher
AA: 3.0 or higher
Fail: below 3.0
```

When `is_large_text` is `False`, the function uses:

```text
AAA: 7.0 or higher
AA: 4.5 or higher
Fail: below 4.5
```

Within each branch, the function checks the highest rating first.

This order is important.

For example, a large-text contrast ratio of `5.0` satisfies both of these conditions:

```text
5.0 >= 4.5
5.0 >= 3.0
```

However, the correct rating is `"AAA"`, not `"AA"`.

By checking the `"AAA"` condition first, the function immediately returns the highest rating that applies.

The general process is:

1. Receive the two relative luminance values.
2. Receive the Boolean value indicating the text size.
3. Add `0.05` to the lighter luminance value.
4. Add `0.05` to the darker luminance value.
5. Divide the adjusted lighter value by the adjusted darker value.
6. Check whether the text is large.
7. Apply the large-text thresholds when the value is `True`.
8. Apply the normal-text thresholds when the value is `False`.
9. Return `"AAA"`, `"AA"`, or `"Fail"`.

This challenge helped me practise mathematical calculations in Python and understand how a formula can be translated into several programming steps.

It also helped me practise working with Boolean values and nested conditional statements.

I learned that the order of conditions matters when several threshold ranges overlap.

The function must check the highest rating first because every `"AAA"` contrast ratio also satisfies the lower `"AA"` requirement.

I also practised using `>=` to include exact boundary values such as `7.0`, `4.5`, and `3.0`.

By separating the large-text and normal-text conditions, the function clearly applies the correct accessibility requirements to each type of text.

All six provided tests passed, confirming that the contrast calculation and rating conditions work correctly.

