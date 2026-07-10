# Today I Completed the Following Python Programming Task

## Exact Change

### The Goal

Develop a Python function called `exact_change(amount)` that returns the number of distinct ways to make exact change for a given amount in cents.

The available coins are:

* pennies: 1 cent
* nickels: 5 cents
* dimes: 10 cents
* quarters: 25 cents

The function receives:

* an integer amount in cents

The function should return:

* the number of different coin combinations that add up exactly to the given amount

The order of the coins does not matter.

For example, for 9 cents, the possible combinations are:

* 9 pennies
* 1 nickel and 4 pennies

Therefore:

```python
exact_change(9)
```

returns:

```python
2
```

## The Tests

The function needs to pass the following tests:

```python
exact_change(3)
# 1

exact_change(9)
# 2

exact_change(17)
# 6

exact_change(39)
# 24

exact_change(61)
# 73

exact_change(99)
# 213
```

All six tests passed.

## My Approach

### 1. Defined the Coin Values

First, I created variables for the four available coin values.

```python
p = 1
n = 5
d = 10
q = 25
```

These variables represent:

* `p` for pennies
* `n` for nickels
* `d` for dimes
* `q` for quarters

This makes the purpose of each coin value easier to understand.

### 2. Created a Counter for the Possible Combinations

I created a variable called `possibilities`.

```python
possibilities = 0
```

This variable keeps track of how many valid coin combinations have been found.

Every time the program finds a valid combination of quarters, dimes, nickels, and pennies, the counter is increased by one.

### 3. Checked Every Possible Number of Quarters

The first loop goes through every possible number of quarters.

```python
for amount_quarters in range(amount // 25 + 1):
```

The expression:

```python
amount // 25
```

calculates the maximum number of quarters that can fit into the given amount.

For example, if the amount is 61 cents:

```python
61 // 25
```

returns:

```python
2
```

This means that the possible numbers of quarters are:

* 0 quarters
* 1 quarter
* 2 quarters

The `+ 1` is necessary because the ending value of `range()` is not included.

### 4. Calculated the Remaining Amount After Quarters

For every possible number of quarters, I calculated how much money was still left.

```python
rest_after_quarters = amount - amount_quarters * 25
```

For example, with an amount of 61 cents:

* 0 quarters leaves 61 cents
* 1 quarter leaves 36 cents
* 2 quarters leaves 11 cents

The next loop only needs to work with the remaining amount.

### 5. Checked Every Possible Number of Dimes

Inside the quarter loop, I added another loop for the possible number of dimes.

```python
for amount_dimes in range(rest_after_quarters // 10 + 1):
```

The maximum number of dimes depends on the amount remaining after the quarters have been removed.

For example, if 36 cents remain:

```python
36 // 10
```

returns:

```python
3
```

Therefore, the program checks:

* 0 dimes
* 1 dime
* 2 dimes
* 3 dimes

### 6. Calculated the Remaining Amount After Dimes

For every possible number of dimes, I calculated the new remaining amount.

```python
rest_after_dimes = rest_after_quarters - amount_dimes * 10
```

For example, if 36 cents remain after choosing the quarters:

* 0 dimes leaves 36 cents
* 1 dime leaves 26 cents
* 2 dimes leaves 16 cents
* 3 dimes leaves 6 cents

The nickel loop then works with this remaining amount.

### 7. Checked Every Possible Number of Nickels

Inside the dime loop, I added a third loop for the possible number of nickels.

```python
for amount_nickels in range(rest_after_dimes // 5 + 1):
```

This loop checks how many nickels can fit into the remaining amount.

For example, if 16 cents remain:

```python
16 // 5
```

returns:

```python
3
```

The possible numbers of nickels are therefore:

* 0 nickels
* 1 nickel
* 2 nickels
* 3 nickels

### 8. Used Pennies to Complete Every Combination

There is no separate loop for pennies.

This is because pennies are worth 1 cent, so every remaining non-negative amount can always be completed with pennies.

For example:

* a remaining amount of 4 cents can be completed with 4 pennies
* a remaining amount of 7 cents can be completed with 7 pennies
* a remaining amount of 0 cents needs no pennies

Therefore, every combination of quarters, dimes, and nickels automatically creates exactly one valid combination when the remaining amount is filled with pennies.

That is why the counter is increased inside the nickel loop.

```python
possibilities += 1
```

### 9. Returned the Total Number of Possibilities

After all possible combinations have been checked, the function returns the counter.

```python
return possibilities
```

This gives the total number of distinct ways to make exact change.

## Example With 17 Cents

For 17 cents, no quarters can be used.

The function checks the possible number of dimes.

### 0 Dimes

17 cents remain.

Possible nickels:

* 0 nickels and 17 pennies
* 1 nickel and 12 pennies
* 2 nickels and 7 pennies
* 3 nickels and 2 pennies

This gives 4 combinations.

### 1 Dime

7 cents remain.

Possible nickels:

* 0 nickels and 7 pennies
* 1 nickel and 2 pennies

This gives 2 more combinations.

The total is:

```python
4 + 2 = 6
```

Therefore:

```python
exact_change(17)
```

returns:

```python
6
```

## The Final Function

```python
def exact_change(amount):
    p = 1
    n = 5
    d = 10
    q = 25

    possibilities = 0

    for amount_quarters in range(amount // 25 + 1):
        rest_after_quarters = amount - amount_quarters * 25

        for amount_dimes in range(rest_after_quarters // 10 + 1):
            rest_after_dimes = rest_after_quarters - amount_dimes * 10

            for amount_nickels in range(rest_after_dimes // 5 + 1):
                possibilities += 1

    return possibilities
```

## Why This Solution Works

The function systematically checks every possible number of quarters, dimes, and nickels.

For each number of quarters, it calculates the remaining amount.

For each number of dimes, it calculates the next remaining amount.

It then checks every possible number of nickels that can fit into that amount.

Any amount left over can always be completed using pennies because pennies are worth 1 cent.

The general process is:

1. Choose a possible number of quarters.
2. Calculate the remaining amount.
3. Choose a possible number of dimes.
4. Calculate the new remaining amount.
5. Choose a possible number of nickels.
6. Fill the remaining amount with pennies.
7. Count the combination as one possibility.

The loops are nested so that every unique combination is counted exactly once.

This allows the function to correctly calculate the number of distinct ways to make exact change for all tested amounts.

