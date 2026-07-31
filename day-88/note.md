# Today I Continued My Java Course and Completed a Python Coding Challenge

Today, I continued learning Java and practised using Boolean variables, conditional statements, nested `if` structures, percentage calculations, and formatted output with `printf`.

I also completed a Python coding challenge about converting RGB colors into relative luminance values and calculating their WCAG contrast rating.

---

# Java Course

## Working With Boolean Variables

I started by creating Boolean variables that describe whether a person is a student or a senior:

```java
boolean isStudent = true;
boolean isSenior = true;
```

A Boolean variable can contain one of two values:

```text
true
false
```

These values can be used to control which parts of a program are executed.

In this exercise:

* `isStudent` determines whether the customer receives a student discount.
* `isSenior` determines whether the customer receives a senior discount.

I also created a variable containing the original ticket price:

```java
double price = 9.99;
```

I used `double` because the ticket price contains decimal places.

---

## Using a Basic `if` Statement

My first version only checked whether the customer was a student:

```java
if (isStudent) {
    System.out.println("You get a student discount of 10%");
    price *= 0.9;
}
```

When `isStudent` is `true`, the code inside the block is executed.

The following calculation applies a discount of 10%:

```java
price *= 0.9;
```

This is a shorter version of:

```java
price = price * 0.9;
```

Multiplying the price by `0.9` means that the customer pays 90% of the original price.

The remaining 10% is the discount.

For an original price of `$9.99`, the calculation is:

```text
9.99 × 0.9 = 8.991
```

---

## Printing the Ticket Price

I initially printed the result using `System.out.println()`:

```java
System.out.println("The price of a ticket is: $" + price);
```

This combines text with the value stored inside `price`.

However, because the result is a decimal calculation, the output may contain more decimal places than required.

---

## Adding a Senior Discount

I then expanded the program by checking both `isStudent` and `isSenior`.

```java
boolean isStudent = true;
boolean isSenior = true;
```

This created four possible situations:

| Student | Senior  | Result                       |
| ------- | ------- | ---------------------------- |
| `true`  | `true`  | Student and senior discounts |
| `true`  | `false` | Student discount             |
| `false` | `true`  | Senior discount              |
| `false` | `false` | No discount                  |

To handle these combinations, I used nested `if` statements.

---

## Using Nested `if` Statements

A nested `if` statement is an `if` statement inside another `if` statement.

I first checked whether the person was a student:

```java
if (isStudent) {
```

Inside this block, I checked whether the same person was also a senior:

```java
if (isSenior) {
```

The complete structure begins like this:

```java
if (isStudent) {
    if (isSenior) {
        // Student and senior
    } else {
        // Student but not senior
    }
}
```

This allowed me to apply different discounts depending on both conditions.

---

## Applying Both Discounts

When the customer is both a student and a senior, the program prints both discount messages:

```java
System.out.println("You get a senior discount of 20%");
System.out.println("You get a student discount of 10%");
```

I then applied a combined discount of 30%:

```java
price *= 0.7;
```

Multiplying the original price by `0.7` means that the customer pays 70% of the original price.

The remaining 30% is the discount.

For a ticket price of `$9.99`, the calculation is:

```text
9.99 × 0.7 = 6.993
```

When formatted to two decimal places, the final ticket price becomes:

```text
$6.99
```

---

## Applying Only the Student Discount

When `isStudent` is `true` but `isSenior` is `false`, the nested `else` block is executed:

```java
else {
    System.out.println("You get a student discount of 10%");
    price *= 0.9;
}
```

This applies only the 10% student discount.

The customer therefore pays 90% of the original ticket price.

---

## Handling Non-Students

The outer `else` block handles customers who are not students:

```java
else {
```

Inside this section, I checked whether the customer was a senior:

```java
if (isSenior) {
```

This means the program can still apply the senior discount even when the customer is not a student.

---

## Applying Only the Senior Discount

