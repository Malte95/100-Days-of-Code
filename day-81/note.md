# My Java Learning Progress Today ☕

Today, I continued learning Java and worked with arithmetic operators, assignment operators, increment and decrement operators, the order of operations, user input and `if` statements.

I also built a small shopping cart program that calculates the total price of several items.

## What I learned

* Arithmetic operators
* The modulo operator `%`
* Augmented assignment operators
* Incrementing and decrementing numbers
* The difference between `int` and `double` division
* The order of operations
* Calculating a total price
* Using user input inside a program
* Writing conditions with `if`, `else if` and `else`
* Comparing numbers
* Checking whether a `String` is empty
* Using a boolean value as a condition

## Arithmetic operators

I started by practicing the basic arithmetic operators in Java:

```java
int x = 10;
int y = 2;
int z;

z = x + y;
z = x - y;
z = x * y;
z = x / y;
z = x % y;
```

The operators have the following meanings:

* `+` adds two values.
* `-` subtracts one value from another.
* `*` multiplies two values.
* `/` divides one value by another.
* `%` returns the remainder of a division.

For example:

```java
int x = 10;
int y = 3;

int z = x % y;

System.out.println(z);
```

The result is:

```text
1
```

This is because `10` divided by `3` leaves a remainder of `1`.

## Augmented assignment operators

I also learned how augmented assignment operators can make calculations shorter.

Instead of writing:

```java
x = x + y;
```

I can write:

```java
x += y;
```

Other augmented assignment operators include:

```java
x += y;
x -= y;
x *= y;
x /= y;
x %= y;
```

Each operator performs a calculation and assigns the result back to the original variable.

## Integer and decimal division

I learned that dividing two `int` values only produces a whole number:

```java
int x = 10;
int y = 3;

x /= y;

System.out.println(x);
```

The result is:

```text
3
```

The decimal part is removed because `x` and `y` are integers.

To receive a decimal result, I used the `double` data type:

```java
double x = 10;
double y = 3;

x /= y;

System.out.println(x);
```

This produces a result close to:

```text
3.3333333333333335
```

## Increment and decrement operators

The increment operator `++` increases a number by `1`.

```java
int x = 1;

x++;
x++;
x++;

System.out.println(x);
```

The result is:

```text
4
```

The decrement operator `--` decreases a number by `1`.

```java
int x = 1;

x--;
x--;
x--;

System.out.println(x);
```

The result is:

```text
-2
```

## Order of operations

I practiced Java's order of operations using the rule:

```text
P-E-M-D-A-S
```

This means:

* Parentheses
* Exponents
* Multiplication
* Division
* Addition
* Subtraction

I used the following calculation:

```java
double result = 3 + 4 * (7 - 5) / 2.0;

System.out.println(result);
```

Java first calculates the parentheses:

```text
7 - 5 = 2
```

It then performs multiplication and division before addition:

```text
4 × 2 = 8
8 ÷ 2.0 = 4.0
3 + 4.0 = 7.0
```

The final result is:

```text
7.0
```

Using `2.0` ensures that the division is performed as decimal division.

## Shopping cart program

I built a shopping cart program that asks the user for:

* The name of an item
* The price of one item
* The desired quantity

The program calculates the total price by multiplying the price by the quantity:

```java
total = price * quantity;
```

My completed program looked like this:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        // SHOPPING CART PROGRAM

        Scanner scanner = new Scanner(System.in);

        String item;
        double price;
        int quantity;
        char currency = '$';
        double total;

        System.out.print("What item would you like to buy?: ");
        item = scanner.nextLine();

        System.out.print("What is the price for each?: ");
        price = scanner.nextDouble();

        System.out.print("How many would you like?: ");
        quantity = scanner.nextInt();

        total = price * quantity;

        System.out.println("\nYou have bought " + quantity + " " + item + "/s");
        System.out.println("Your total is " + currency + total);

        scanner.close();
    }
}
```

This exercise combined user input, variables, arithmetic operators and console output.

## If statements

I then started learning about `if` statements.

An `if` statement performs a block of code when its condition is `true`.

```java
int age = 25;

if (age >= 18) {
    System.out.println("You are an adult.");
} else {
    System.out.println("You are not an adult.");
}
```

The comparison operator `>=` means “greater than or equal to.”

## Multiple conditions with else if

I also used `else if` to check several possible conditions:

```java
int age = 50;

