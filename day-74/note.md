# Today I Completed the Following Python Programming Task

## Birthday Countdown

## The Goal

Develop a Python function called `days_until_birthday(today, birthday)` that calculates the number of days until a person's next birthday.

The parameter `today` is provided as a string in the following format:

```text
"YYYY-MM-DD"
```

For example:

```python
"2026-07-16"
```

The parameter `birthday` is provided as a string containing the month and day:

```text
"M/D"
```

For example:

```python
"9/7"
```

The function must return the number of days between today's date and the person's next birthday.

If today is the person's birthday, the function must calculate the number of days until the birthday in a future year instead of returning `0`.

Leap years must also be handled correctly.

## The Tests

The function should correctly handle examples such as:

```python
days_until_birthday("2026-07-16", "9/7")
# 53
```

```python
days_until_birthday("2026-07-16", "3/22")
# 249
```

```python
days_until_birthday("2026-07-16", "7/16")
# 365
```

```python
days_until_birthday("2024-02-28", "3/1")
# 2
```

```python
days_until_birthday("2023-04-24", "12/30")
# 250
```

The function must also work with birthdays on February 29.

For example:

```python
days_until_birthday("2024-03-01", "2/29")
```

The next valid birthday would be:

```text
2028-02-29
```

## My Approach

### 1. Imported the `date` Class

I imported the `date` class from Python's `datetime` module.

```python
from datetime import date
```

The `date` class allows Python to work with actual calendar dates.

This is useful because the original values are strings, and strings cannot be directly subtracted from each other.

For example, Python cannot calculate this:

```python
"2026-09-07" - "2026-07-16"
```

However, Python can subtract two `date` objects.

### 2. Converted Today's Date

The `today` parameter is provided in ISO format:

```text
"YYYY-MM-DD"
```

Because this is already the format expected by `date.fromisoformat()`, I used it to convert the string into a date object.

```python
today_date = date.fromisoformat(today)
```

For example:

```python
today = "2026-07-16"
```

becomes equivalent to:

```python
date(2026, 7, 16)
```

After this conversion, Python can use the value in date calculations.

### 3. Separated the Birthday Month and Day

The birthday is provided as a string such as:

```python
"9/7"
```

I used `.split("/")` to separate the month and day.

```python
month, day = birthday.split("/")
```

This produces:

```python
month = "9"
day = "7"
```

At this point, both values are still strings.

### 4. Converted the Month and Day into Integers

The `date()` constructor requires numbers instead of strings.

Therefore, I converted both values using `int()`.

```python
month = int(month)
day = int(day)
```

The values are now:

```python
month = 9
day = 7
```

They can now be used to create a complete date.

### 5. Started with the Current Year

The birthday string only contains a month and day, so the year is missing.

I first used the year from today's date.

```python
year = today_date.year
```

For example, if today's date is:

```python
date(2026, 7, 16)
```

then:

```python
year = 2026
```

The first birthday date the function attempts to create is therefore the birthday in the current year.

### 6. Used a Loop to Search for the Next Birthday

I used a `while True` loop because the function may need to check multiple years.

```python
while True:
```

For most birthdays, the function only needs to check the current year or the following year.

However, a birthday on February 29 may require checking several years before a valid date is found.

For example:

```text
2025-02-29 → invalid
2026-02-29 → invalid
2027-02-29 → invalid
2028-02-29 → valid
```

Because the exact number of attempts is not always known in advance, a `while` loop is useful here.

### 7. Tried to Create a Complete Birthday Date

Inside the loop, I attempted to create the birthday using the current values of `year`, `month`, and `day`.

```python
birthday_date = date(year, month, day)
```

For example:

```python
year = 2026
month = 9
day = 7
```

produces:

```python
date(2026, 9, 7)
```

This represents the person's birthday in 2026.

### 8. Checked Whether the Birthday Is in the Future

After creating the date, I checked whether it occurs after today's date.

```python
if birthday_date > today_date:
    break
```

The `>` comparison is important.

It means the birthday must be strictly later than today.

If today is the person's birthday, the two dates are equal:

```python
birthday_date == today_date
```