When the customer is not a student but is a senior, the program prints:

```java
System.out.println("You get a senior discount of 20%");
```

It then applies the senior discount:

```java
price *= 0.8;
```

Multiplying by `0.8` means that the customer pays 80% of the original price.

The remaining 20% is the discount.

For a ticket price of `$9.99`, the calculation is:

```text
9.99 × 0.8 = 7.992
```

Formatted to two decimal places, the customer pays:

```text
$7.99
```

---

## Handling Customers Without a Discount

When the customer is neither a student nor a senior, the final `else` block is executed:

```java
else {
    price *= 1;
}
```

Multiplying the price by `1` leaves it unchanged:

```text
9.99 × 1 = 9.99
```

This means the customer receives no discount.

Although this calculation is not strictly necessary, it makes the final case explicit.

---

## Formatting the Price With `printf`

I improved the ticket output by using `System.out.printf()`:

```java
System.out.printf("The price of a ticket is: $%.2f", price);
```

The format specifier:

```text
%.2f
```

means:

```text
Display a floating-point number with exactly two digits after the decimal point.
```

For example:

```text
6.993
```

is displayed as:

```text
6.99
```

This is especially useful for prices because monetary values are normally displayed with two decimal places.

---

## Final Java Program

```java
public class Main {
    public static void main(String[] args) {

        boolean isStudent = true;
        boolean isSenior = true;
        double price = 9.99;

        if (isStudent) {
            if (isSenior) {
                System.out.println("You get a senior discount of 20%");
                System.out.println("You get a student discount of 10%");
                price *= 0.7;

            } else {
                System.out.println("You get a student discount of 10%");
                price *= 0.9;
            }

            System.out.printf(
                "The price of a ticket is: $%.2f",
                price
            );

        } else {
            if (isSenior) {
                System.out.println("You get a senior discount of 20%");
                price *= 0.8;

            } else {
                price *= 1;
            }

            System.out.printf(
                "The price of a ticket is: $%.2f",
                price
            );
        }
    }
}
```

---

# Python Coding Challenge

## Contrast Rating 3

I also completed a Python coding challenge about calculating the WCAG contrast rating between two RGB colors.

---

## The Goal

The goal was to create a function called:

```python
get_contrast_rating(rgb1, rgb2, is_large_text)
```

The function receives two arrays containing RGB values.

For example:

```python
[255, 255, 255]
```

represents white, while:

```python
[0, 0, 0]
```

represents black.

Each RGB array contains three channels:

```text
[R, G, B]
```

The channels represent:

* Red
* Green
* Blue

Each channel has a value between `0` and `255`.

The Boolean parameter:

```python
is_large_text
```

indicates whether the accessibility rating should use the thresholds for large text or normal text.

The first RGB color is guaranteed to be the lighter color.

The function must return one of the following ratings:

```text
AAA
AA
Fail
```

---

## Creating Lists for the Corrected Channels

I created two empty lists:

```python
result1 = []
result2 = []
```

These lists store the gamma-corrected RGB channels.

`result1` contains the corrected channels from `rgb1`.

`result2` contains the corrected channels from `rgb2`.

---

## Iterating Through the First RGB Array

I used a `for` loop to process every channel in `rgb1`:

```python
for value in range(len(rgb1)):
```

An RGB array normally contains three values, so `range(len(rgb1))` produces:

```text
0
1
2
```

These numbers are the positions of the red, green, and blue channels.

I accessed the actual channel value with:

```python
rgb1[value]
```

---

## Normalizing the RGB Channels

Before calculating luminance, every channel must be converted from the range `0–255` into the range `0–1`.

I divided each channel by `255`:

```python
channel = rgb1[value] / 255
```

For example:

```text
255 / 255 = 1.0
```

A channel value of `0` becomes:

```text
0 / 255 = 0.0
```

A channel value of `100` becomes approximately:

```text
100 / 255 = 0.3922
```

---

