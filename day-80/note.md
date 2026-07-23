# My Java Learning Progress Today ☕

Today, I continued working through my Java tutorial. The main topic was **user input with the Scanner class**. I also used user input to create a rectangle area calculator and a small Mad Libs game.

## What I learned

* Importing the `Scanner` class
* Creating a `Scanner` object
* Reading text with `nextLine()`
* Reading whole numbers with `nextInt()`
* Reading decimal numbers with `nextDouble()`
* Reading boolean values with `nextBoolean()`
* Storing user input inside variables
* Using user input in calculations
* Using user input inside an `if` and `else` condition
* Closing the Scanner with `scanner.close()`
* Adding a line break with `\n`

## Creating a Scanner

To receive input from the user, I imported the Scanner class and created a Scanner object:

```java
import java.util.Scanner;

Scanner scanner = new Scanner(System.in);
```

`System.in` allows the program to receive input from the keyboard.

At the end of the program, I closed the Scanner:

```java
scanner.close();
```

## User input methods I used

I used different Scanner methods for different data types:

```java
String name = scanner.nextLine();
int age = scanner.nextInt();
double gpa = scanner.nextDouble();
boolean isStudent = scanner.nextBoolean();
```

I learned that:

* `nextLine()` reads a complete line of text.
* `nextInt()` reads a whole number.
* `nextDouble()` reads a decimal number.
* `nextBoolean()` reads either `true` or `false`.

Because my computer uses the German number format, I had to enter decimal numbers with a comma, for example:

```text
3,5
```

Entering `3.5` did not work with my current Scanner settings.

## User information program

I created a program that asks the user for their name, age, GPA and student status:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = scanner.nextLine();

        System.out.print("Enter your age: ");
        int age = scanner.nextInt();

        System.out.print("What is your GPA: ");
        double gpa = scanner.nextDouble();

        System.out.print("Are you a student? (true/false): ");
        boolean isStudent = scanner.nextBoolean();

        System.out.println("Hello " + name);
        System.out.println("You are " + age + " years old");
        System.out.println("Your GPA is: " + gpa);

        if (isStudent) {
            System.out.println("You are enrolled as a student");
        } else {
            System.out.println("You are NOT enrolled as a student");
        }

        scanner.close();
    }
}
```

This exercise helped me combine user input, variables, console output and conditions.

## Rectangle area calculator

I also created a small calculator that asks the user for the width and height of a rectangle.

The program calculates the area by multiplying the width by the height:

```java
area = width * height;
```

My finished program looked like this:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        // Calculate the area of a rectangle

        double width = 0;
        double height = 0;
        double area = 0;

        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter a width: ");
        width = scanner.nextDouble();

        System.out.print("Enter a height: ");
        height = scanner.nextDouble();

        area = width * height;

        System.out.println("The area is: " + area + " cm^2");

        scanner.close();
    }
}
```

This exercise showed me how user input can be used in mathematical calculations.

## Mad Libs game

At the end of the lesson, I created a small Mad Libs game.

The program asks the user to enter several words:

* Three adjectives
* One noun
* One verb ending in `-ing`

The words are then inserted into a short story:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        // MAD LIBS GAME

        Scanner scanner = new Scanner(System.in);

        String adjective1;
        String noun1;
        String adjective2;
        String verb1;
        String adjective3;

        System.out.print("Enter an adjective (description): ");
        adjective1 = scanner.nextLine();

        System.out.print("Enter a noun (animal or person): ");
        noun1 = scanner.nextLine();

        System.out.print("Enter an adjective (description): ");
        adjective2 = scanner.nextLine();

        System.out.print("Enter a verb ending with -ing (action): ");
        verb1 = scanner.nextLine();

        System.out.print("Enter an adjective (description): ");
        adjective3 = scanner.nextLine();

        System.out.println("\nToday I went to a " + adjective1 + " zoo.");
        System.out.println("In an exhibit, I saw a " + noun1 + ".");
        System.out.println(noun1 + " was " + adjective2 + " and " + verb1 + "!");
        System.out.println("I was " + adjective3 + "!");

        scanner.close();
    }
}
```

I used `\n` before the story to add an empty line between the user input and the finished result.

Today, I learned how to make Java programs interactive. Instead of only using values written directly inside the code, my programs can now receive information from the user. I also practiced combining input with variables, calculations, conditions and text output.

