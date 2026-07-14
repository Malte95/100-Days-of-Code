# Today I Completed the Following Python Programming Task

## Pet Years

## The Goal

Develop a Python function called `pet_years(pet, age)` that receives a pet type and its age in human years.

The function should return the equivalent age in pet years.

Each pet type has a different age multiplier:

| Pet            | Multiplier |
| -------------- | ---------: |
| `"dog"`        |          7 |
| `"cat"`        |          6 |
| `"rabbit"`     |          8 |
| `"hamster"`    |         30 |
| `"guinea pig"` |         12 |
| `"goldfish"`   |          6 |
| `"bird"`       |          5 |

To calculate the age in pet years, the human age must be multiplied by the corresponding multiplier.

The general calculation is:

```text
pet age = human age × multiplier
```

For example, one human year for a dog is equivalent to seven dog years:

```text
1 × 7 = 7
```

Therefore:

```python
pet_years("dog", 1)
# 7
```

## The Tests

The function should correctly handle examples such as:

```python
pet_years("dog", 3)
# 21
```

The multiplier for a dog is:

```text
7
```

Therefore:

```text
3 × 7 = 21
```

Another example:

```python
pet_years("cat", 4)
# 24
```

The multiplier for a cat is:

```text
6
```

Therefore:

```text
4 × 6 = 24
```

For a hamster:

```python
pet_years("hamster", 2)
# 60
```

The calculation is:

```text
2 × 30 = 60
```

For a guinea pig:

```python
pet_years("guinea pig", 5)
# 60
```

The calculation is:

```text
5 × 12 = 60
```

The function can also process decimal ages:

```python
pet_years("rabbit", 1.5)
# 12.0
```

The calculation is:

```text
1.5 × 8 = 12.0
```

The function should also reject invalid pet types.

For example:

```python
pet_years("horse", 3)
```

This should raise an error because `"horse"` is not included in the conversion table:

```text
ValueError: Unknown pet type: horse
```

Negative ages should also be rejected:

```python
pet_years("dog", -2)
```

This should raise:

```text
ValueError: Age cannot be negative
```

## My Approach

### 1. Created a Dictionary for the Multipliers

I created a dictionary called `multipliers`.

```python
multipliers = {
    "dog": 7,
    "cat": 6,
    "rabbit": 8,
    "hamster": 30,
    "guinea pig": 12,
    "goldfish": 6,
    "bird": 5,
}
```

A dictionary stores information as key-value pairs.

In this dictionary, each pet type is a key and its multiplier is the corresponding value.

For example:

```text
"dog" → 7
"cat" → 6
"rabbit" → 8
```

The key `"dog"` is connected to the value `7`.

The key `"hamster"` is connected to the value `30`.

This makes it possible to retrieve the correct multiplier by using the pet type.

For example:

```python
multipliers["dog"]
# 7
```

```python
multipliers["hamster"]
# 30
```

Using a dictionary makes the function shorter and easier to understand than using a long chain of `if` and `elif` statements.

An alternative solution could look like this:

```python
if pet == "dog":
    return age * 7
elif pet == "cat":
    return age * 6
elif pet == "rabbit":
    return age * 8
```

However, this approach becomes longer every time another pet type is added.

With a dictionary, a new pet can be added using only one additional key-value pair.

For example:

```python
"turtle": 4
```

### 2. Checked Whether the Pet Type Exists

Before accessing the multiplier, I checked whether the supplied pet type exists in the dictionary.

```python
if pet not in multipliers:
```

The `in` operator checks whether a key exists in a dictionary.

For example:

```python
"dog" in multipliers
# True
```

```python
"horse" in multipliers
# False
```

The `not in` operator checks the opposite.

```python
"horse" not in multipliers
# True
```

Therefore, this condition becomes `True` when the function receives an unknown pet type.

```python
if pet not in multipliers:
```

### 3. Raised an Error for an Unknown Pet Type

When the pet type does not exist in the dictionary, I raise a `ValueError`.

