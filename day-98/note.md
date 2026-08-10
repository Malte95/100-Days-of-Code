# Daily Coding Challenge: Spoken Duration

Today, I completed a Python coding challenge about converting a number of seconds into a duration written in spoken English.

## The Challenge

The function receives a number of seconds and returns the duration using hours, minutes, and seconds.

The requirements are:

* break the total duration into hours, minutes, and seconds
* skip units with a value of zero
* use singular or plural correctly
* connect the last two units with `"and"`
* if all three units are present, separate the first two with a comma

For example:

```text
3723 seconds
```

should become:

```text
1 hour, 2 minutes and 3 seconds
```

To solve this, the first step is to break the total number of seconds into the three different time units.

## Calculating the Hours

One hour contains:

```text
3600 seconds
```

To find out how many complete hours are contained in the total number of seconds, I used integer division:

```python
hours = seconds // 3600
```

The `//` operator performs floor division.

For example:

```text
3723 // 3600 = 1
```

This means that `3723` seconds contains one complete hour.

Normal division would give:

```text
3723 / 3600 = 1.034...
```

But I only need the number of complete hours, so integer division is the correct operation.

Next, I need to know how many seconds are left after removing the complete hours.

For this, I used the modulo operator `%`:

```python
rest = seconds % 3600
```

For example:

```text
3723 % 3600 = 123
```

So after removing one complete hour, there are:

```text
123 seconds
```

remaining.

## Calculating the Minutes

One minute contains:

```text
60 seconds
```

I can use the remaining `123` seconds to calculate the number of complete minutes:

```python
minutes = rest // 60
```

For the example:

```text
123 // 60 = 2
```

So there are two complete minutes.

After that, I calculate the remaining seconds:

```python
seconds = rest % 60
```

For example:

```text
123 % 60 = 3
```

The complete breakdown is therefore:

```text
1 hour
2 minutes
3 seconds
```

## Using `//` and `%`

One important concept in this challenge was understanding the difference between integer division and modulo.

The `//` operator tells me how many complete units fit into a value.

For example:

```text
3723 // 3600 = 1
```

There is one complete hour.

The `%` operator gives me the remainder:

```text
3723 % 3600 = 123
```

There are `123` seconds left after removing the complete hour.

The same idea is then used again for minutes:

```text
123 // 60 = 2
123 % 60 = 3
```

This gives two complete minutes and three remaining seconds.

## Building the Spoken Duration

After calculating the hours, minutes, and seconds, I created an empty list:

```python
time = []
```

This list stores only the time units that should appear in the final result.

The challenge says that zero values should be skipped.

For example:

```text
3603 seconds
```

contains:

```text
1 hour
0 minutes
3 seconds
```

The final result should therefore be:

```text
1 hour and 3 seconds
```

and not:

```text
1 hour, 0 minutes and 3 seconds
```

Because of this, I only add a time unit to the list if its value is greater than zero.

For the hours, I use:

```python
if hours > 0:
```

The same principle is used for minutes and seconds.

## Singular and Plural

The challenge also requires the correct singular or plural form.

For example:

```text
1 hour
2 hours
```

The same applies to minutes:

```text
1 minute
2 minutes
```

and seconds:

```text
1 second
2 seconds
```

I therefore check whether the value is greater than `1`.

For example, for hours:

```python
if hours > 1:
    time.append(f"{hours} hours")
else:
    time.append(f"{hours} hour")
```

If the value is greater than one, I use the plural form.

Otherwise, because I already know that `hours > 0`, the only remaining possibility is:

```text
1
```

so I use the singular form.

I repeated the same idea for minutes and seconds.

## Using f-Strings

I used f-strings to combine the numeric values with the corresponding unit.

For example:

```python
f"{hours} hours"
```

If:

```text
hours = 2
```

the resulting string is:

```text
2 hours
```

These strings are then added to the `time` list using `.append()`.

For example, with `3723` seconds, the list eventually becomes:

```python
["1 hour", "2 minutes", "3 seconds"]
```

## Joining the Time Units

After building the list, I need to format it correctly depending on how many elements it contains.

I use:

```python
len(time)
```

to determine the number of elements.

There are four possible cases.

### No Units

If the input is `0`, all calculated values are zero.

