# Today I Completed the Following Python Programming Task

## Horoscope Match

## The Goal

Develop a Python function called `horoscope_match(sign1, sign2)` that receives two star signs and returns their compatibility percentage.

The twelve star signs are arranged in a circular wheel in the following order:

```text
Aries
Taurus
Gemini
Cancer
Leo
Virgo
Libra
Scorpio
Sagittarius
Capricorn
Aquarius
Pisces
```

After `"Pisces"`, the wheel wraps back to `"Aries"`.

The function must determine the shortest distance between the two signs on this wheel.

The compatibility depends on that distance:

| Distance | Compatibility |
| -------: | ------------- |
|      `0` | `"100%"`      |
|      `1` | `"40%"`       |
|      `2` | `"80%"`       |
|      `3` | `"30%"`       |
|      `4` | `"90%"`       |
|      `5` | `"20%"`       |
|      `6` | `"50%"`       |

## The Tests

The function should correctly handle examples such as:

```python
horoscope_match("Aries", "Aries")
# "100%"
```

Both signs are at the same position, so the distance is `0`.

```python
horoscope_match("Aries", "Taurus")
# "40%"
```

The signs are directly next to each other, so the distance is `1`.

```python
horoscope_match("Aries", "Gemini")
# "80%"
```

The distance between the two signs is `2`.

```python
horoscope_match("Aries", "Leo")
# "90%"
```

The distance between `"Aries"` and `"Leo"` is `4`.

The function must also handle the circular structure of the zodiac wheel.

For example:

```python
horoscope_match("Aries", "Pisces")
# "40%"
```

Inside the list, `"Aries"` is at index `0` and `"Pisces"` is at index `11`.

The direct difference between the indexes is `11`, but because the zodiac signs form a circle, the two signs are actually next to each other.

The shortest distance is therefore `1`.

## My Approach

### 1. Created a List of the Zodiac Signs

I created a list called `zodiac_signs` that contains all twelve star signs in the correct order.

```python
zodiac_signs = [
    "Aries",
    "Taurus",
    "Gemini",
    "Cancer",
    "Leo",
    "Virgo",
    "Libra",
    "Scorpio",
    "Sagittarius",
    "Capricorn",
    "Aquarius",
    "Pisces"
]
```

The position of each sign in the list represents its position on the zodiac wheel.

| Index | Star sign       |
| ----: | --------------- |
|   `0` | `"Aries"`       |
|   `1` | `"Taurus"`      |
|   `2` | `"Gemini"`      |
|   `3` | `"Cancer"`      |
|   `4` | `"Leo"`         |
|   `5` | `"Virgo"`       |
|   `6` | `"Libra"`       |
|   `7` | `"Scorpio"`     |
|   `8` | `"Sagittarius"` |
|   `9` | `"Capricorn"`   |
|  `10` | `"Aquarius"`    |
|  `11` | `"Pisces"`      |

### 2. Found the Position of Each Sign

I used the `.index()` method to find the position of each star sign inside the list.

```python
zodiac_signs.index(sign1)
```

and:

```python
zodiac_signs.index(sign2)
```

For example:

```python
zodiac_signs.index("Aries")
# 0
```

```python
zodiac_signs.index("Leo")
# 4
```

### 3. Calculated the Direct Distance

I subtracted the two positions to calculate the distance between the signs.

```python
zodiac_signs.index(sign1) - zodiac_signs.index(sign2)
```

However, the result could be negative depending on the order of the two signs.

For example:

```text
0 - 4 = -4
```

A distance should not be negative, so I used the built-in `abs()` function.

```python
distance = abs(
    zodiac_signs.index(sign1) - zodiac_signs.index(sign2)
)
```

`abs()` returns the absolute value of a number.

For example:

```python
abs(-4)
# 4
```

Therefore, the direct distance between `"Aries"` and `"Leo"` is `4`, regardless of the order in which the signs are passed to the function.

### 4. Considered the Circular Zodiac Wheel

The zodiac signs are not arranged in a normal straight list.

They form a circle, which means that `"Pisces"` connects back to `"Aries"`.

Because there are twelve signs, there are always two possible paths between two positions:

1. The direct path through the list.
2. The path around the other side of the wheel.

The direct path is stored in:

```python
distance
```

The distance around the other side of the wheel is:

```python
12 - distance
```

For example, with `"Aries"` and `"Pisces"`:

```text
Aries index  = 0
Pisces index = 11
```

The direct distance is:

```text
|0 - 11| = 11
```

The distance around the other side of the wheel is:

```text
12 - 11 = 1
```

The shortest distance is therefore `1`.

### 5. Selected the Shortest Path

I compared the direct distance with the distance around the other side of the wheel.

```python
if distance < 12 - distance:
    shortest_path = distance
else:
    shortest_path = 12 - distance
```

