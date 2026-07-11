# Today I Completed the Following Python Programming Task

## Five Dice

## The Goal

Develop a Python function called `five_dice(dice)` that receives a list containing five dice values and returns the best possible hand.

Every die has a value from `1` to `6`.

The possible hands are ranked from lowest to highest:

| Hand                | Description                                               |
| ------------------- | --------------------------------------------------------- |
| `"no pair"`         | No pair or better                                         |
| `"pair"`            | Two dice with the same value                              |
| `"two pair"`        | Two different pairs                                       |
| `"three of a kind"` | Three dice with the same value                            |
| `"small straight"`  | Four consecutive values                                   |
| `"large straight"`  | Five consecutive values                                   |
| `"full house"`      | Three dice with one value and two dice with another value |
| `"four of a kind"`  | Four dice with the same value                             |
| `"five of a kind"`  | All five dice have the same value                         |

The function must return the name of the highest-ranking hand found in the list.

## The Tests

The function should correctly handle examples such as:

```python
five_dice([4, 4, 4, 4, 4])
# "five of a kind"
```

```python
five_dice([2, 2, 2, 2, 5])
# "four of a kind"
```

```python
five_dice([3, 3, 3, 6, 6])
# "full house"
```

```python
five_dice([1, 2, 3, 4, 5])
# "large straight"
```

```python
five_dice([1, 2, 3, 4, 4])
# "small straight"
```

```python
five_dice([2, 2, 2, 4, 6])
# "three of a kind"
```

```python
five_dice([2, 2, 5, 5, 6])
# "two pair"
```

```python
five_dice([1, 3, 3, 5, 6])
# "pair"
```

```python
five_dice([1, 2, 3, 5, 6])
# "no pair"
```

## My Approach

### 1. Created a List to Count the Dice Values

Instead of sorting the original list, I created a second list called `count_values`.

```python
count_values = [0, 0, 0, 0, 0, 0]
```

Each position represents one possible dice value:

| Index | Dice value |
| ----: | ---------: |
|   `0` |        `1` |
|   `1` |        `2` |
|   `2` |        `3` |
|   `3` |        `4` |
|   `4` |        `5` |
|   `5` |        `6` |

The value stored at each position shows how often that dice value occurred.

For example:

```python
[0, 3, 0, 1, 0, 1]
```

means:

* The value `2` occurred three times.
* The value `4` occurred once.
* The value `6` occurred once.

### 2. Iterated Through the Dice

I used a loop to go through every die in the input list.

```python
for die in dice:
```

For each die, I calculated the correct position in `count_values`.

Because list indexes start at `0`, I subtracted `1` from the dice value.

```python
index = die - 1
```

For example:

* A dice value of `1` uses index `0`.
* A dice value of `2` uses index `1`.
* A dice value of `6` uses index `5`.

### 3. Increased the Correct Counter

After finding the correct index, I increased the value stored at that position.

```python
count_values[index] += 1
```

For example, the dice:

```python
[2, 4, 2, 6, 2]
```

produce the following counter list:

```python
[0, 3, 0, 1, 0, 1]
```

The value `2` occurred three times, so this hand contains a three of a kind.

### 4. Checked the Hands from Highest to Lowest

The order of the conditions is important.

Some hands also contain the properties of weaker hands.

For example, a full house contains both:

* a three of a kind
* a pair

If I checked for a three of a kind first, the function would return the weaker result and never reach the full-house condition.

Therefore, I checked the strongest hands first.

### 5. Checked for Five of a Kind

A five of a kind exists when one value occurs five times.

This means that the number `5` must be present in `count_values`.

```python
if 5 in count_values:
    return "five of a kind"
```

For example:

```python
[4, 4, 4, 4, 4]
```

produces:

```python
[0, 0, 0, 5, 0, 0]
```

### 6. Checked for Four of a Kind

A four of a kind exists when one value occurs four times.

```python
elif 4 in count_values:
    return "four of a kind"
```

For example:

```python
[2, 2, 2, 2, 5]
```

produces:

```python
[0, 4, 0, 0, 1, 0]
```

### 7. Checked for a Full House

A full house contains one value that occurs three times and another value that occurs twice.

Therefore, `count_values` must contain both a `3` and a `2`.

```python
elif 3 in count_values and 2 in count_values:
    return "full house"
```

For example:

```python
[3, 3, 3, 6, 6]
```

produces:

```python
[0, 0, 3, 0, 0, 2]
```

### 8. Checked for a Large Straight

A large straight contains five consecutive values.

There are only two possible large straights:

```python
[1, 2, 3, 4, 5]
```

or:

```python
[2, 3, 4, 5, 6]
```

In `count_values`, this means that either the first five positions or the last five positions must all be greater than zero.

