# Today I Completed the Following Python Programming Task

## Contrast Rating 1

## The Goal

Develop a Python function called `get_contrast_rating(ratio, is_large_text)` that receives:

* A contrast ratio as a string
* A Boolean value indicating whether the text is large

The function must return the correct WCAG contrast rating.

The possible ratings are:

| Rating   | Normal Text | Large Text  |
| -------- | ----------- | ----------- |
| `"AAA"`  | `7.0+`      | `4.5+`      |
| `"AA"`   | `4.5+`      | `3.0+`      |
| `"Fail"` | Below `4.5` | Below `3.0` |

The required rating depends on whether the text is normal-sized or large.

## The Tests

The function should correctly handle examples such as:

```python
get_contrast_rating("7.5", False)
# "AAA"
```

```python
get_contrast_rating("4.8", False)
# "AA"
```

```python
get_contrast_rating("4.2", False)
# "Fail"
```

```python
get_contrast_rating("4.5", True)
# "AAA"
```

```python
get_contrast_rating("3.0", True)
# "AA"
```

```python
get_contrast_rating("2.7", False)
# "Fail"
```

## My Approach

### 1. Converted the Contrast Ratio into a Decimal Number

The `ratio` parameter is provided as a string.

For example:

```python
"7.5"
```

A string cannot be compared directly with decimal numbers such as `7.0` or `4.5`.

Therefore, I converted the string into a floating-point number using `float()`.

```python
new_ratio = float(ratio)
```

After the conversion, `"7.5"` becomes the decimal number `7.5`.

Using `float()` is important because the contrast ratios can contain decimal places.

### 2. Checked Whether the Text Is Large

The `is_large_text` parameter is a Boolean value.

It can contain one of two values:

* `True`: The text is large.
* `False`: The text is normal-sized.

I used an `if` statement to determine which set of contrast requirements should be applied.

```python
if is_large_text:
```

When this condition is true, the function uses the thresholds for large text.

Otherwise, it uses the thresholds for normal text.

### 3. Checked the Ratings for Large Text

Large text receives an `"AAA"` rating when its contrast ratio is at least `4.5`.

```python
if new_ratio >= 4.5:
    return "AAA"
```

For example:

```python
get_contrast_rating("4.5", True)
```

returns:

```python
"AAA"
```

The value `4.5` is included because the requirement is `4.5` or higher.

### 4. Checked for an AA Rating for Large Text

If the contrast ratio is below `4.5`, I checked whether it is at least `3.0`.

```python
elif new_ratio >= 3.0:
    return "AA"
```

For example:

```python
get_contrast_rating("3.0", True)
```

returns:

```python
"AA"
```

### 5. Returned Fail for Large Text

If the contrast ratio is below `3.0`, it does not meet the minimum requirement for large text.

```python
else:
    return "Fail"
```

For example:

```python
get_contrast_rating("2.8", True)
```

returns:

```python
"Fail"
```

### 6. Checked the Ratings for Normal Text

When `is_large_text` is `False`, the function uses the requirements for normal text.

Normal text needs a contrast ratio of at least `7.0` to receive an `"AAA"` rating.

```python
if new_ratio >= 7.0:
    return "AAA"
```

For example:

```python
get_contrast_rating("7.5", False)
```

returns:

```python
"AAA"
```

### 7. Checked for an AA Rating for Normal Text

If the contrast ratio is below `7.0`, I checked whether it is at least `4.5`.

```python
elif new_ratio >= 4.5:
    return "AA"
```

For example:

```python
get_contrast_rating("4.8", False)
```

returns:

```python
"AA"
```

### 8. Returned Fail for Normal Text

If the contrast ratio is below `4.5`, the normal text does not meet the minimum contrast requirement.

```python
else:
    return "Fail"
```

For example:

```python
get_contrast_rating("4.2", False)
```

returns:

```python
"Fail"
```

## Why the Order of the Conditions Is Important

I checked the highest rating first.

For normal text, a contrast ratio of `7.5` satisfies both of these conditions:

* It is at least `7.0`.
* It is also at least `4.5`.

If I checked the `"AA"` requirement first, the function could return `"AA"` even though the contrast ratio qualifies for `"AAA"`.

Therefore, the conditions must be checked from the highest rating to the lowest rating:

1. Check for `"AAA"`.
2. Check for `"AA"`.
3. Return `"Fail"` if neither condition matches.

The same logic applies to large text.

## The Final Function

```python
def get_contrast_rating(ratio, is_large_text):

    new_ratio = float(ratio)

    if is_large_text:
        if new_ratio >= 4.5:
            return "AAA"
        elif new_ratio >= 3.0:
            return "AA"
        else:
            return "Fail"
    else:
        if new_ratio >= 7.0:
            return "AAA"
        elif new_ratio >= 4.5:
            return "AA"
        else:
            return "Fail"
```

## Why This Solution Works

The function first converts the contrast ratio from a string into a decimal number.

It then uses the Boolean value `is_large_text` to choose the correct contrast requirements.

For large text, the function checks:

1. Whether the ratio is at least `4.5` for `"AAA"`.
2. Whether the ratio is at least `3.0` for `"AA"`.
3. Otherwise, it returns `"Fail"`.

For normal text, the function checks:

1. Whether the ratio is at least `7.0` for `"AAA"`.
2. Whether the ratio is at least `4.5` for `"AA"`.
3. Otherwise, it returns `"Fail"`.

Checking the ratings from highest to lowest ensures that the function always returns the best possible rating.

This challenge helped me understand how to convert strings into floating-point numbers, how Boolean values can control program logic, and why the order of conditional statements is important.

