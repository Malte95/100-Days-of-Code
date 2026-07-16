# Today I Completed the Following Python Programming Task

## Pig Latin Converter

## The Goal

Develop a Python function called `pig_latin(s)` that receives a string and converts every word into Pig Latin.

The conversion follows three main rules.

### Words Beginning with a Vowel

If a word begins with one of the following vowels:

```text
a
e
i
o
u
```

the function adds `"way"` to the end of the word.

For example:

```text
universe → universeway
```

Another example is:

```text
apple → appleway
```

### Words Beginning with Consonants

If a word begins with one or more consonants, the consonants before the first vowel are moved to the end of the word.

The function then adds `"ay"`.

For example:

```text
hello → ellohay
```

The first consonant is:

```text
h
```

The remaining part of the word is:

```text
ello
```

After moving the consonant to the end:

```text
elloh
```

Finally, `"ay"` is added:

```text
ellohay
```

A word can also begin with several consonants.

For example:

```text
string → ingstray
```

The consonants before the first vowel are:

```text
str
```

The remaining part is:

```text
ing
```

The consonants are moved to the end:

```text
ingstr
```

After adding `"ay"`, the result is:

```text
ingstray
```

### Preserving Capitalization

The function must preserve whether the first letter of the original word was uppercase.

For example:

```text
Hello → Ellohay
```

The original word begins with an uppercase letter, so the translated word must also begin with an uppercase letter.

## The Tests

The function should correctly handle examples such as:

```python
pig_latin("universe")
# "universeway"
```

Because `"universe"` begins with the vowel `"u"`, `"way"` is added to the end.

```text
universe + way = universeway
```

Another example is:

```python
pig_latin("hello")
# "ellohay"
```

The word begins with the consonant `"h"`.

The consonant is moved to the end:

```text
hello → elloh
```

Then `"ay"` is added:

```text
elloh + ay = ellohay
```

The function should also handle words that begin with several consonants:

```python
pig_latin("string")
# "ingstray"
```

The initial consonants are:

```text
str
```

The first vowel is:

```text
i
```

Therefore:

```text
string → ing + str + ay
```

The result is:

```text
ingstray
```

Capitalized words should remain capitalized:

```python
pig_latin("Hello")
# "Ellohay"
```

The function should also process several words in one string:

```python
pig_latin("Hello universe")
# "Ellohay universeway"
```

Each word is translated separately and then added back to the final sentence.

## My Approach

### 1. Created a List of Vowels

I created a list containing the five vowels:

```python
vowls = ["a", "e", "i", "o", "u"]
```

This list is used to check whether a character is a vowel.

For example:

```python
"a" in vowls
# True
```

```python
"h" in vowls
# False
```

The function uses `.lower()` when checking characters, so uppercase vowels are recognized as well.

For example:

```python
"A".lower()
```

becomes:

```text
a
```

Therefore:

```python
"A".lower() in vowls
# True
```

### 2. Checked Whether the String Is Empty

Before processing the string, I checked whether it was empty.

```python
if not s:
    return s
```

An empty string does not contain any words that can be translated.

Therefore, the function immediately returns it.

For example:

```python
pig_latin("")
# ""
```

This also prevents the function from trying to access characters that do not exist.

### 3. Split the String into Individual Words

I used the `.split()` method to divide the input string into words.

```python
words = s.split()
```

For example:

```python
"Hello universe".split()
```

returns:

```python
["Hello", "universe"]
```

This allows the function to translate every word separately.

### 4. Created a List for the Translated Words

I created an empty list called `translated_words`.

```python
translated_words = []
```

Every translated word is added to this list.

For example, after translating:

```text
Hello universe
```

the list will contain:

```python
["Ellohay", "universeway"]
```

At the end of the function, the words in this list are joined together again.

### 5. Iterated Through Every Word

I used a `for` loop to process every word in the string.

```python
for word in words:
```

During each iteration, `word` represents one individual word.

For example, for the string:

```text
Hello universe
```

the loop first processes:

```text
Hello
```

and then:

```text
universe
```

### 6. Checked Whether the First Letter Was Uppercase

Before translating a word, I checked whether its first letter was uppercase.

```python
is_capitalized = word[0].isupper()
```

The `.isupper()` method returns `True` when the character is uppercase.

For example:

```python
"H".isupper()
# True
```

```python
"h".isupper()
# False
```

This information is stored in the variable `is_capitalized`.

The function can then restore the capitalization after translating the word.

### 7. Checked Whether the Word Begins with a Vowel

I checked whether the first character of the word was inside the vowel list.

```python
if word[0].lower() in vowls:
```

The first character is converted to lowercase before the comparison.

This means that both lowercase and uppercase vowels are recognized.

