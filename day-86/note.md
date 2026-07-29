# Today I Continued My Java Course and Completed a Python Coding Challenge

Today, I continued learning Java and practised using the `Math` class, user input with `Scanner`, mathematical formulas, and formatted output with `printf`.

I also completed a Python coding challenge about calculating WCAG contrast ratings.

---

# Java Course

## Creating the Basic Java Program Structure

I started with the basic structure of a Java program:

```java
public class Main {
    public static void main(String[] args) {



    }
}
```

The `Main` class contains the program.

```java
public class Main
```

The `main` method is the starting point of the program:

```java
public static void main(String[] args)
```

When the program is executed, Java begins running the instructions inside this method.

---

## Using the Java Math Class

Java provides a built-in class called `Math`.

The `Math` class contains mathematical constants and methods that can be used without creating a `Math` object.

For example:

```java
System.out.println(Math.PI);
System.out.println(Math.E);
```

`Math.PI` contains an approximation of the mathematical constant π:

```text
3.141592653589793
```

`Math.E` contains an approximation of Euler’s number:

```text
2.718281828459045
```

These constants can be used in mathematical formulas.

---

## Calculating Powers With `Math.pow()`

I used the `Math.pow()` method to calculate a power:

```java
double result;

result = Math.pow(2, 3);

System.out.println(result);
```

The first argument is the base and the second argument is the exponent.

```java
Math.pow(2, 3)
```

This represents:

```text
2³
```

The calculation is:

```text
2 × 2 × 2 = 8
```

The result is returned as a `double`:

```text
8.0
```

---

## Calculating Absolute Values With `Math.abs()`

I then used `Math.abs()`:

```java
result = Math.abs(-5);
```

An absolute value represents the distance of a number from zero.

The absolute value is therefore never negative.

```text
|-5| = 5
```

The value stored in `result` becomes:

```text
5.0
```

Because each new value is assigned to the same variable, it replaces the value that was previously stored in `result`.

---

## Calculating Square Roots With `Math.sqrt()`

I used `Math.sqrt()` to calculate a square root:

```java
result = Math.sqrt(9);
```

The square root of `9` is `3` because:

```text
3 × 3 = 9
```

The method returns:

```text
3.0
```

---

## Rounding Numbers

Java provides several methods for rounding decimal numbers.

### `Math.round()`

```java
result = Math.round(3.14);
```

`Math.round()` rounds a value to the nearest whole number.

Because `3.14` is closer to `3` than to `4`, the result is:

```text
3
```

### `Math.ceil()`

```java
result = Math.ceil(3.14);
```

`Math.ceil()` always rounds upward to the next whole number.

The result is:

```text
4.0
```

### `Math.floor()`

```java
result = Math.floor(3.99);
```

`Math.floor()` always rounds downward.

The result is:

```text
3.0
```

The difference between these methods is:

```text
Math.round(3.14) = 3
Math.ceil(3.14)  = 4.0
Math.floor(3.99) = 3.0
```

---

## Finding Maximum and Minimum Values

I also used `Math.max()` and `Math.min()`.

### `Math.max()`

```java
result = Math.max(10, 20);
```

`Math.max()` compares two values and returns the larger one.

```text
20
```

### `Math.min()`

```java
result = Math.min(10, 20);
```

`Math.min()` returns the smaller value.

```text
10
```

---

## Complete Math Class Example

```java
public class Main {
    public static void main(String[] args) {

        // System.out.println(Math.PI);
        // System.out.println(Math.E);

        double result;

        result = Math.pow(2, 3);
        result = Math.abs(-5);
        result = Math.sqrt(9);
        result = Math.round(3.14);
        result = Math.ceil(3.14);
        result = Math.floor(3.99);
        result = Math.max(10, 20);
        result = Math.min(10, 20);

        System.out.println(result);
    }
}
```

Every assignment replaces the previous value of `result`.

Therefore, only the result of the final calculation is printed:

```java
result = Math.min(10, 20);
```

The output is:

```text
10.0
```

---

# Hypotenuse Calculator

I then created a program that calculates the hypotenuse of a right triangle.

The program asks the user to enter the lengths of sides `a` and `b`.

It then calculates side `c` using the Pythagorean theorem.

The formula is:

```text
c = √(a² + b²)
```

## Importing Scanner

To receive input from the user, I imported the `Scanner` class:

```java
import java.util.Scanner;
```

I then created a `Scanner` object:

```java
Scanner scanner = new Scanner(System.in);
```

`System.in` tells the scanner to read input entered through the console.

---

## Declaring the Variables

I declared three variables:

```java
double a;
double b;
double c;
```

`a` and `b` contain the lengths entered by the user.

`c` stores the calculated hypotenuse.

I used `double` because side lengths can contain decimal values.

---

## Reading the User Input

The program asks for side `a`:

```java
System.out.print("Enter the length of side A: ");
a = scanner.nextDouble();
```

It then asks for side `b`:

```java
System.out.print("Enter the length of side B: ");
b = scanner.nextDouble();
```

`scanner.nextDouble()` reads a decimal number from the console.

---

## Calculating the Hypotenuse