if (age >= 65) {
    System.out.println("You are a senior!");
} else if (age >= 18) {
    System.out.println("You are an adult!");
} else if (age < 0) {
    System.out.println("You haven't been born yet!");
} else if (age == 0) {
    System.out.println("You are a baby!");
} else {
    System.out.println("You are a child!");
}
```

Java checks the conditions from top to bottom. As soon as one condition is `true`, its code is executed and the remaining conditions are skipped.

I used the following comparison operators:

* `>=` means greater than or equal to.
* `<` means less than.
* `==` checks whether two values are equal.

## Combining user input and conditions

I changed the age program so that the user could enter their own age:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        int age;

        System.out.print("Enter your age: ");
        age = scanner.nextInt();

        if (age >= 65) {
            System.out.println("You are a senior!");
        } else if (age >= 18) {
            System.out.println("You are an adult!");
        } else if (age < 0) {
            System.out.println("You haven't been born yet!");
        } else if (age == 0) {
            System.out.println("You are a baby!");
        } else {
            System.out.println("You are a child!");
        }

        scanner.close();
    }
}
```

The output now depends on the value entered by the user.

## Checking an empty String

I learned how to check whether the user entered a name by using `isEmpty()`:

```java
if (name.isEmpty()) {
    System.out.println("You didn't enter your name!");
} else {
    System.out.println("Hello " + name + "!");
}
```

`name.isEmpty()` returns `true` when the `String` contains no characters.

## Using a boolean in an if statement

I also used a boolean variable to check whether the user is a student:

```java
if (isStudent) {
    System.out.println("You are a student!");
} else {
    System.out.println("You are NOT a student!");
}
```

Because `isStudent` already contains either `true` or `false`, I can use it directly as the condition.

## Final program with multiple condition groups

At the end, I created a program that asks the user for their name, age and student status.

The program uses three separate groups of conditions:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        String name;
        int age;
        boolean isStudent;

        System.out.print("Enter your name: ");
        name = scanner.nextLine();

        System.out.print("Enter your age: ");
        age = scanner.nextInt();

        System.out.print("Are you a student (true/false): ");
        isStudent = scanner.nextBoolean();

        // GROUP 1
        if (name.isEmpty()) {
            System.out.println("You didn't enter your name!");
        } else {
            System.out.println("Hello " + name + "!");
        }

        // GROUP 2
        if (age >= 65) {
            System.out.println("You are a senior!");
        } else if (age >= 18) {
            System.out.println("You are an adult!");
        } else if (age < 0) {
            System.out.println("You haven't been born yet!");
        } else if (age == 0) {
            System.out.println("You are a baby!");
        } else {
            System.out.println("You are a child!");
        }

        // GROUP 3
        if (isStudent) {
            System.out.println("You are a student!");
        } else {
            System.out.println("You are NOT a student!");
        }

        scanner.close();
    }
}
```

Today, I improved my understanding of calculations and conditions in Java. I learned how Java performs arithmetic, how data types affect division and how conditions can control which parts of a program are executed.

I also combined several concepts from previous lessons, including variables, user input, calculations, booleans and console output. My programs are becoming more interactive and can now make decisions based on the information entered by the user.


## Coding challenge: Loan repayment schedule

I also completed a coding challenge in Python that calculates the remaining balance of a loan after each monthly payment.

The function receives:

* The original loan amount
* The annual interest rate as a percentage
* The fixed monthly payment

The returned list starts with the original loan amount. For each month, the program calculates the interest on the current remaining balance, subtracts the monthly payment and stores the new balance.

The monthly interest rate is calculated with:

```text
(annual interest rate / 100) / 12
```

For example, an annual interest rate of `12%` produces a monthly interest rate of:

```text
(12 / 100) / 12 = 0.01
```

This means that the monthly interest rate is `1%`.

For a loan balance of `$1,000`, the interest for the first month would be:

```text
1000 × 0.01 = 10
```

After subtracting a monthly payment of `$300`, the new balance would be:

```text
1000 + 10 - 300 = 710
```

The function continues this calculation until the loan has been completely paid off.

My completed function looked like this:

```python
def get_loan_schedule(loan_amount, annual_rate, monthly_payment):

    payments = [loan_amount]

    while loan_amount > 0:
        monthly_interest = loan_amount * ((annual_rate / 100) / 12)
        new_loan_amount = loan_amount + monthly_interest - monthly_payment

        if new_loan_amount <= 0:
            payments.append(0)
            break
        else:
            payments.append(round(new_loan_amount))
            loan_amount = new_loan_amount

    return payments
```

While solving this challenge, I learned that writing a calculation is not enough by itself. The result must also be assigned to a variable so that it can be used during the next loop iteration.

I also learned that:

* The interest must be recalculated every month.
* The calculation must use the current remaining balance instead of the original loan amount.
* A list can be used to store every balance.
* The original loan amount must be the first value in the list.
* A `while` loop can repeat the calculation until the balance reaches zero.
* The final balance must be exactly `0` and not a negative number.
* `round()` can be used to store each remaining balance as a whole dollar amount.
* A `break` statement can stop a loop when the loan has been paid off.

One important part of the challenge was checking the newly calculated balance instead of the previous balance. At the beginning of every loop iteration, the previous balance is still greater than zero because that is required for the loop to continue.

This challenge helped me understand how calculations, variables, lists, conditions and loops work together. It also showed me how a program can repeatedly update a value and use the updated result in the next calculation.

