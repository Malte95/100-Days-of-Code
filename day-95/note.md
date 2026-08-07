# My Java Learning Progress Today ☕

Today, I continued learning Java and focused on working with `String` methods and substrings.

I learned how to inspect and modify text using built-in Java methods such as `.length()`, `.charAt()`, `.indexOf()`, `.trim()`, `.replace()`, `.contains()` and `.equals()`.

After that, I learned how to extract specific parts of a `String` using `.substring()`. I combined this with user input and built a small program that separates an email address into a username and a domain.

## What I learned

* Getting the length of a `String`
* Accessing individual characters
* Finding the position of characters inside a `String`
* Finding the last occurrence of a character
* Converting text to uppercase and lowercase
* Removing spaces at the beginning and end of a `String`
* Replacing characters inside a `String`
* Checking whether a `String` is empty
* Checking whether a `String` contains certain characters
* Comparing Strings with `.equals()`
* Extracting parts of a `String` with `.substring()`
* Combining `.substring()` with `.indexOf()`
* Separating an email address into username and domain
* Using `Scanner` together with Strings
* Checking user input before using `.substring()`

## String length

I started by learning how to get the length of a `String` using `.length()`:

```java
String name = "Malte";

int length = name.length();

System.out.println(length);
```

The result is:

```text
5
```

The `.length()` method returns the number of characters inside the `String`.

For `"Malte"`, there are five characters.

## Accessing characters with charAt()

I learned how to access a specific character inside a `String` using `.charAt()`:

```java
String name = "Malte";

char letter = name.charAt(0);

System.out.println(letter);
```

The result is:

```text
M
```

Java starts counting positions at `0`.

This means that the positions in `"Malte"` are:

```text
M a l t e
0 1 2 3 4
```

Because of this, `charAt(0)` returns the first character.

## Finding characters with indexOf()

I used `.indexOf()` to find the position of a character:

```java
String name = "Malte";

int index = name.indexOf("l");

System.out.println(index);
```

The result is:

```text
2
```

The letter `l` is located at index `2`.

`.indexOf()` returns the index of the first occurrence of the specified character or text.

## Finding the last occurrence with lastIndexOf()

I also learned about `.lastIndexOf()`:

```java
String name = "Malte";

int lastIndex = name.lastIndexOf("a");

System.out.println(lastIndex);
```

The result is:

```text
1
```

`.lastIndexOf()` searches for the last occurrence of a character or piece of text inside the `String`.

This becomes especially useful when the same character appears multiple times.

## Converting Strings to uppercase and lowercase

I practiced changing the capitalization of a `String`.

To convert the entire text to uppercase, I used:

```java
String name = "Malte";

name = name.toUpperCase();

System.out.println(name);
```

The result is:

```text
MALTE
```

I can also convert a `String` to lowercase:

```java
String name = "MALTE";

String lowerName = name.toLowerCase();

System.out.println(lowerName);
```

The result is:

```text
malte
```

The methods are:

```java
.toUpperCase()
.toLowerCase()
```

They return a new version of the `String` with the capitalization changed.

## Removing spaces with trim()

I learned how to remove unnecessary spaces from the beginning and end of a `String` using `.trim()`:

```java
String name = "   Malte   ";

name = name.trim();

System.out.println(name);
```

Before using `.trim()`, the `String` contains spaces:

```text
"   Malte   "
```

After using `.trim()`, it becomes:

```text
"Malte"
```

This is useful when working with user input because users may accidentally enter spaces before or after their text.

## Replacing characters

I also practiced `.replace()`:

```java
String name = "Malte";

name = name.replace("a", "o");

System.out.println(name);
```

The result is:

```text
Molte
```

`.replace()` searches for characters or text and replaces them with something else.

The general structure is:

```java
string.replace(oldValue, newValue);
```

## Checking whether a String is empty

I learned how to use `.isEmpty()` inside an `if` statement:

```java
if (name.isEmpty()) {
    System.out.println("Your name is empty");
} else {
    System.out.println("Hello " + name);
}
```

`.isEmpty()` returns a boolean value.

It returns:

```text
true
```

when the `String` contains no characters, and:

```text
false
```

when the `String` contains something.

This makes it useful for validating user input.

## Checking whether a String contains something

I also used `.contains()`:

```java
if (name.contains(" ")) {
    System.out.println("Your name contains a space");
} else {
    System.out.println("Your name DOESN'T contain any spaces");
}
```

`.contains()` checks whether a certain sequence of characters exists inside a `String`.

In this example, I checked whether the name contains a space.

This could be useful for checking names, usernames, email addresses or other user input.

## Comparing Strings with equals()

I learned that Strings can be compared using `.equals()`:

```java
if (name.equals("password")) {
    System.out.println("Your name can't be password");
} else {
    System.out.println("Hello " + name);
}
```

`.equals()` checks whether two Strings contain the same text.

In this example, the program checks whether the entered name is exactly:

```text
password
```

If it is, the program displays an error message.

Otherwise, it greets the user.

## Combining several String methods

I practiced several of these methods together:

```java
String name = "Malte";

int length = name.length();
char letter = name.charAt(0);
int index = name.indexOf("l");
int lastIndex = name.lastIndexOf("a");

System.out.println(length);
System.out.println(letter);
System.out.println(index);
System.out.println(lastIndex);
```

This helped me understand that Java provides many built-in methods for analyzing Strings without having to write the logic myself.

## Substrings

After practicing basic String methods, I started learning about `.substring()`.

A substring is a smaller part extracted from a larger `String`.

The method can be used like this:

```java
.substring(start, end)
```

For example:

```java
String email = "MaxMustermann123@gmail.com";

String username = email.substring(0, 16);

System.out.println(username);
```

This extracts the characters starting at index `0` and ending before index `16`.

An important thing I learned is that the starting index is included, but the ending index is not included.

The general structure is:

```java
string.substring(startIndex, endIndex);
```

## Using substring with only a starting index

I can also use `.substring()` with only one index:

```java
String email = "MaxMustermann123@gmail.com";

String domain = email.substring(17);

System.out.println(domain);
```

When only one index is provided, Java starts at that position and extracts everything until the end of the `String`.

The structure is:

```java
string.substring(startIndex);
```

## Extracting an email username and domain

I first separated an email address using fixed index positions:

```java
String email = "MaxMustermann123@gmail.com";

String username = email.substring(0, 16);
String domain = email.substring(17);

System.out.println(username);
System.out.println(domain);
```

This works for this specific email address.

However, I then improved the program by using `.indexOf("@")` instead of fixed numbers.

## Combining substring() and indexOf()

Instead of manually counting the characters, I used `.indexOf("@")` to automatically find the position of the `@` symbol:

```java
String email = "MaxMustermann123@gmail.com";

String username = email.substring(0, email.indexOf("@"));
String domain = email.substring(email.indexOf("@"));

System.out.println(username);
System.out.println(domain);
```

This is much more flexible because the username can now have different lengths.

For example, this part:

```java
email.indexOf("@")
```

finds the position of the `@` character.

Then:

```java
email.substring(0, email.indexOf("@"));
```

extracts everything before the `@`.

And:

```java
email.substring(email.indexOf("@"));
```

extracts everything starting from the `@` until the end of the email address.

For:

```text
MaxMustermann123@gmail.com
```

the program separates the email into:

```text
MaxMustermann123
@gmail.com
```

This showed me how different String methods can be combined to solve a more useful problem.

## Combining substrings with user input

I then improved the program again by allowing the user to enter their own email address.

I used `Scanner`:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);

        String email;
        String username;
        String domain;

        System.out.print("Enter your email: ");

        email = scanner.nextLine();

        username = email.substring(0, email.indexOf("@"));
        domain = email.substring(email.indexOf("@"));

        System.out.println(username);
        System.out.println(domain);

        scanner.close();
    }
}
```

The user can now enter an email address instead of having it hard-coded inside the program.

This exercise combined several concepts I have already learned:

* Variables
* Strings
* User input
* `Scanner`
* String methods
* Console output

## Validating the email address

Finally, I added an `if` statement to make the email program safer.

Before using `.substring()`, the program checks whether the entered email actually contains an `@` symbol:

```java
if (email.contains("@")) {
    username = email.substring(0, email.indexOf("@"));
    domain = email.substring(email.indexOf("@"));

    System.out.println(username);
    System.out.println(domain);
} else {
    System.out.println("Emails must contain @");
}
```

This is important because the program relies on the position of `@` to separate the email address.

If there is no `@`, `.indexOf("@")` returns `-1`, which would make the substring operation invalid.

By checking:

```java
email.contains("@")
```

first, I can make sure that the expected character exists before processing the `String`.

## Final email program

My final program combined user input, String methods, substrings and an `if` statement:

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {

        // .substring() = A method used to extract a portion of a string
        //                .substring(start, end)

        Scanner scanner = new Scanner(System.in);

        String email;
        String username;
        String domain;

        System.out.print("Enter your email: ");

        email = scanner.nextLine();

        if (email.contains("@")) {
            username = email.substring(0, email.indexOf("@"));
            domain = email.substring(email.indexOf("@"));

            System.out.println(username);
            System.out.println(domain);
        } else {
            System.out.println("Emails must contain @");
        }

        scanner.close();
    }
}
```

Today, I improved my understanding of how Strings work in Java.

I learned that a `String` is not just text that I can store inside a variable. Java provides many useful methods that allow me to inspect, modify, compare and extract information from Strings.

I practiced finding the length of text, accessing individual characters, searching for characters, changing capitalization, removing spaces, replacing text and checking Strings with methods such as `.isEmpty()`, `.contains()` and `.equals()`.

I also learned how `.substring()` can extract specific parts of a `String`. By combining `.substring()` with `.indexOf()`, I was able to separate an email address without relying on fixed character positions.

Finally, I combined String methods with `Scanner` and `if` statements to create a more interactive program that accepts an email address from the user, checks whether it contains an `@` symbol and then separates it into a username and domain.

This showed me how concepts from previous lessons can be combined to create programs that can analyze and process user input instead of only storing and displaying values.