The calculation is:

```java
c = Math.sqrt(Math.pow(a, 2) + Math.pow(b, 2));
```

First, both side lengths are squared:

```java
Math.pow(a, 2)
Math.pow(b, 2)
```

The squared values are added together:

```text
a² + b²
```

Finally, `Math.sqrt()` calculates the square root:

```text
√(a² + b²)
```

For example, when:

```text
a = 3
b = 4
```

the calculation is:

```text
c = √(3² + 4²)
```

This becomes:

```text
c = √(9 + 16)
c = √25
c = 5
```

---

## Printing the Result

The result is displayed with:

```java
System.out.println(
    "The hypotenuse (side c) is the following: " + c + "cm"
);
```

For sides `3` and `4`, the output is:

```text
The hypotenuse (side c) is the following: 5.0cm
```

---

## Closing the Scanner

At the end of the program, I closed the scanner:

```java
scanner.close();
```

Closing the scanner releases the resource after it is no longer needed.

---

## Final Hypotenuse Program

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        // HYPOTENUSE c = Math.sqrt(a^2 + b^2)

        Scanner scanner = new Scanner(System.in);

        double a;
        double b;
        double c;

        System.out.print("Enter the length of side A: ");
        a = scanner.nextDouble();

        System.out.print("Enter the length of side B: ");
        b = scanner.nextDouble();

        c = Math.sqrt(Math.pow(a, 2) + Math.pow(b, 2));

        System.out.println(
            "The hypotenuse (side c) is the following: " + c + "cm"
        );

        scanner.close();
    }
}
```

---

# Circle and Sphere Calculator

I also created a program that receives a radius and calculates:

* The circumference of a circle
* The area of a circle
* The volume of a sphere

The program uses `Math.PI` and `Math.pow()`.

---

## The Formulas

The circumference of a circle is calculated with:

```text
circumference = 2 × π × radius
```

The area of a circle is:

```text
area = π × radius²
```

The volume of a sphere is:

```text
volume = 4/3 × π × radius³
```

In Java, the formulas are:

```java
circumference = 2 * Math.PI * radius;
area = Math.PI * Math.pow(radius, 2);
volume = (4.0 / 3.0) * Math.PI * Math.pow(radius, 3);
```

---

## Reading the Radius

The user is asked to enter a radius:

```java
System.out.print("Enter the radius: ");
radius = scanner.nextDouble();
```

The entered number is stored in the `radius` variable.

---

## Calculating the Circumference

The circumference is calculated with:

```java
circumference = 2 * Math.PI * radius;
```

For example, when the radius is `5`:

```text
circumference = 2 × π × 5
```

The result is approximately:

```text
31.4159
```

---

## Calculating the Area

The area is calculated with:

```java
area = Math.PI * Math.pow(radius, 2);
```

For a radius of `5`:

```text
area = π × 5²
area = π × 25
```

The result is approximately:

```text
78.5398
```

The unit for an area is squared:

```text
cm²
```

---

## Calculating the Volume

The volume is calculated with:

```java
volume = (4.0 / 3.0) * Math.PI * Math.pow(radius, 3);
```

I used:

```java
4.0 / 3.0
```

instead of:

```java
4 / 3
```

When both numbers are integers, Java performs integer division.

```text
4 / 3 = 1
```

The decimal part would be removed.

Using decimal values performs floating-point division:

```text
4.0 / 3.0 = 1.3333...
```

For a radius of `5`, the volume is approximately:

```text
523.5988
```

The unit for a volume is cubed:

```text
cm³
```

---

## Printing the Values With `println`

My first version printed the complete decimal values:

```java
System.out.println("The circumference is: " + circumference + "cm");
System.out.println("The area is: " + area + "cm²");
System.out.println("The volume is: " + volume + "cm³");
```

This works, but the results can contain many digits after the decimal point.

---

## Formatting the Output With `printf`

I improved the output by using `System.out.printf()`:

```java
System.out.printf("The circumference is: %.1fcm\n", circumference);
System.out.printf("The area is: %.1fcm²\n", area);
System.out.printf("The volume is: %.1fcm³\n", volume);
```

The format specifier:

```text
%.1f
```

means:

```text
Display a floating-point value with one digit after the decimal point.
```

For example:

```text
31.4159
```

is displayed as:

```text
31.4
```

The newline character:

```text
\n
```

moves the cursor to the next line after the value is printed.

---

## Final Circle and Sphere Program

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        // circumference = 2 * Math.PI * radius;
        // area = Math.PI * Math.pow(radius, 2);
        // volume = (4.0 / 3.0) * Math.PI * Math.pow(radius, 3);

        Scanner scanner = new Scanner(System.in);

        double radius;
        double circumference;
        double area;
        double volume;

        System.out.print("Enter the radius: ");
        radius = scanner.nextDouble();

        circumference = 2 * Math.PI * radius;
        area = Math.PI * Math.pow(radius, 2);
        volume = (4.0 / 3.0) * Math.PI * Math.pow(radius, 3);

        System.out.printf(
            "The circumference is: %.1fcm\n",
            circumference
        );

        System.out.printf(
            "The area is: %.1fcm²\n",
            area
        );

        System.out.printf(
            "The volume is: %.1fcm³\n",
            volume
        );

        scanner.close();
    }
}
```