```python
raise ValueError(f"Unknown pet type: {pet}")
```

A `ValueError` indicates that the function received a value that it cannot process.

The error message uses an f-string:

```python
f"Unknown pet type: {pet}"
```

The value of `pet` is inserted directly into the message.

For example, when the function receives:

```python
pet_years("horse", 3)
```

the f-string becomes:

```text
Unknown pet type: horse
```

The complete error is:

```text
ValueError: Unknown pet type: horse
```

This is more helpful than allowing Python to produce an unclear error later in the function.

It also makes the expected input requirements easier to understand.

### 4. Checked Whether the Age Is Negative

A pet cannot have a negative age.

Therefore, I added another validation condition:

```python
if age < 0:
```

This condition checks whether the provided age is less than zero.

For example:

```text
3 < 0
```

is:

```text
False
```

However:

```text
-2 < 0
```

is:

```text
True
```

If the condition is `True`, the input is invalid.

### 5. Raised an Error for a Negative Age

When the age is negative, I raise another `ValueError`.

```python
raise ValueError("Age cannot be negative")
```

For example:

```python
pet_years("cat", -4)
```

raises:

```text
ValueError: Age cannot be negative
```

This prevents the function from returning an unrealistic negative pet age.

Without this validation, the calculation would be:

```text
-4 × 6 = -24
```

The function would return:

```python
-24
```

However, a negative pet age does not make sense, so rejecting the input is the better solution.

### 6. Retrieved the Correct Multiplier

After both validation checks have passed, the pet type is guaranteed to exist in the dictionary.

I can therefore access the multiplier with:

```python
multipliers[pet]
```

For example, when:

```text
pet = "dog"
```

this expression becomes:

```python
multipliers["dog"]
```

The result is:

```python
7
```

When:

```text
pet = "bird"
```

the expression becomes:

```python
multipliers["bird"]
```

The result is:

```python
5
```

### 7. Multiplied the Age by the Multiplier

The equivalent age in pet years is calculated by multiplying the human age by the correct multiplier.

```python
age * multipliers[pet]
```

For example, when the arguments are:

```python
pet_years("rabbit", 3)
```

the values are:

```text
pet = "rabbit"
age = 3
```

The multiplier is retrieved:

```python
multipliers["rabbit"]
# 8
```

The calculation becomes:

```text
3 × 8 = 24
```

### 8. Returned the Result

Finally, I returned the calculated pet age.

```python
return age * multipliers[pet]
```

The `return` statement sends the result back to the code that called the function.

For example:

```python
result = pet_years("bird", 4)
```

The calculation is:

```text
4 × 5 = 20
```

Therefore, the value stored in `result` is:

```python
20
```

## The Final Function

```python
def pet_years(pet, age):
    multipliers = {
        "dog": 7,
        "cat": 6,
        "rabbit": 8,
        "hamster": 30,
        "guinea pig": 12,
        "goldfish": 6,
        "bird": 5,
    }

    if pet not in multipliers:
        raise ValueError(f"Unknown pet type: {pet}")

    if age < 0:
        raise ValueError("Age cannot be negative")

    return age * multipliers[pet]
```

## How the Function Processes a Dog Aged Three Years

The function is called with:

```python
pet_years("dog", 3)
```

The arguments are assigned to the function parameters:

```text
pet = "dog"
age = 3
```

The function creates the dictionary containing all pet multipliers.

```python
multipliers = {
    "dog": 7,
    "cat": 6,
    "rabbit": 8,
    "hamster": 30,
    "guinea pig": 12,
    "goldfish": 6,
    "bird": 5,
}
```

The first validation checks whether `"dog"` exists in the dictionary:

```python
if pet not in multipliers:
```

This becomes:

```python
if "dog" not in multipliers:
```

Because `"dog"` is a valid dictionary key, the condition is:

```text
False
```

No error is raised.

The second validation checks whether the age is negative:

```python
if age < 0:
```

This becomes:

```python
if 3 < 0:
```

The condition is:

```text
False
```

Again, no error is raised.

The function retrieves the dog's multiplier:

```python
multipliers["dog"]
```

The result is:

```text
7
```

It then performs the calculation:

```text
3 × 7 = 21
```

The function returns:

```python
21
```

## How the Function Processes a Hamster Aged Two Years

The function is called with:

```python
pet_years("hamster", 2)
```

The arguments are:

```text
pet = "hamster"
age = 2
```

The pet type exists in the dictionary:

```python
"hamster" in multipliers
# True
```

The age is not negative:

```python
2 < 0
# False
```

The hamster multiplier is retrieved:

```python
multipliers["hamster"]
# 30
```

The age is multiplied by the multiplier:

```text
2 × 30 = 60
```

The function returns:

```python
60
```

## How the Function Handles an Unknown Pet

The function is called with:

```python
pet_years("horse", 3)
```

The arguments are:

```text
pet = "horse"
age = 3
```

The first condition checks whether `"horse"` exists in the dictionary:

```python
if "horse" not in multipliers:
```

Because `"horse"` is not a dictionary key, the condition is:

```text
True
```

The function immediately raises an error:

```python
raise ValueError(f"Unknown pet type: {pet}")
```

The resulting message is:

```text
ValueError: Unknown pet type: horse
```

Because an error is raised, the function stops at this point.

The age is not multiplied and no result is returned.

## How the Function Handles a Negative Age

The function is called with:

```python
pet_years("cat", -2)
```

The pet type `"cat"` exists in the dictionary, so the first validation passes.

The second condition checks:

```python
if -2 < 0:
```

This condition is:

```text
True
```

The function raises:

```text
ValueError: Age cannot be negative
```

The multiplication is not performed.

## Additional Tests

The function can be tested using `assert` statements:

```python
assert pet_years("dog", 3) == 21
assert pet_years("cat", 4) == 24
assert pet_years("rabbit", 2) == 16
assert pet_years("hamster", 2) == 60
assert pet_years("guinea pig", 5) == 60
assert pet_years("goldfish", 3) == 18
assert pet_years("bird", 4) == 20
```

Decimal ages can also be tested:

```python
assert pet_years("rabbit", 1.5) == 12.0
```

An age of zero is valid:

```python
assert pet_years("dog", 0) == 0
```

The validation errors can be tested with `try` and `except`:

```python
try:
    pet_years("horse", 3)
except ValueError as error:
    print(error)
```

The output is:

```text
Unknown pet type: horse
```

The negative age validation can be tested in the same way:

```python
try:
    pet_years("dog", -2)
except ValueError as error:
    print(error)
```

The output is:

```text
Age cannot be negative
```

## Why This Solution Works

The function stores every pet type and its corresponding multiplier in a dictionary.

The pet type received by the function is used as the dictionary key.

This allows the function to retrieve the correct multiplier directly without using many separate `if` and `elif` conditions.

Before performing the calculation, the function validates both arguments.

It first checks whether the supplied pet type exists in the dictionary.

If the pet type is unknown, the function raises a `ValueError` with a clear error message.

It then checks whether the age is negative.

If the age is less than zero, another `ValueError` is raised.

When both inputs are valid, the function multiplies the human age by the multiplier stored for the selected pet.

The general process is:

1. Create a dictionary containing the pet multipliers.
2. Check whether the pet type exists in the dictionary.
3. Raise an error when the pet type is unknown.
4. Check whether the age is negative.
5. Raise an error when the age is invalid.
6. Retrieve the correct multiplier from the dictionary.
7. Multiply the human age by the multiplier.
8. Return the equivalent age in pet years.

This challenge helped me understand how dictionaries store key-value pairs, how to retrieve values using dictionary keys, and how dictionaries can replace long chains of `if` and `elif` statements.

It also helped me practise input validation and learn how to raise clear errors with `ValueError`.

By adding validation, the function does not only calculate the correct result for valid inputs. It also handles invalid inputs in a predictable and understandable way.