Nothing is added to the list:

```python
[]
```

Because there is no spoken duration to return, I return an empty string:

```python
""
```

### One Unit

If the list contains only one element, I return that element directly.

For example:

```python
["1 minute"]
```

becomes:

```text
1 minute
```

The first element of a Python list can be accessed with:

```python
time[0]
```

### Two Units

If there are two units, they must be connected with `"and"`.

For example:

```python
["1 minute", "1 second"]
```

should become:

```text
1 minute and 1 second
```

I combine the two strings with:

```python
time[0] + " and " + time[1]
```

### Three Units

If all three units are present, the first two units are separated with a comma and the final two are connected with `"and"`.

For example:

```python
["1 hour", "2 minutes", "3 seconds"]
```

becomes:

```text
1 hour, 2 minutes and 3 seconds
```

The three list elements can be accessed using their indexes:

```text
time[0]
time[1]
time[2]
```

The final string is then built using string concatenation.

## My Solution

```python
def get_spoken_duration(seconds):

    time = []

    hours = seconds // 3600
    if hours > 0:
        if hours > 1:
            time.append(f"{hours} hours")
        else:
            time.append(f"{hours} hour")
    rest = seconds % 3600

    minutes = rest // 60
    if minutes > 0:
        if minutes > 1:
            time.append(f"{minutes} minutes")
        else:
            time.append(f"{minutes} minute")
    seconds = rest % 60
    if seconds > 0:
        if seconds > 1:
            time.append(f"{seconds} seconds")
        else:
            time.append(f"{seconds} second")

    if len(time) == 0:
        return ""
    elif len(time) == 1:
        return time[0]
    elif len(time) == 2:
        return time[0] + " and " + time[1]
    else:
        return time[0] + ", " + time[1] + " and " + time[2]
```

## Example

For:

```python
get_spoken_duration(3723)
```

the hours are calculated first:

```text
3723 // 3600 = 1
```

The remaining seconds are:

```text
3723 % 3600 = 123
```

The minutes are:

```text
123 // 60 = 2
```

and the remaining seconds are:

```text
123 % 60 = 3
```

The list therefore becomes:

```python
["1 hour", "2 minutes", "3 seconds"]
```

Because the list contains three elements, the result is:

```text
1 hour, 2 minutes and 3 seconds
```

## What I Learned

During this challenge, I practiced working with:

* integer division using `//`
* the modulo operator `%`
* converting seconds into hours, minutes, and seconds
* Python lists
* `.append()`
* `if`, `elif`, and `else`
* nested `if` statements
* singular and plural words
* f-strings
* `len()`
* list indexes
* string concatenation
* handling zero values
* returning different output formats depending on the number of values

One of the most important things I learned was the relationship between integer division and modulo.

Integer division tells me how many complete units are contained in a number:

```text
3723 // 3600 = 1
```

Modulo tells me what remains:

```text
3723 % 3600 = 123
```

I can then repeat the same process with the remainder:

```text
123 // 60 = 2
123 % 60 = 3
```

This makes it possible to break one large value into smaller units.

I also learned why a list is useful when some values should be skipped.

Instead of immediately creating the final sentence, I first collect only the units that actually exist.

For example:

```text
3603 seconds
```

produces:

```python
["1 hour", "3 seconds"]
```

The zero-minute value never enters the list.

This makes the final formatting easier because I only need to work with values that should actually be displayed.

Another important concept was singular and plural handling.

A value of exactly `1` needs the singular form:

```text
1 hour
1 minute
1 second
```

while larger values need the plural form:

```text
2 hours
5 minutes
20 seconds
```

I also practiced using list indexes.

For example:

```python
time[0]
```

accesses the first element of the list, while:

```python
time[1]
```

accesses the second.

This was useful when creating the final spoken sentence.

Finally, I learned that formatting the result is easier when I first solve the calculation problem and the text-formatting problem separately.

First, I calculate:

```text
hours
minutes
seconds
```

Then I decide which values should be displayed.

Finally, I combine those values into the required sentence.

Breaking the challenge into smaller steps made the problem much easier to understand and solve.

Overall, this challenge helped me improve my understanding of integer division, modulo, lists, conditionals, string formatting, indexing, and breaking a larger programming problem into smaller logical steps.

