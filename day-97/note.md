# Daily Coding Challenge: Golf Handicap Calculator

Today, I completed a Python coding challenge about calculating a golfer's handicap index from a list of scores and corresponding course par values.

## The Challenge

The function receives two arrays:

* one containing the golfer's scores
* one containing the corresponding par values

For each round, the differential is calculated by subtracting the par from the score.

For example:

```text
Score: 42
Par:   36
```

The differential is:

```text
42 - 36 = 6
```

This calculation must be performed for every round.

After all differentials have been calculated, the function returns their average rounded to one decimal place.

For example:

```python
scores = [42, 45, 46, 44]
pars = [36, 36, 36, 36]
```

The differentials are:

```text
42 - 36 = 6
45 - 36 = 9
46 - 36 = 10
44 - 36 = 8
```

So the list of differentials is:

```python
[6, 9, 10, 8]
```

Their average is:

```text
(6 + 9 + 10 + 8) / 4
= 33 / 4
= 8.25
```

Rounded to one decimal place, the expected result is:

```text
8.3
```

## My Approach

First, I added input validation.

The first check makes sure that `scores` and `pars` contain the same number of elements:

```python
if len(scores) != len(pars):
    raise ValueError("scores and pars must have the same length")
```

This is important because every score needs a corresponding par value.

For example, if there were four scores but only three par values, the final score could not be matched with a par value.

I used `raise ValueError()` to stop the function when the provided input cannot be used correctly.

Next, I checked whether either list is empty:

```python
if not scores or not pars:
    raise ValueError("scores and pars cannot be empty")
```

This is necessary because calculating an average requires at least one value.

If there were no differentials, dividing by the number of differentials would mean dividing by zero.

## Calculating the Differentials

After validating the input, I created an empty list called `differentials`:

```python
differentials = []
```

This list stores the differential from every round.

Next, I used a `for` loop together with `range()` and `len()`:

```python
for score in range(len(scores)):
```

`len(scores)` returns the number of elements in the `scores` list.

`range(len(scores))` then creates the indexes needed to access each score.

For example, if there are four scores, the indexes are:

```text
0
1
2
3
```

During every loop iteration, I use the same index for both lists:

```python
scores[score]
pars[score]
```

This ensures that the correct score is matched with the correct par value.

The differential is then calculated with:

```python
differential = scores[score] - pars[score]
```

Each differential is added to the list using `.append()`:

```python
differentials.append(differential)
```

After the loop, the list might look like this:

```python
[6, 9, 10, 8]
```

## Calculating the Average

Next, I calculate the average of all differentials.

`sum()` adds all values:

```python
sum(differentials)
```

and `len()` gives the number of differentials:

```python
len(differentials)
```

The average is therefore calculated by dividing the total by the number of values.

Initially, I used Python's built-in `round()` function.

However, I discovered an important detail about Python's rounding behavior.

For example:

```text
8.25
```

rounded to one decimal place with Python's normal `round()` can become:

```text
8.2
```

instead of:

```text
8.3
```

This happens because Python uses a rounding method commonly known as **banker's rounding**, or **round half to even**.

The challenge, however, expects traditional rounding where:

```text
8.25 → 8.3
```

Because of this, I used Python's `decimal` module.

## Using Decimal and ROUND_HALF_UP

First, I imported:

```python
from decimal import Decimal, ROUND_HALF_UP
```

`Decimal` allows decimal numbers to be handled more precisely than normal floating-point numbers in situations where exact decimal rounding matters.

I calculated the average using `Decimal` values:

```python
average = Decimal(sum(differentials)) / Decimal(len(differentials))
```

An important detail is that I convert the values to `Decimal` **before performing the division**.

This avoids first creating a normal floating-point result and only converting it afterwards.

Next, I used the `.quantize()` method:

```python
handicap = average.quantize(
    Decimal("0.1"),
    rounding=ROUND_HALF_UP
)
```

`Decimal("0.1")` tells Python that the result should have one decimal place.

`ROUND_HALF_UP` defines the rounding rule.

With this rounding mode:

```text
8.24 → 8.2
8.25 → 8.3
8.26 → 8.3
```

Finally, I converted the result back into a normal floating-point number:

```python
return float(handicap)
```

## My Solution

```python
from decimal import Decimal, ROUND_HALF_UP


def calculate_handicap(scores, pars):

    if len(scores) != len(pars):
        raise ValueError("scores and pars must have the same length")

    if not scores or not pars:
        raise ValueError("scores and pars cannot be empty")

    differentials = []

    for score in range(len(scores)):
        differential = scores[score] - pars[score]
        differentials.append(differential)

    average = Decimal(sum(differentials)) / Decimal(len(differentials))

    handicap = average.quantize(
        Decimal("0.1"),
        rounding=ROUND_HALF_UP
    )

    return float(handicap)
```

## What I Learned

During this challenge, I practiced working with:

* Python lists
* `for` loops
* `range()`
* `len()`
* list indexes
* accessing corresponding values from two lists
* `.append()`
* `sum()`
* calculating averages
* input validation
* `if` statements
* the `or` operator
* `raise`
* `ValueError`
* Python's rounding behavior
* the `decimal` module
* `Decimal`
* `.quantize()`
* `ROUND_HALF_UP`
* converting values with `float()`

One important thing I learned was how to work with two related lists at the same time.

Because `scores` and `pars` contain corresponding values, I can use the same index to access matching elements from both lists.

For example:

```python
scores[score]
pars[score]
```

Both expressions access the element at the same position.

I also learned how `range()` and `len()` can work together.

Using:

```python
range(len(scores))
```

allows me to iterate over the indexes of the list instead of directly over its values.

This is useful when the same index is needed for more than one list.

Another important concept was calculating an average.

The general idea is:

```text
sum of all values / number of values
```

In this challenge, that means adding all differentials and dividing the result by the number of rounds.

I also learned more about input validation.

By checking whether the two lists have different lengths, I can prevent mismatched data from being processed.

By checking whether a list is empty, I can prevent a division-by-zero error later in the function.

One of the most interesting things I learned was that Python's built-in `round()` does not always behave the way I initially expected.

The value:

```text
8.25
```

can become:

```text
8.2
```

when rounded to one decimal place with `round()`.

The challenge expected:

```text
8.3
```

so I learned how to use `Decimal`, `.quantize()`, and `ROUND_HALF_UP` to explicitly control the rounding rule.

I also learned why it is better to convert values to `Decimal` before performing the division rather than converting the already calculated floating-point result afterwards.

Finally, I learned again how important indentation is in Python.

The calculation of the final handicap and the `return` statement must be outside the `for` loop.

If `return` were inside the loop, the function would stop after calculating only the first differential.

Overall, this challenge helped me improve my understanding of lists, indexes, loops, averages, validation, exceptions, decimal arithmetic, and rounding behavior in Python.