For example:

```python
"u".lower() in vowls
# True
```

```python
"U".lower() in vowls
# True
```

If the word begins with a vowel, I added `"way"` to it.

```python
translated_word = word + "way"
```

For example:

```text
universe + way
```

becomes:

```text
universeway
```

No characters need to be moved because the word already begins with a vowel.

### 8. Searched for the First Vowel

If the word does not begin with a vowel, the function must find the position of its first vowel.

I first created a variable called `vowel_index`.

```python
vowel_index = 0
```

This variable stores the index of the first vowel.

I then used `enumerate()` to iterate through the word.

```python
for i, char in enumerate(word):
```

The `enumerate()` function provides both the index and the character.

For example, when processing `"hello"`, the loop produces:

```text
i = 0, char = "h"
i = 1, char = "e"
i = 2, char = "l"
i = 3, char = "l"
i = 4, char = "o"
```

The function checks every character:

```python
if char.lower() in vowls:
```

When it finds a vowel, it stores its index:

```python
vowel_index = i
```

It then stops the loop using `break`.

```python
break
```

For the word `"hello"`, the first vowel is `"e"`.

Its index is:

```text
1
```

Therefore:

```python
vowel_index = 1
```

For the word `"string"`, the first vowel is `"i"`.

Its index is:

```text
3
```

Therefore:

```python
vowel_index = 3
```

### 9. Handled Words Without Vowels

The `for` loop contains an `else` block:

```python
else:
    vowel_index = len(word)
```

A `for` loop's `else` block runs when the loop finishes without encountering `break`.

In this function, that means no vowel was found.

For example, a word such as:

```text
rhythm
```

does not contain any of the vowels from the list.

The function therefore sets the vowel index to the length of the word:

```python
vowel_index = len(word)
```

For `"rhythm"`:

```python
len("rhythm")
# 6
```

Therefore:

```python
vowel_index = 6
```

This causes the complete word to be treated as the initial consonant section.

### 10. Separated the Initial Consonants from the Rest of the Word

After finding the first vowel, I divided the word into two sections.

The first section contains all characters before the first vowel:

```python
consonants = word[:vowel_index]
```

The second section contains the first vowel and everything after it:

```python
rest_of_word = word[vowel_index:]
```

For the word `"hello"`, the vowel index is `1`.

Therefore:

```python
consonants = word[:1]
```

returns:

```text
h
```

The remaining part is:

```python
rest_of_word = word[1:]
```

which returns:

```text
ello
```

For the word `"string"`, the vowel index is `3`.

The consonants are:

```python
word[:3]
```

```text
str
```

The remaining part is:

```python
word[3:]
```

```text
ing
```

### 11. Constructed the Pig Latin Word

I placed the remaining part of the word first, followed by the initial consonants.

I then added `"ay"`.

```python
translated_word = rest_of_word.lower() + consonants.lower() + "ay"
```

Both parts are converted to lowercase before they are combined.

For `"hello"`:

```text
rest_of_word = "ello"
consonants = "h"
```

The expression becomes:

```python
"ello" + "h" + "ay"
```

The result is:

```text
ellohay
```

For `"string"`:

```text
rest_of_word = "ing"
consonants = "str"
```

The expression becomes:

```python
"ing" + "str" + "ay"
```

The result is:

```text
ingstray
```

### 12. Restored the Capitalization

After translating the word, I checked the value of `is_capitalized`.

```python
if is_capitalized:
```

If the original word began with an uppercase letter, I used `.capitalize()`.

```python
translated_word = translated_word.capitalize()
```

The `.capitalize()` method makes the first character uppercase and the remaining characters lowercase.

For example:

```python
"ellohay".capitalize()
```

returns:

```text
Ellohay
```

Therefore:

```text
Hello → Ellohay
```

If the original word began with a lowercase letter, this step is skipped.

For example:

```text
hello → ellohay
```

### 13. Added the Translated Word to the List

After translating and formatting the word, I added it to `translated_words`.

```python
translated_words.append(translated_word)
```

For example, after processing `"Hello"`, the list contains:

```python
["Ellohay"]
```

After processing `"universe"` as well, it contains:

```python
["Ellohay", "universeway"]
```

### 14. Joined the Words into a String

After every word has been translated, I used the `.join()` method to combine the words.

```python
return " ".join(translated_words)
```

The string `" "` between the quotation marks represents one space.

Therefore:

```python
" ".join(["Ellohay", "universeway"])
```

returns:

```text
Ellohay universeway
```

The completed Pig Latin sentence is then returned by the function.

## The Final Function