## Applying Gamma Correction

After normalizing the channel, I applied the required gamma-correction formula.

When the normalized value is less than or equal to `0.04045`, I divided it by `12.92`:

```python
if channel <= 0.04045:
    channel = channel / 12.92
```

When the value is greater than `0.04045`, I used the second formula:

```python
else:
    channel = ((channel + 0.055) / 1.055) ** 2.4
```

In Python, the operator:

```python
**
```

is used for exponentiation.

Therefore:

```python
value ** 2.4
```

means that the value is raised to the power of `2.4`.

---

## Saving the Corrected Channels

After applying gamma correction, I added the corrected value to `result1`:

```python
result1.append(channel)
```

Because this statement is inside the loop, all three corrected channels are stored.

After the loop, the list contains:

```text
[corrected red, corrected green, corrected blue]
```

---

## Assigning the First RGB Channels

I assigned the three corrected channels to separate variables:

```python
R1 = result1[0]
G1 = result1[1]
B1 = result1[2]
```

The list positions represent:

```text
result1[0] = red
result1[1] = green
result1[2] = blue
```

---

## Calculating the First Relative Luminance

I calculated the relative luminance of `rgb1` with the WCAG formula:

```python
luminance1 = 0.2126 * R1 + 0.7152 * G1 + 0.0722 * B1
```

The channels use different weights:

```text
Red:   0.2126
Green: 0.7152
Blue:  0.0722
```

Green has the largest influence on the luminance value.

Blue has the smallest influence.

---

## Processing the Second RGB Color

I repeated the same steps for `rgb2`.

First, I iterated through its channels:

```python
for value in range(len(rgb2)):
```

I normalized each channel:

```python
channel = rgb2[value] / 255
```

I then applied gamma correction:

```python
if channel <= 0.04045:
    channel = channel / 12.92
else:
    channel = ((channel + 0.055) / 1.055) ** 2.4
```

Finally, I stored the corrected channel:

```python
result2.append(channel)
```

---

## Calculating the Second Relative Luminance

I assigned the corrected channels from `result2`:

```python
R2 = result2[0]
G2 = result2[1]
B2 = result2[2]
```

I then calculated the second relative luminance:

```python
luminance2 = 0.2126 * R2 + 0.7152 * G2 + 0.0722 * B2
```

At this point, I had one luminance value for each color:

```text
luminance1
luminance2
```

---

## Calculating the Contrast Ratio

The WCAG contrast ratio is calculated by adding `0.05` to both luminance values.

The adjusted luminance of the lighter color is then divided by the adjusted luminance of the darker color:

```python
contrast_ratio = (luminance1 + 0.05) / (luminance2 + 0.05)
```

The challenge guarantees that `rgb1` is always the lighter color.

Therefore, `luminance1` is placed above `luminance2` in the division.

The smallest possible contrast ratio is:

```text
1:1
```

This occurs when both colors are identical.

The highest possible contrast ratio is:

```text
21:1
```

This occurs between pure white and pure black.

---

## Contrast Rating Requirements

The result depends on both the contrast ratio and the text size.

| Rating   | Normal Text | Large Text |
| -------- | ----------: | ---------: |
| `"AAA"`  |        7.0+ |       4.5+ |
| `"AA"`   |        4.5+ |       3.0+ |
| `"Fail"` |   Below 4.5 |  Below 3.0 |

---

## Checking Large Text

I first checked whether `is_large_text` is `True`:

```python
if is_large_text:
```

For large text, a contrast ratio of at least `4.5` receives the `"AAA"` rating:

```python
if contrast_ratio >= 4.5:
    return "AAA"
```

A ratio of at least `3.0` receives the `"AA"` rating:

```python
elif contrast_ratio >= 3.0:
    return "AA"
```

Anything below `3.0` fails:

```python
else:
    return "Fail"
```

---

## Checking Normal Text

When `is_large_text` is `False`, the function uses the stricter normal-text requirements.