In that case, the loop does not stop. Instead, the function searches for the birthday in a future year.

For example:

```text
Today:      2026-07-16
Birthday:   2026-07-16
```

The next birthday should be:

```text
2027-07-16
```

not the current date.

### 9. Increased the Year When the Date Was Not in the Future

If the birthday date was today or had already passed, I increased the year by one.

```python
else:
    year += 1
```

For example:

```text
Today:              2026-10-12
Birthday this year: 2026-09-07
```

The birthday in 2026 has already passed, so the function continues with:

```text
2027-09-07
```

The loop then checks the newly selected year.

### 10. Handled Invalid Dates with `try` and `except`

A birthday such as February 29 does not exist every year.

For example, this causes a `ValueError`:

```python
date(2026, 2, 29)
```

To prevent the program from stopping, I placed the date creation inside a `try` block.

```python
try:
    birthday_date = date(year, month, day)
```

If the date is invalid, the `except` block catches the error.

```python
except ValueError:
    year += 1
    continue
```

The year is increased, and `continue` starts the next loop iteration.

For example, if the birthday is February 29, the function may check:

```text
2026-02-29 → invalid
2027-02-29 → invalid
2028-02-29 → valid
```

This allows the function to automatically find the next leap year.

### 11. Stopped the Loop Only When the Date Was Valid and in the Future

The loop only ends when both of the following conditions are true:

1. The birthday date exists.
2. The birthday date occurs after today's date.

The `break` statement is therefore placed inside this condition:

```python
if birthday_date > today_date:
    break
```

This ensures that the function does not stop on:

* an invalid date,
* a birthday that already passed,
* or today's date.

### 12. Calculated the Difference Between the Dates

After the loop ends, `birthday_date` contains the next valid birthday.

I subtracted `today_date` from `birthday_date`.

```python
birthday_date - today_date
```

Subtracting two date objects produces a `timedelta` object.

To retrieve only the number of days, I used its `.days` attribute.

```python
(birthday_date - today_date).days
```

The function then returns this value.

```python
return (birthday_date - today_date).days
```

For example:

```python
date(2026, 9, 7) - date(2026, 7, 16)
```

represents a difference of:

```text
53 days
```

## The Final Function

```python
from datetime import date


def days_until_birthday(today, birthday):
    today_date = date.fromisoformat(today)

    month, day = birthday.split("/")
    month = int(month)
    day = int(day)

    year = today_date.year

    while True:
        try:
            birthday_date = date(year, month, day)

            if birthday_date > today_date:
                break
            else:
                year += 1

        except ValueError:
            year += 1
            continue

    return (birthday_date - today_date).days
```

## A Shorter Version

The same function can also be written slightly more concisely.

The `map()` function can convert the month and day into integers immediately:

```python
month, day = map(int, birthday.split("/"))
```

The `else` block is also unnecessary because the year should be increased whenever the `if` condition is false.

Additionally, `continue` is optional at the end of the `except` block because the loop automatically starts its next iteration after the block finishes.

```python
from datetime import date


def days_until_birthday(today, birthday):
    today_date = date.fromisoformat(today)
    month, day = map(int, birthday.split("/"))

    year = today_date.year

    while True:
        try:
            birthday_date = date(year, month, day)

            if birthday_date > today_date:
                return (birthday_date - today_date).days

            year += 1

        except ValueError:
            year += 1
```

Both versions use the same logic.

## Why This Solution Works

The function first converts the provided strings into values that Python can use for date calculations.

The general process is:

1. Convert today's date from a string into a date object.
2. Separate the birthday into its month and day.
3. Convert the month and day into integers.
4. Begin with the current year.
5. Try to create the birthday in that year.
6. If the date is invalid, move to the next year.
7. If the date is today or already passed, move to the next year.
8. Stop when a valid birthday in the future is found.
9. Subtract today's date from the birthday date.
10. Return the number of days in the resulting difference.

The loop handles normal birthdays, birthdays that already passed, birthdays that occur today, year changes, and birthdays on February 29.

This challenge helped me understand how to convert strings into date objects, compare dates, calculate the difference between dates, use loops when the number of attempts is unknown, and handle invalid values with `try` and `except`.

