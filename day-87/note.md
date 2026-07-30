# My Java Learning Progress Today ☕

Today, I continued learning Java and focused on formatted console output with `printf()`.

I learned how format specifiers, precision, flags and field widths can be used to control how different values are displayed. I also built a compound interest calculator that receives financial information from the user and calculates the future value of an investment.

## What I learned

* Using `System.out.printf()`
* Formatting `String`, `char`, `int`, `double` and `boolean` values
* Printing several variables in one formatted statement
* Controlling decimal precision
* Displaying positive and negative signs
* Adding grouping separators to large numbers
* Displaying negative numbers inside parentheses
* Adding spaces before positive numbers
* Padding integers with zeros
* Right-aligning and left-aligning output
* Reading numerical input with `Scanner`
* Converting a percentage into a decimal value
* Using `Math.pow()`
* Calculating compound interest
* Formatting a calculated monetary amount

## The printf() method

I started by learning about the `printf()` method.

`printf()` is used to produce formatted output. Unlike `println()`, it allows me to control how variables are displayed.

The general structure of a format placeholder is:

```text
%[flags][width][.precision][specifier-character]
```

Each placeholder begins with the `%` symbol.

The remaining parts determine how the corresponding value should be displayed.

## Format specifiers

I created variables with several different data types:

```java
String name = "Spongebob";
char firstLetter = 'S';
int age = 30;
double height = 60.5;
boolean isEmployed = true;
```

I then displayed them with the appropriate format specifiers:

```java
System.out.printf("Hello %s\n", name);
System.out.printf("Your name starts with a %c\n", firstLetter);
System.out.printf("Your age is %d years old\n", age);
System.out.printf("You are %f inches tall\n", height);
System.out.printf("Employed: %b\n", isEmployed);
```

The format specifiers have the following meanings:

* `%s` displays a `String`.
* `%c` displays a character.
* `%d` displays an integer.
* `%f` displays a floating-point number.
* `%b` displays a boolean value.

The `\n` character starts a new line after each output.

## Using multiple values in one printf() statement

I learned that one `printf()` statement can contain several placeholders:

```java
System.out.printf("%s is %d years old", name, age);
```

The values after the format string are inserted into the placeholders from left to right.

In this example:

* `%s` is replaced by the value of `name`.
* `%d` is replaced by the value of `age`.

The resulting output is:

```text
Spongebob is 30 years old
```

## Formatting decimal numbers

By default, `%f` displays six digits after the decimal point.

For example:

```java
double price1 = 9.99;
double price2 = 100.15;
double price3 = -54.01;

System.out.printf("%f\n", price1);
System.out.printf("%f\n", price2);
System.out.printf("%f\n", price3);
```

The output is:

```text
9.990000
100.150000
-54.010000
```

## Controlling decimal precision

I used the precision section of the placeholder to control how many decimal places are displayed.

For one decimal place, I used `%.1f`:

```java
System.out.printf("%.1f\n", price1);
System.out.printf("%.1f\n", price2);
System.out.printf("%.1f\n", price3);
```

This produces:

```text
10.0
100.2
-54.0
```

The values are rounded to one decimal place.

For two decimal places, I used `%.2f`:

```java
System.out.printf("%.2f\n", price1);
System.out.printf("%.2f\n", price2);
System.out.printf("%.2f\n", price3);
```

This produces:

```text
9.99
100.15
-54.01
```

Using two decimal places is especially useful when displaying monetary values.

## Displaying a sign

The `+` flag displays a sign before both positive and negative numbers:

```java
System.out.printf("%+.2f\n", price1);
System.out.printf("%+.2f\n", price2);
System.out.printf("%+.2f\n", price3);
```

The output is:

```text
+9.99
+100.15
-54.01
```

Positive numbers receive a `+` sign, while negative numbers continue to use a `-` sign.

## Grouping large numbers

The comma flag adds grouping separators to large numbers.

I tested it with the following values:

```java
double price1 = 9000.99;
double price2 = 100000.15;
double price3 = -54000.01;
```

I formatted them using `%,.2f`:

```java
System.out.printf("%,.2f\n", price1);
System.out.printf("%,.2f\n", price2);
System.out.printf("%,.2f\n", price3);
```

This makes large values easier to read by separating groups of thousands.

The exact separator displayed can depend on the active locale.

## Displaying negative numbers with parentheses

The `(` flag displays negative numbers inside parentheses instead of using a minus sign:

```java
System.out.printf("%(.2f\n", price1);
System.out.printf("%(.2f\n", price2);
System.out.printf("%(.2f\n", price3);
```

A negative value such as `-54.01` is displayed as:

```text
(54.01)
```

Positive numbers are displayed normally.

This style is often used in financial and accounting reports.

## Adding a leading space

The space flag adds a space before positive numbers while negative numbers retain their minus sign:

```java
System.out.printf("% .2f\n", price1);
System.out.printf("% .2f\n", price2);
System.out.printf("% .2f\n", price3);
```

This can help align positive and negative values in a list.

## Zero padding

I also practiced formatting integer IDs:

```java
int id1 = 1;
int id2 = 23;
int id3 = 456;
int id4 = 7890;
```

Using `%04d` creates a field that is at least four characters wide and fills empty positions with zeros:

