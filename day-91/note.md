# Daily Coding Challenge: Piggy Bank

Today, I completed a Python coding challenge about calculating the total value of coins in a piggy bank.

## The Challenge

The function receives a dictionary representing the coins inside a piggy bank.

The dictionary may contain any of the following coin types:

| Coin     | Value |
| -------- | ----: |
| pennies  | $0.01 |
| nickels  | $0.05 |
| dimes    | $0.10 |
| quarters | $0.25 |

Each dictionary key represents a type of coin, while its value represents the number of coins of that type.

For example:

```python
{
    "pennies": 3,
    "nickels": 5,
    "dimes": 2,
    "quarters": 6
}
```

The function must calculate the total value and return it as a string in the format `"$D.CC"`.

For this example, the result is:

```text
$1.98
```

The function also needs to handle special cases:

* Some coin types may be missing from the dictionary.
* A coin amount may be zero.
* The dictionary may be empty.
* The result must always contain exactly two decimal places.

## My Approach

First, I created a dictionary called `coin_values`.

This dictionary stores the monetary value of each coin:

```python
coin_values = {
    "pennies": 0.01,
    "nickels": 0.05,
    "dimes": 0.10,
    "quarters": 0.25
}
```

Then, I created a variable called `total_value` and set it to zero.

Next, I used a `for` loop with the `.items()` method to access each coin type and its amount:

```python
for coin, amount in coins.items():
```

The `.items()` method returns the key and value of each dictionary entry.

For example, an entry such as:

```python
"pennies": 3
```

provides:

```python
coin = "pennies"
amount = 3
```

During each loop iteration, I accessed the value of the current coin from the `coin_values` dictionary and multiplied it by the amount:

```python
coin_values[coin] * amount
```

I then added the result to `total_value` using `+=`.

Finally, I used an f-string to add the dollar sign and format the result with exactly two decimal places:

```python
f"${total_value:.2f}"
```

## My Solution

```python
def piggy_bank(coins):
    coin_values = {
        "pennies": 0.01,
        "nickels": 0.05,
        "dimes": 0.10,
        "quarters": 0.25
    }

    total_value = 0

    for coin, amount in coins.items():
        total_value += coin_values[coin] * amount

    return f"${total_value:.2f}"
```

## What I Learned

During this challenge, I practiced working with:

* Python dictionaries
* dictionary keys and values
* the `.items()` method
* `for` loops
* accessing dictionary values with square brackets
* multiplication and addition
* the `+=` operator
* f-strings
* formatting decimal numbers
* handling empty dictionaries

The biggest challenge was understanding how Python knows what `coin` and `amount` represent inside the loop.

I learned that `.items()` returns each dictionary entry as a key-value pair. Python assigns the key to `coin` and the corresponding value to `amount`.

For example:

```python
"quarters": 6
```

becomes:

```python
coin = "quarters"
amount = 6
```

I also learned that using:

```python
total_value = coin_values[coin] * amount
```

would replace the previous total during every loop iteration.

Instead, I needed to use:

```python
total_value += coin_values[coin] * amount
```

This adds each calculated coin value to the existing total.

Another important part was formatting the result. Without formatting, Python might return values such as `2.0` instead of `"$2.00"`.

Using `:.2f` ensures that the result always contains exactly two decimal places.

Overall, this was a useful exercise for improving my understanding of dictionaries, loops, key-value pairs, arithmetic operations, accumulation, and string formatting in Python.