```python
elif (
    count_values[0] > 0
    and count_values[1] > 0
    and count_values[2] > 0
    and count_values[3] > 0
    and count_values[4] > 0
) or (
    count_values[1] > 0
    and count_values[2] > 0
    and count_values[3] > 0
    and count_values[4] > 0
    and count_values[5] > 0
):
    return "large straight"
```

For example:

```python
[1, 2, 3, 4, 5]
```

produces:

```python
[1, 1, 1, 1, 1, 0]
```

### 9. Checked for a Small Straight

A small straight contains four consecutive values.

There are three possible groups:

```python
[1, 2, 3, 4]
```

```python
[2, 3, 4, 5]
```

```python
[3, 4, 5, 6]
```

I checked whether all four positions in at least one of these groups were greater than zero.

```python
elif (
    count_values[0] > 0
    and count_values[1] > 0
    and count_values[2] > 0
    and count_values[3] > 0
) or (
    count_values[1] > 0
    and count_values[2] > 0
    and count_values[3] > 0
    and count_values[4] > 0
) or (
    count_values[2] > 0
    and count_values[3] > 0
    and count_values[4] > 0
    and count_values[5] > 0
):
    return "small straight"
```

The counters do not have to be exactly `1`.

For example:

```python
[1, 2, 3, 4, 4]
```

produces:

```python
[1, 1, 1, 2, 0, 0]
```

The values `1`, `2`, `3`, and `4` are all present, so the hand is a small straight.

### 10. Checked for Three of a Kind

If the hand was not a full house or a straight, I checked whether one value occurred three times.

```python
elif 3 in count_values:
    return "three of a kind"
```

For example:

```python
[2, 2, 2, 4, 6]
```

produces:

```python
[0, 3, 0, 1, 0, 1]
```

### 11. Checked for Two Pair

For two pair, two different dice values must each occur twice.

I used the list method `.count()` to check how often the number `2` appeared inside `count_values`.

```python
elif count_values.count(2) == 2:
    return "two pair"
```

For example:

```python
[2, 2, 5, 5, 6]
```

produces:

```python
[0, 2, 0, 0, 2, 1]
```

The counter value `2` appears twice, so there are two different pairs.

### 12. Checked for a Pair

A pair exists when at least one value occurs twice.

Because two pair was already checked before this condition, checking whether `2` is present is enough.

```python
elif 2 in count_values:
    return "pair"
```

For example:

```python
[1, 3, 3, 5, 6]
```

produces:

```python
[1, 0, 2, 0, 1, 1]
```

### 13. Returned No Pair

If none of the previous conditions matched, the hand does not contain a pair or any stronger combination.

```python
else:
    return "no pair"
```

For example:

```python
[1, 2, 3, 5, 6]
```

produces:

```python
[1, 1, 1, 0, 1, 1]
```

There is no pair and no sequence of four consecutive values.

## The Final Function

```python
def five_dice(dice):
    count_values = [0, 0, 0, 0, 0, 0]

    for die in dice:
        index = die - 1
        count_values[index] += 1

    if 5 in count_values:
        return "five of a kind"

    elif 4 in count_values:
        return "four of a kind"

    elif 3 in count_values and 2 in count_values:
        return "full house"

    elif (
        count_values[0] > 0
        and count_values[1] > 0
        and count_values[2] > 0
        and count_values[3] > 0
        and count_values[4] > 0
    ) or (
        count_values[1] > 0
        and count_values[2] > 0
        and count_values[3] > 0
        and count_values[4] > 0
        and count_values[5] > 0
    ):
        return "large straight"

    elif (
        count_values[0] > 0
        and count_values[1] > 0
        and count_values[2] > 0
        and count_values[3] > 0
    ) or (
        count_values[1] > 0
        and count_values[2] > 0
        and count_values[3] > 0
        and count_values[4] > 0
    ) or (
        count_values[2] > 0
        and count_values[3] > 0
        and count_values[4] > 0
        and count_values[5] > 0
    ):
        return "small straight"

    elif 3 in count_values:
        return "three of a kind"

    elif count_values.count(2) == 2:
        return "two pair"

    elif 2 in count_values:
        return "pair"

    else:
        return "no pair"
```

## Why This Solution Works

The function first converts the five dice into a list of frequencies.

This makes it easy to determine how often every dice value appears.

The function then checks the possible hands from the highest rank to the lowest rank.

The general process is:

1. Create six counters for the possible dice values.
2. Iterate through the five dice.
3. Convert every dice value into the correct list index.
4. Increase the counter at that position.
5. Check for five of a kind.
6. Check for four of a kind.
7. Check for a full house.
8. Check for a large straight.
9. Check for a small straight.
10. Check for three of a kind.
11. Check for two pair.
12. Check for one pair.
13. Return no pair if no stronger hand was found.

Checking the hands in this order ensures that the function always returns the strongest possible result.

This challenge helped me understand how list indexes can be used to count values and how the order of conditional statements affects the final result.