```java
System.out.printf("%04d\n", id1);
System.out.printf("%04d\n", id2);
System.out.printf("%04d\n", id3);
System.out.printf("%04d\n", id4);
```

The output is:

```text
0001
0023
0456
7890
```

This can be useful for IDs, reference numbers and other values that should have a consistent length.

## Right-aligned padding

A positive field width right-aligns a value.

I used `%4d`:

```java
System.out.printf("%4d\n", id1);
System.out.printf("%4d\n", id2);
System.out.printf("%4d\n", id3);
System.out.printf("%4d\n", id4);
```

Each value occupies a field that is at least four characters wide.

Shorter values receive spaces on the left:

```text
   1
  23
 456
7890
```

## Left-aligned padding

The `-` flag left-aligns a value inside the field.

I used `%-4d`:

```java
System.out.printf("%-4d\n", id1);
System.out.printf("%-4d\n", id2);
System.out.printf("%-4d\n", id3);
System.out.printf("%-4d\n", id4);
```

Shorter values receive spaces on the right instead of the left.

This is useful when creating aligned columns or table-like output.

## Compound interest calculator

After practicing `printf()`, I built a compound interest calculator.

The program asks the user to enter:

* The principal amount
* The annual interest rate
* The number of times interest is compounded per year
* The number of years

The program then calculates the final amount.

## Creating the Scanner

I imported and created a `Scanner` so that the program could receive user input:

```java
import java.util.Scanner;
```

Inside the `main()` method, I created the scanner:

```java
Scanner scanner = new Scanner(System.in);
```

I also declared the required variables:

```java
double principal;
double rate;
int timesCompounded;
int years;
double amount;
```

I used `double` for values that can contain decimal places and `int` for whole-number values.

## Receiving the principal amount

The principal is the starting amount of money:

```java
System.out.print("Enter the principal amount: ");
principal = scanner.nextDouble();
```

The value entered by the user is stored in the `principal` variable.

## Converting the interest rate

The user enters the interest rate as a percentage:

```java
System.out.print("Enter the interest rate (in %): ");
rate = scanner.nextDouble() / 100;
```

Dividing the entered value by `100` converts the percentage into a decimal value.

For example:

```text
5% = 5 / 100 = 0.05
```

The decimal version is required for the compound interest formula.

## Receiving the compounding frequency

The program asks how many times the interest is compounded each year:

```java
System.out.print("Enter the # of times compounded per year: ");
timesCompounded = scanner.nextInt();
```

For example:

* `1` means annually.
* `4` means quarterly.
* `12` means monthly.

## Receiving the number of years

The program also asks how long the money will remain invested:

```java
System.out.print("Enter the # of years: ");
years = scanner.nextInt();
```

The entered value is stored as an integer.

## Calculating compound interest

I used the compound interest formula:

```text
amount = principal × (1 + rate / timesCompounded)^(timesCompounded × years)
```

In Java, the calculation looks like this:

```java
amount = principal * Math.pow(
        1 + rate / timesCompounded,
        timesCompounded * years
);
```

`Math.pow()` raises its first argument to the power of its second argument.

In this calculation:

* `principal` is the original amount.
* `rate` is the annual interest rate as a decimal.
* `timesCompounded` is the number of compounding periods per year.
* `years` is the total investment duration.
* `amount` is the final value after interest has been added.

## Formatting the result

At first, the result could be displayed using string concatenation:

```java
System.out.println("The amount after " + years + " is: $" + amount);
```

However, this could display too many decimal places.

I improved the output by combining the project with what I had learned about `printf()`:

```java
System.out.printf(
        "The amount after %d years is $%.2f",
        years,
        amount
);
```

Here:

* `%d` displays the number of years.
* `%.2f` displays the final amount with exactly two decimal places.

This produces a cleaner result that is more suitable for money.

## Completed program

My completed compound interest calculator looked like this:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        // Compound Interest Calculator

        Scanner scanner = new Scanner(System.in);

        double principal;
        double rate;
        int timesCompounded;
        int years;
        double amount;

        System.out.print("Enter the principal amount: ");
        principal = scanner.nextDouble();

        System.out.print("Enter the interest rate (in %): ");
        rate = scanner.nextDouble() / 100;

        System.out.print("Enter the # of times compounded per year: ");
        timesCompounded = scanner.nextInt();

        System.out.print("Enter the # of years: ");
        years = scanner.nextInt();

        amount = principal * Math.pow(
                1 + rate / timesCompounded,
                timesCompounded * years
        );

        System.out.printf(
                "The amount after %d years is $%.2f",
                years,
                amount
        );

        scanner.close();
    }
}
```

## Final reflection

Today, I improved my understanding of formatted console output in Java.

I learned that `printf()` can do much more than simply print a variable. Format specifiers determine which data type is displayed, while flags, widths and precision values control the appearance of the output.

I practiced displaying text, characters, integers, decimal numbers and boolean values. I also learned how to round decimal output, add signs, group large numbers, format negative values and align integers inside fixed-width fields.

The compound interest calculator allowed me to combine several concepts from previous lessons, including variables, user input, arithmetic calculations and console output.

I also used `Math.pow()` for the first time to perform an exponent calculation. Finally, I applied `printf()` to display the calculated amount with two decimal places.

This project showed me how Java can receive information from a user, perform a financial calculation and present the result in a clear and professional format.