```python
def pig_latin(s):
    vowls = ["a", "e", "i", "o", "u"]

    if not s:
        return s

    words = s.split()
    translated_words = []

    for word in words:
        is_capitalized = word[0].isupper()

        if word[0].lower() in vowls:
            translated_word = word + "way"
        else:
            vowel_index = 0

            for i, char in enumerate(word):
                if char.lower() in vowls:
                    vowel_index = i
                    break
            else:
                vowel_index = len(word)

            consonants = word[:vowel_index]
            rest_of_word = word[vowel_index:]

            translated_word = (
                rest_of_word.lower()
                + consonants.lower()
                + "ay"
            )

        if is_capitalized:
            translated_word = translated_word.capitalize()

        translated_words.append(translated_word)

    return " ".join(translated_words)
```

## How the Function Processes `"hello"`

The function receives:

```text
hello
```

It splits the string into a list:

```python
["hello"]
```

The first letter is:

```text
h
```

It is not uppercase:

```python
"h".isupper()
# False
```

It is also not a vowel:

```python
"h" in ["a", "e", "i", "o", "u"]
# False
```

The function searches for the first vowel.

The first character is:

```text
h
```

This is not a vowel.

The second character is:

```text
e
```

This is a vowel, and its index is `1`.

The word is separated into:

```text
consonants = "h"
rest_of_word = "ello"
```

The parts are combined:

```text
"ello" + "h" + "ay"
```

The result is:

```text
ellohay
```

Because the original word was not capitalized, the translated word remains lowercase.

The function returns:

```python
"ellohay"
```

## How the Function Processes `"Hello"`

The function receives:

```text
Hello
```

The first character is uppercase:

```python
"H".isupper()
# True
```

Therefore:

```python
is_capitalized = True
```

The first vowel is `"e"` at index `1`.

The two sections are:

```text
consonants = "H"
rest_of_word = "ello"
```

The translated lowercase word is:

```text
ellohay
```

Because `is_capitalized` is `True`, the function applies `.capitalize()`.

```python
"ellohay".capitalize()
```

The result is:

```text
Ellohay
```

The function returns:

```python
"Ellohay"
```

## How the Function Processes `"string"`

The function receives:

```text
string
```

The word begins with three consonants:

```text
s
t
r
```

The first vowel is:

```text
i
```

Its index is:

```text
3
```

The function separates the word into:

```text
consonants = "str"
rest_of_word = "ing"
```

The translated word is constructed:

```python
"ing" + "str" + "ay"
```

This produces:

```text
ingstray
```

The function returns:

```python
"ingstray"
```

## How the Function Processes `"universe"`

The function receives:

```text
universe
```

The first character is:

```text
u
```

The character `"u"` is a vowel.

Therefore, the consonant-moving logic is not required.

The function simply adds `"way"`:

```python
"universe" + "way"
```

The result is:

```text
universeway
```

The function returns:

```python
"universeway"
```

## How the Function Processes `"Hello universe"`

The original string is:

```text
Hello universe
```

The string is divided into two words:

```python
["Hello", "universe"]
```

The first word is:

```text
Hello
```

It begins with a consonant and is capitalized.

The translated result is:

```text
Ellohay
```

The second word is:

```text
universe
```

It begins with a vowel, so `"way"` is added.

The translated result is:

```text
universeway
```

The translated words list becomes:

```python
["Ellohay", "universeway"]
```

The words are joined with a space:

```python
" ".join(["Ellohay", "universeway"])
```

The final result is:

```text
Ellohay universeway
```

## Why This Solution Works

The function processes each word individually, which allows it to translate complete sentences rather than only single words.

It first checks whether the input is empty. If it is, the original empty string is returned immediately.

For every word, the function remembers whether its first letter was uppercase.

It then checks the first character.

If the word begins with a vowel, `"way"` is added directly to the end.

If the word begins with a consonant, the function searches for the first vowel using `enumerate()`.

The index of the first vowel divides the word into two sections:

```text
initial consonants
remaining part of the word
```

The remaining part is placed first, the initial consonants are moved to the end, and `"ay"` is added.

After the translation, the function restores the capitalization when necessary.

Finally, every translated word is stored in a list, and the words are joined together with spaces.

The general process is:

1. Create a list containing the vowels.
2. Return immediately if the input string is empty.
3. Split the string into individual words.
4. Create a list for the translated words.
5. Iterate through every word.
6. Remember whether the first letter is uppercase.
7. Check whether the word begins with a vowel.
8. Add `"way"` if the word begins with a vowel.
9. Otherwise, find the first vowel.
10. Separate the initial consonants from the rest of the word.
11. Move the consonants to the end.
12. Add `"ay"`.
13. Restore the capitalization.
14. Add the translated word to the result list.
15. Join all translated words with spaces.
16. Return the completed Pig Latin string.