For a radius of `5`, the formatted output is:

```text
The circumference is: 31.4cm
The area is: 78.5cm²
The volume is: 523.6cm³
```

---

# Python Coding Challenge

## Contrast Rating 2

I also completed a Python coding challenge about calculating WCAG contrast ratings.

## The Goal

The goal was to create a function called:

```python
get_contrast_rating(l1, l2, is_large_text)
```

The function receives:

* The relative luminance of the lighter color
* The relative luminance of the darker color
* A Boolean indicating whether the text is large

The lighter luminance value is always the first argument.

The function must calculate the contrast ratio and return:

```text
AAA
AA
Fail
```

---

## Calculating the Contrast Ratio

The contrast ratio is calculated by adding `0.05` to both luminance values.

The adjusted lighter value is then divided by the adjusted darker value:

```text
contrast ratio = (l1 + 0.05) ÷ (l2 + 0.05)
```

In Python:

```python
quotient = (l1 + 0.05) / (l2 + 0.05)
```

In my solution, I first updated the variables:

```python
l1 += 0.05
l2 += 0.05
```

I then performed the division:

```python
quotient = l1 / l2
```

---

## Contrast Rating Requirements

The rating depends on the contrast ratio and the text size.

| Rating   | Normal Text | Large Text |
| -------- | ----------: | ---------: |
| `"AAA"`  |        7.0+ |       4.5+ |
| `"AA"`   |        4.5+ |       3.0+ |
| `"Fail"` |   Below 4.5 |  Below 3.0 |

For large text:

```text
AAA: 4.5 or higher
AA: 3.0 or higher
Fail: below 3.0
```

For normal text:

```text
AAA: 7.0 or higher
AA: 4.5 or higher
Fail: below 4.5
```

---

## Checking Whether the Text Is Large

The Boolean parameter is called:

```python
is_large_text
```

When it is `True`, the function uses the large-text thresholds:

```python
if is_large_text:
```

When it is `False`, the function uses the normal-text thresholds:

```python
else:
```

---

## Checking the Highest Rating First

The function checks the `"AAA"` requirement before checking the `"AA"` requirement.

For example, a large-text contrast ratio of `5.0` satisfies both of these comparisons:

```text
5.0 >= 4.5
5.0 >= 3.0
```

However, the correct rating is `"AAA"`.

Checking the highest threshold first ensures that the function returns the highest valid rating.

---

## My Final Python Function

```python
def get_contrast_rating(l1, l2, is_large_text):
    l1 += 0.05
    l2 += 0.05

    quotient = l1 / l2

    if is_large_text:
        if quotient >= 4.5:
            return "AAA"
        elif quotient >= 3.0:
            return "AA"
        else:
            return "Fail"

    else:
        if quotient >= 7.0:
            return "AAA"
        elif quotient >= 4.5:
            return "AA"
        else:
            return "Fail"
```

---

## The Tests

The function passed all six tests:

```python
assert get_contrast_rating(1.0, 0.0, False) == "AAA"
assert get_contrast_rating(0.9015, 0.1364, False) == "AA"
assert get_contrast_rating(0.8965, 0.1628, False) == "Fail"

assert get_contrast_rating(0.7469, 0.0957, True) == "AAA"
assert get_contrast_rating(0.7489, 0.2018, True) == "AA"
assert get_contrast_rating(0.6571, 0.1974, True) == "Fail"
```

---

## Example Calculation

For the following function call:

```python
get_contrast_rating(1.0, 0.0, False)
```

The calculation is:

```text
(1.0 + 0.05) ÷ (0.0 + 0.05)
```

This becomes:

```text
1.05 ÷ 0.05 = 21.0
```

The text is normal text.

A contrast ratio of `21.0` is greater than the `"AAA"` threshold of `7.0`.

Therefore, the function returns:

```text
AAA
```

---

# What I Learned Today

Today’s Java exercises helped me understand how to use the built-in `Math` class.

I practised working with:

```java
Math.PI
Math.E
Math.pow()
Math.abs()
Math.sqrt()
Math.round()
Math.ceil()
Math.floor()
Math.max()
Math.min()
```

I also learned how several assignments to the same variable replace its previous value.

The hypotenuse calculator helped me combine user input, mathematical methods, and the Pythagorean theorem in one program.

The circle and sphere calculator helped me translate mathematical formulas into Java expressions.

It also showed me why decimal numbers are important when performing division.

Using:

```java
4.0 / 3.0
```

prevents Java from performing integer division.

I also practised using `System.out.printf()` and format specifiers such as:

```text
%.1f
```

This makes numerical output shorter and easier to read.

The Python coding challenge helped me practise:

* Translating a mathematical formula into code
* Working with Boolean values
* Using nested `if`, `elif`, and `else` statements
* Comparing values with `>=`
* Applying different thresholds
* Checking the highest matching condition first

Overall, I practised combining mathematical formulas with programming logic in both Java and Python.


