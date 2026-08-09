# Daily Coding Challenge: Golf Handicap Calculator

Today, I completed a Python coding challenge about calculating a golfer's handicap index based on multiple golf scores and their corresponding par values.

## The Challenge

The function receives two arrays:

* one array containing the golfer's scores
* one array containing the corresponding par values for each round

For every round, the function must calculate the **differential** by subtracting the par value from the golfer's score.

For example:

```text
Score: 78
Par:   72
```

The differential is:

```text
78 - 72 = 6
```

This calculation needs to be performed for every round.

After calculating all differentials, the function must calculate their average and round the result to one decimal place.

For example, if the differentials are:

```python
[6, 4, 8]
```

their average is:

```text
(6 + 4 + 8) / 3 = 6.0
```

The function should therefore return:

```text
6.0
```

## My Approach

First, I added two checks to make sure the provided data can be used correctly.

The first check verifies that `scores` and `pars` contain the same number of elements:

```python
if len(scores) != len(pars):
    raise ValueError("scores and pars must have the same length")
```

This is important because every golf score needs a corresponding par value.

For example, if there are three scores but only two par values, the program would not know which par belongs to the third score.

I used `raise ValueError()` to stop the function when the provided values are not suitable for the calculation.

Next, I checked whether either of the lists is empty:

```python
if not scores or not pars:
    raise ValueError("scores and pars cannot be empty")
```

This prevents the function from trying to calculate an average when there are no rounds available.

An empty list would also cause a problem later because calculating the average would require dividing by the number of differentials. If there are no differentials, that number would be zero.

After validating the input, I created an empty list called `differentials`:

```python
differentials = []
```

This list is used to store the calculated differential for every golf round.

Next, I used a `for` loop together with `range()` and `len()`:

```python
for score in range(len(scores)):
```

`len(scores)` returns the number of elements inside the `scores` list.

`range(len(scores))` then creates the indexes needed to access each element.

For example, if there are three scores, the indexes are:

```text
0
1
2
```

During each loop iteration, I use the current index to access both the score and its corresponding par value.

The differential is calculated by subtracting the par from the score:

```python
differential = scores[score] - pars[score]
```

Because both lists use the same index, the correct score and par value are matched together.

For example:

```python
scores = [78, 75, 80]
pars   = [72, 72, 72]
```

The loop calculates:

```text
78 - 72 = 6
75 - 72 = 3
80 - 72 = 8
```

Each differential is then added to the `differentials` list using `.append()`:

```python
differentials.append(differential)
```

After the loop finishes, the list would look like this:

```python
[6, 3, 8]
```

Next, I calculated the average of all differentials.

I used `sum()` to add all values inside the list:

```python
sum(differentials)
```

Then I used `len()` to determine how many differentials there are:

```python
len(differentials)
```

Dividing the sum by the number of values gives the average.

Finally, I used `round()` with `1` as the second argument to round the result to one decimal place:

```python
round(sum(differentials) / len(differentials), 1)
```

The result is stored in the variable `handicap` and returned by the function.

## My Solution

```python
def calculate_handicap(scores, pars):

    if len(scores) != len(pars):
        raise ValueError("scores and pars must have the same length")

    if not scores or not pars:
        raise ValueError("scores and pars cannot be empty")

    differentials = []

    for score in range(len(scores)):
        differential = scores[score] - pars[score]
        differentials.append(differential)

    handicap = round(sum(differentials) / len(differentials), 1)

    return handicap
```

## What I Learned

During this challenge, I practiced working with:

* Python lists
* `for` loops
* `range()`
* `len()`
* list indexes
* accessing corresponding elements from multiple lists
* the `.append()` method
* the `sum()` function
* calculating averages
* the `round()` function
* `if` statements
* the `or` operator
* `raise`
* `ValueError`
* input validation

One important thing I learned was how to work with two related lists at the same time.

Because `scores` and `pars` contain corresponding values, I can use the same index to access elements from both lists.

For example:

```python
scores[score]
pars[score]
```

Both expressions access values at the same position in their respective lists.

I also learned more about how `range()` and `len()` can work together.

Instead of iterating directly over the values in a list, I can use:

```python
range(len(scores))
```

to iterate over the indexes of the list.

This is useful when I need the same index to access values from multiple lists.

Another important concept was calculating an average.

First, I use:

```python
sum(differentials)
```

to calculate the total of all differentials.

Then:

```python
len(differentials)
```

gives me the number of values.

Dividing these two values gives the average differential.

I also practiced using `round()`:

```python
round(value, 1)
```

The second argument tells Python how many decimal places the result should have. In this challenge, the handicap needs to be rounded to one decimal place.

Another new concept was validating the input before performing the actual calculation.

By checking:

```python
len(scores) != len(pars)
```

I can detect when the two lists do not contain the same number of elements.

I also learned that:

```python
not scores
```

can be used to check whether a list is empty.

Using `raise ValueError()` allows the function to stop immediately when invalid data is provided instead of continuing with a calculation that would fail or produce an incorrect result.

I also learned something important about indentation and `return`.

The handicap calculation and `return` statement need to be outside the `for` loop.

If `return` were inside the loop, the function would stop after processing only the first golf round. By placing it after the loop, Python first calculates every differential before calculating and returning the final handicap.

Overall, this challenge helped me improve my understanding of lists, indexes, loops, averages, rounding, input validation, exceptions, and the importance of correctly structuring a Python function.

