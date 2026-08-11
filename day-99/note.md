# Daily Coding Challenge: Spoken Time

Today, I completed a Python coding challenge about converting the angles of the hour and minute hands of an analog clock into a time written in spoken English.

## The Challenge

The function receives two angles:

```text
hour_angle
minute_angle
```

Both angles are measured clockwise from 12 o'clock.

The goal is to convert these angles into hours and minutes and then return the time using spoken English.

The requirements are:

- convert the minute hand angle into minutes
- convert the hour hand angle into the current hour
- handle angles that do not land exactly on a clock number
- return `"Y o'clock"` when the minutes are `0`
- return `"quarter past Y"` when the minutes are `15`
- return `"X minutes past Y"` for minutes between `1` and `29`, excluding `15`
- return `"half past Y"` when the minutes are `30`
- return `"quarter to Z"` when the minutes are `45`
- return `"X minutes to Z"` for minutes between `31` and `59`, excluding `45`
- correctly handle the transition from `12` back to `1`

For example:

```text
hour_angle = 160
minute_angle = 120
```

should return:

```text
20 minutes past 5
```

To solve this challenge, I first needed to understand how the angles of a clock relate to hours and minutes.

## Converting the Minute Angle

A complete circle contains:

```text
360 degrees
```

A clock contains:

```text
60 minutes
```

Therefore, one minute represents:

```text
360 / 60 = 6 degrees
```

This means I can convert the minute hand angle into minutes by dividing the angle by `6`.

For example:

```text
120 / 6 = 20
```

So an angle of `120` degrees represents:

```text
20 minutes
```

However, the challenge also uses angles that do not always land exactly on a minute.

For example:

```text
335 / 6 = 55.833...
```

The expected result is `55` minutes rather than `56`.

Because of this, I used `math.floor()`:

```python
minutes = math.floor(minute_angle / 6)
```

`math.floor()` always rounds a number down to the nearest integer.

For example:

```text
55.833... -> 55
```

This was important because using `round()` caused some of the tests to fail.

## Converting the Hour Angle

A complete clock contains:

```text
12 hours
```

The full circle is:

```text
360 degrees
```

Therefore, each hour represents:

```text
360 / 12 = 30 degrees
```

This means I can calculate the current hour using:

```python
hours = math.floor(hour_angle / 30)
```

For example:

```text
160 / 30 = 5.333...
```

Using `math.floor()` gives:

```text
5
```

So the current hour is:

```text
5
```

This also makes sense for an analog clock because the hour hand moves continuously between the hour numbers.

For example:

```text
67.5 degrees
```

is between:

```text
60 degrees = 2 o'clock
90 degrees = 3 o'clock
```

The calculation is:

```text
67.5 / 30 = 2.25
```

Using `math.floor()` gives:

```text
2
```

So the current hour is still `2`.

## Why I Used `math.floor()`

Originally, I used `round()` for the minute calculation.

For example:

```python
minutes = round(minute_angle / 6)
```

But this caused problems.

For an angle of:

```text
273 degrees
```

the calculation is:

```text
273 / 6 = 45.5
```

Using `round()` would not give the expected result for the challenge.

The expected minute value is:

```text
45
```

Another example is:

```text
335 / 6 = 55.833...
```

The challenge expects:

```text
55
```

because the spoken result should be:

```text
5 minutes to 4
```

Therefore, I changed the calculation to:

```python
minutes = math.floor(minute_angle / 6)
```

I also used `math.floor()` for the hour calculation.

This had another useful effect.

If I used floor division with a floating-point angle:

```python
67.5 // 30
```

Python could produce:

```text
2.0
```

Then the final string could become:

```text
quarter past 2.0
```

instead of:

```text
quarter past 2
```

Using:

```python
math.floor(67.5 / 30)
```

returns the integer:

```text
2
```

which is exactly what I need.

## Handling 12 O'Clock

There is another special case when converting the hour angle.

At:

```text
0 degrees
```

the calculation gives:

```text
0 / 30 = 0
```

But an analog clock does not display hour `0`.

It displays:

```text
12
```

Because of this, I check whether the calculated hour is `0`:

```python
if hours == 0:
    hours += 12
```

This changes:

```text
0
```

into:

```text
12
```

So an angle of `0` degrees correctly represents:

```text
12 o'clock
```

## Keeping the Hour Between 1 and 12

The hour must always stay between:

```text
1 and 12
```

If the hour becomes greater than `12`, I subtract `12`:

```python
if hours > 12:
    hours -= 12
```

For example:

```text
13 - 12 = 1
```

This handles the transition from:

```text
12 -> 1
```

which is necessary on a 12-hour clock.

## Calculating the Next Hour

The challenge uses two different hour values.

`Y` is the current hour.

`Z` is the next hour.

For example:

```text
3:45
```

is spoken as:

```text
quarter to 4
```

The current hour is:

```text
3
```

but the spoken result uses the next hour:

```text
4
```

I calculate the next hour with:

```python
z = hours + 1
```

For example:

```text
hours = 3
z = 4
```

There is also a special case when the current hour is `12`.

Without another check:

```text
12 + 1 = 13
```

But the hour after `12` is:

```text
1
```

Therefore, I use:

```python
if z > 12:
    z -= 12
```

So:

```text
13 - 12 = 1
```

This keeps `z` inside the valid 12-hour clock range.

## Handling Zero Minutes

The first spoken-time rule is:

```text
0 minutes -> "Y o'clock"
```

For example:

```text
hour = 3
minutes = 0
```

should return:

```text
3 o'clock
```

I check this using:

```python
if minutes == 0:
    return f"{hours} o'clock"
```

I use an f-string to insert the current hour into the result.

## Quarter Past

When the minute value is exactly:

```text
15
```

the time should be spoken as:

```text
quarter past Y
```

For example:

```text
2:15
```

becomes:

```text
quarter past 2
```

I check this using:

```python
elif minutes == 15:
    return f"quarter past {hours}"
```

This is checked before the general `1–29` minute case because `15` is a special value.

## Minutes Past the Hour

For minutes between:

```text
1 and 29
```

excluding `15`, the result should be:

```text
X minutes past Y
```

For example:

```text
5:20
```

becomes:

```text
20 minutes past 5
```

Because `0` and `15` are already handled by previous conditions, I can use:

```python
elif minutes <= 29:
    return f"{minutes} minutes past {hours}"
```

For example:

```text
minutes = 20
hours = 5
```

produces:

```text
20 minutes past 5
```

## Half Past

When the minutes are exactly:

```text
30
```

the result should be:

```text
half past Y
```

For example:

```text
8:30
```

becomes:

```text
half past 8
```

I use:

```python
elif minutes == 30:
    return f"half past {hours}"
```

## Quarter To

When the minutes are exactly:

```text
45
```

the result uses the next hour.

For example:

```text
10:45
```

becomes:

```text
quarter to 11
```

Because I already calculated the next hour and stored it in `z`, I can use:

```python
elif minutes == 45:
    return f"quarter to {z}"
```

## Minutes To the Next Hour

For minute values between:

```text
31 and 59
```

excluding `45`, the time is spoken using the number of minutes remaining until the next hour.

For example:

```text
6:40
```

has:

```text
20 minutes
```

remaining until `7`.

To calculate the remaining minutes, I use:

```python
remainder = 60 - minutes
```

For example:

```text
60 - 40 = 20
```

The spoken result is therefore:

```text
20 minutes to 7
```

In the function, this is handled by the final `else`:

```python
else:
    remainder = 60 - minutes
    return f"{remainder} minutes to {z}"
```

Because all the other minute values have already been handled, the remaining values belong to the `"minutes to"` case.

## Using `if`, `elif`, and `else`

The order of the conditions is important.

I check the special values first:

```text
0
15
30
45
```

and use the general ranges around them.

The order is:

```text
0
15
1-29
30
45
31-59
```

The `15` minute case needs to appear before the general `1-29` condition.

Otherwise:

```text
15 <= 29
```

would be true and the function would return:

```text
15 minutes past Y
```

instead of:

```text
quarter past Y
```

The same idea applies to `45`.

It is a special case and should return:

```text
quarter to Z
```

instead of:

```text
15 minutes to Z
```

Using an `if` / `elif` / `else` chain allows only one matching branch to execute.

## Using f-Strings

I used f-strings to insert calculated values into the spoken result.

For example:

```python
f"{minutes} minutes past {hours}"
```

If:

```text
minutes = 20
hours = 5
```

the result becomes:

```text
20 minutes past 5
```

Another example is:

```python
f"quarter to {z}"
```

If:

```text
z = 11
```

the result becomes:

```text
quarter to 11
```

This makes it easy to combine text with variables.

## My Solution

```python
import math

def get_spoken_time(hour_angle, minute_angle):

    minutes = math.floor(minute_angle / 6)
    hours = math.floor(hour_angle / 30)

    if minutes == 60:
        minutes = 0
        hours += 1

    if hours == 0:
        hours += 12

    if hours > 12:
        hours -= 12

    z = hours + 1

    if z > 12:
        z -= 12

    if minutes == 0:
        return f"{hours} o'clock"
    elif minutes == 15:
        return f"quarter past {hours}"
    elif minutes <= 29:
        return f"{minutes} minutes past {hours}"
    elif minutes == 30:
        return f"half past {hours}"
    elif minutes == 45:
        return f"quarter to {z}"
    else:
        remainder = 60 - minutes
        return f"{remainder} minutes to {z}"
```

## Example 1

For:

```python
get_spoken_time(90, 0)
```

the hour is:

```text
90 / 30 = 3
```

and the minutes are:

```text
0 / 6 = 0
```

Because the minute value is `0`, the result is:

```text
3 o'clock
```

## Example 2

For:

```python
get_spoken_time(160, 120)
```

the hour calculation is:

```text
160 / 30 = 5.333...
```

Using `math.floor()` gives:

```text
5
```

