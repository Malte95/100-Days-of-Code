# Today I Completed the Following Python Programming Task

## Round to Nearest Multiple

## The Goal

Develop a Python function called `round_to_nearest_multiple(num, multiple)` that rounds the first integer to the nearest multiple of the second integer.

The function must:

* receive two integers
* divide the number by the multiple
* round the result to the nearest whole number
* multiply the rounded result by the multiple
* return the nearest multiple

For example:

```python
round_to_nearest_multiple(5, 3)
```

should return:

```python
6
```

This is because the closest multiples of `3` are:

```python
3
6
```

The number `5` is closer to `6` than to `3`.

## The Tests

The function needs to pass the following tests:

```python
round_to_nearest_multiple(5, 3)
# 6
```

```python
round_to_nearest_multiple(17, 4)
# 16
```

```python
round_to_nearest_multiple(43, 5)
# 45
```

```python
round_to_nearest_multiple(38, 11)
# 33
```

```python
round_to_nearest_multiple(93, 12)
# 96
```

## My Approach

### 1. Divided the Number by the Multiple

First, I divided `num` by `multiple`.

```python
num / multiple
```

This shows how many times the multiple fits into the number.

For example:

```python
17 / 4
```

results in:

```python
4.25
```

This means that `17` is a little more than four groups of `4`.

### 2. Rounded the Result

Next, I used Python’s `round()` function.

```python
round(num / multiple)
```

This rounds the division result to the nearest whole number.

For example:

```python
round(17 / 4)
```

becomes:

```python
round(4.25)
```

which returns:

```python
4
```

### 3. Multiplied by the Multiple Again

After rounding, I multiplied the result by `multiple`.

```python
round(num / multiple) * multiple
```

For example:

```python
round(17 / 4) * 4
```

becomes:

```python
4 * 4
```

which returns:

```python
16
```

This gives the closest multiple of `4` to the original number `17`.

### 4. Stored the Result in a Variable

I stored the result in a variable called `n`.

```python
n = round(num / multiple) * multiple
```

This makes the code easier to read because the calculation has a clear name before it is returned.

### 5. Returned the Final Result

Finally, I returned `n`.

```python
return n
```

## The Final Function

```python
def round_to_nearest_multiple(num, multiple):
    n = round(num / multiple) * multiple

    return n
```

## Why This Solution Works

The function follows the same process for every pair of numbers:

1. Divide the number by the multiple.
2. Round the result to the nearest whole number.
3. Multiply that whole number by the multiple.
4. Return the result.

This makes the function work for different numbers and different multiples.

For example:

```python
round_to_nearest_multiple(43, 5)
```

First:

```python
43 / 5
```

becomes:

```python
8.6
```

Then:

```python
round(8.6)
```

becomes:

```python
9
```

Finally:

```python
9 * 5
```

returns:

```python
45
```

So the nearest multiple of `5` to `43` is `45`.