If the direct distance is smaller, it is stored in `shortest_path`.

Otherwise, the distance around the other side of the zodiac wheel is stored in `shortest_path`.

For example, with `"Aries"` and `"Leo"`:

```text
Direct distance: 4
Other direction: 12 - 4 = 8
```

Because `4` is smaller than `8`, the shortest path is `4`.

With `"Aries"` and `"Pisces"`:

```text
Direct distance: 11
Other direction: 12 - 11 = 1
```

Because `1` is smaller than `11`, the shortest path is `1`.

### 6. Handled Opposite Signs

The largest possible shortest distance on a wheel with twelve positions is `6`.

For example, `"Aries"` and `"Libra"` are opposite each other.

Their direct distance is:

```text
|0 - 6| = 6
```

The distance in the other direction is also:

```text
12 - 6 = 6
```

In this case, both paths have the same length.

The condition:

```python
distance < 12 - distance
```

is false because `6` is not smaller than `6`.

The `else` block therefore calculates:

```python
shortest_path = 12 - 6
```

The result is still `6`, so the function handles this case correctly.

### 7. Converted the Distance into a Compatibility Percentage

After finding the shortest distance, I used an `if` and `elif` chain to return the correct compatibility percentage.

For a distance of `0`:

```python
if shortest_path == 0:
    return "100%"
```

For a distance of `1`:

```python
elif shortest_path == 1:
    return "40%"
```

For a distance of `2`:

```python
elif shortest_path == 2:
    return "80%"
```

For a distance of `3`:

```python
elif shortest_path == 3:
    return "30%"
```

For a distance of `4`:

```python
elif shortest_path == 4:
    return "90%"
```

For a distance of `5`:

```python
elif shortest_path == 5:
    return "20%"
```

For a distance of `6`:

```python
elif shortest_path == 6:
    return "50%"
```

Because the shortest distance on a wheel of twelve positions can only be between `0` and `6`, these conditions cover every possible result.

## The Final Function

```python
def horoscope_match(sign1, sign2):
    zodiac_signs = [
        "Aries",
        "Taurus",
        "Gemini",
        "Cancer",
        "Leo",
        "Virgo",
        "Libra",
        "Scorpio",
        "Sagittarius",
        "Capricorn",
        "Aquarius",
        "Pisces"
    ]

    distance = abs(
        zodiac_signs.index(sign1) - zodiac_signs.index(sign2)
    )

    if distance < 12 - distance:
        shortest_path = distance
    else:
        shortest_path = 12 - distance

    if shortest_path == 0:
        return "100%"
    elif shortest_path == 1:
        return "40%"
    elif shortest_path == 2:
        return "80%"
    elif shortest_path == 3:
        return "30%"
    elif shortest_path == 4:
        return "90%"
    elif shortest_path == 5:
        return "20%"
    elif shortest_path == 6:
        return "50%"
```

## How the Function Processes `"Aries"` and `"Pisces"`

The two positions are:

```text
Aries  = index 0
Pisces = index 11
```

The direct distance is calculated:

```text
|0 - 11| = 11
```

The distance around the other side of the wheel is:

```text
12 - 11 = 1
```

The function compares the two distances:

```text
11 < 1
```

This is false, so the `else` block is executed:

```text
shortest_path = 1
```

A shortest distance of `1` returns:

```text
"40%"
```

Therefore:

```python
horoscope_match("Aries", "Pisces")
# "40%"
```

## How the Function Processes `"Aries"` and `"Leo"`

The positions are:

```text
Aries = index 0
Leo   = index 4
```

The direct distance is:

```text
|0 - 4| = 4
```

The distance in the other direction is:

```text
12 - 4 = 8
```

The function compares the distances:

```text
4 < 8
```

This is true, so:

```text
shortest_path = 4
```

A shortest distance of `4` returns:

```text
"90%"
```

Therefore:

```python
horoscope_match("Aries", "Leo")
# "90%"
```

## Why This Solution Works

The function first stores the zodiac signs in their correct circular order.

It then uses `.index()` to find the position of both signs.

The absolute difference between the positions gives the direct distance through the list.

Because the zodiac signs are arranged in a wheel, the function also calculates the distance in the opposite direction by subtracting the direct distance from `12`.

The smaller of these two distances is the shortest path between the signs.

Finally, the function converts that shortest distance into the required compatibility percentage.

The general process is:

1. Create a list containing the twelve zodiac signs.
2. Find the index of the first sign.
3. Find the index of the second sign.
4. Calculate the absolute difference between the indexes.
5. Calculate the distance around the other side of the wheel.
6. Select the shorter of the two paths.
7. Match the shortest distance with its compatibility percentage.
8. Return the percentage as a string.

This challenge helped me understand how to find elements inside a list, calculate the distance between list positions, use `abs()` to avoid negative values, and work with values arranged in a circular structure.