The minute calculation is:

```text
120 / 6 = 20
```

Because `20` is between `1` and `29`, the result is:

```text
20 minutes past 5
```

## Example 3

For:

```python
get_spoken_time(255, 180)
```

the hour calculation is:

```text
255 / 30 = 8.5
```

Using `math.floor()` gives:

```text
8
```

The minute calculation is:

```text
180 / 6 = 30
```

Because the minutes are exactly `30`, the result is:

```text
half past 8
```

## Example 4

For:

```python
get_spoken_time(67.5, 92)
```

the hour calculation is:

```text
67.5 / 30 = 2.25
```

Using `math.floor()` gives:

```text
2
```

The minute calculation is:

```text
92 / 6 = 15.333...
```

Using `math.floor()` gives:

```text
15
```

Because the minutes are `15`, the result is:

```text
quarter past 2
```

## Example 5

For:

```python
get_spoken_time(200, 240)
```

the hour calculation is:

```text
200 / 30 = 6.666...
```

Using `math.floor()` gives:

```text
6
```

The minute calculation is:

```text
240 / 6 = 40
```

There are:

```text
60 - 40 = 20
```

minutes remaining until the next hour.

The next hour is:

```text
7
```

So the result is:

```text
20 minutes to 7
```

## Example 6

For:

```python
get_spoken_time(322.5, 273)
```

the hour calculation is:

```text
322.5 / 30 = 10.75
```

Using `math.floor()` gives:

```text
10
```

The minute calculation is:

```text
273 / 6 = 45.5
```

Using `math.floor()` gives:

```text
45
```

The next hour is:

```text
11
```

Because the minutes are `45`, the result is:

```text
quarter to 11
```

## Example 7

For:

```python
get_spoken_time(117.5, 335)
```

the hour calculation is:

```text
117.5 / 30 = 3.916...
```

Using `math.floor()` gives:

```text
3
```

The minute calculation is:

```text
335 / 6 = 55.833...
```

Using `math.floor()` gives:

```text
55
```

The remaining minutes are:

```text
60 - 55 = 5
```

The next hour is:

```text
4
```

So the result is:

```text
5 minutes to 4
```

## What I Learned

During this challenge, I practiced working with:

- converting angles into time values
- understanding that `360` degrees represent a complete clock
- calculating minutes using `6` degrees per minute
- calculating hours using `30` degrees per hour
- using `math.floor()`
- understanding the difference between `round()` and `math.floor()`
- working with floating-point numbers
- handling special clock values such as `12`
- calculating the next hour
- handling the transition from `12` back to `1`
- `if`, `elif`, and `else`
- ordering conditions correctly
- f-strings
- calculating remaining minutes
- separating calculation logic from output formatting
- testing edge cases

One of the most important things I learned was that choosing the correct rounding method matters.

At first, normal rounding seemed like the obvious solution because the hand angles may not land exactly on a number.

However, the tests showed that the expected behavior was to round down.

For example:

```text
335 / 6 = 55.833...
```

Using normal rounding would give:

```text
56
```

but the expected value is:

```text
55
```

Using:

```python
math.floor()
```

solves this problem.

I also learned that the hour hand should represent the current hour section of the clock.

For example:

```text
67.5 degrees
```

is between `2` and `3`.

The calculation gives:

```text
67.5 / 30 = 2.25
```

The current hour is therefore:

```text
2
```

Using `math.floor()` gives exactly this result.

Another important concept was understanding the difference between `"past"` and `"to"`.

For times before or equal to half past the hour, I use the current hour.

For example:

```text
20 minutes past 5
```

uses:

```text
hours = 5
```

For times after half past the hour, I use the next hour.

For example:

```text
20 minutes to 7
```

uses the next hour:

```text
z = 7
```

This is why calculating `z` separately was useful.

I also practiced handling clock boundaries.

The number:

```text
0
```

has to become:

```text
12
```

because an analog clock uses `12` instead of `0`.

Similarly, the hour after:

```text
12
```

must become:

```text
1
```

instead of:

```text
13
```

This taught me how important edge cases are when working with circular values such as clocks.

Another useful lesson was the importance of ordering `if` and `elif` conditions correctly.

Special cases such as:

```text
15
30
45
```

need their own conditions.

For example, `15` is technically also less than `29`, but it should return:

```text
quarter past
```

instead of:

```text
15 minutes past
```

By checking `15` first, I prevent the more general condition from handling it.

Finally, I learned that it is easier to solve a challenge like this by separating it into smaller problems.

First, I converted the angles:

```text
angle -> minutes
angle -> hours
```

Then I handled the clock boundaries:

```text
0 -> 12
12 -> 1
```

After that, I calculated the next hour.

Finally, I handled the different spoken-time formats.

Breaking the challenge into smaller steps made it much easier to understand, debug, and test.

Overall, this challenge helped me improve my understanding of mathematical conversions, `math.floor()`, floating-point values, conditionals, f-strings, edge cases, clock arithmetic, and breaking a larger programming problem into smaller logical steps.