A ratio of at least `7.0` receives `"AAA"`:

```python
if contrast_ratio >= 7.0:
    return "AAA"
```

A ratio of at least `4.5` receives `"AA"`:

```python
elif contrast_ratio >= 4.5:
    return "AA"
```

Anything below `4.5` returns:

```python
"Fail"
```

---

## Checking the Highest Rating First

I checked the `"AAA"` condition before checking the `"AA"` condition.

For example, a normal-text contrast ratio of `8.0` satisfies both comparisons:

```text
8.0 >= 7.0
8.0 >= 4.5
```

However, the correct result is `"AAA"`.

By checking the highest threshold first, the function immediately returns the highest valid rating.

---

## Final Python Solution

```python
def get_contrast_rating(rgb1, rgb2, is_large_text):

    result1 = []
    result2 = []

    for value in range(len(rgb1)):
        channel = rgb1[value] / 255

        if channel <= 0.04045:
            channel = channel / 12.92
        else:
            channel = ((channel + 0.055) / 1.055) ** 2.4

        result1.append(channel)

    R1 = result1[0]
    G1 = result1[1]
    B1 = result1[2]

    luminance1 = 0.2126 * R1 + 0.7152 * G1 + 0.0722 * B1

    for value in range(len(rgb2)):
        channel = rgb2[value] / 255

        if channel <= 0.04045:
            channel = channel / 12.92
        else:
            channel = ((channel + 0.055) / 1.055) ** 2.4

        result2.append(channel)

    R2 = result2[0]
    G2 = result2[1]
    B2 = result2[2]

    luminance2 = 0.2126 * R2 + 0.7152 * G2 + 0.0722 * B2

    contrast_ratio = (luminance1 + 0.05) / (luminance2 + 0.05)

    if is_large_text:
        if contrast_ratio >= 4.5:
            return "AAA"
        elif contrast_ratio >= 3.0:
            return "AA"
        else:
            return "Fail"

    else:
        if contrast_ratio >= 7.0:
            return "AAA"
        elif contrast_ratio >= 4.5:
            return "AA"
        else:
            return "Fail"
```

---

# What I Learned Today

Today’s Java exercise helped me understand how Boolean values can control the flow of a program.

I practised declaring and using variables such as:

```java
boolean isStudent;
boolean isSenior;
double price;
```

I also practised using:

```java
if
else
```

Nested `if` statements helped me handle several related conditions.

Instead of checking only whether someone was a student, I was able to distinguish between:

* Students
* Seniors
* People who are both students and seniors
* People who receive no discount

I also practised percentage calculations with compound assignment operators:

```java
price *= 0.9;
price *= 0.8;
price *= 0.7;
```

These calculations showed me how multiplying by a decimal value can apply a percentage discount.

Using:

```java
System.out.printf()
```

helped me display prices in a cleaner format.

The format specifier:

```text
%.2f
```

ensures that prices are displayed with exactly two decimal places.

The Python coding challenge helped me practise:

* Iterating through lists
* Accessing list elements by index
* Normalizing numerical values
* Applying different mathematical formulas depending on a condition
* Appending calculated values to a list
* Calculating relative luminance
* Calculating a contrast ratio
* Working with Boolean parameters
* Using nested `if`, `elif`, and `else` statements
* Comparing values with `>=`
* Returning different strings depending on numerical thresholds

The challenge also showed me why the order of operations inside a program is important.

I first had to:

1. Normalize each RGB channel.
2. Apply gamma correction.
3. Store the corrected channels.
4. Calculate both luminance values.
5. Calculate the contrast ratio.
6. Determine the correct WCAG rating.

Overall, I practised using conditional logic in both Java and Python.

In Java, the conditions controlled ticket discounts.

In Python, the conditions controlled gamma correction and accessibility ratings.

Both exercises helped me understand how programs can make decisions based on Boolean values and numerical comparisons.

