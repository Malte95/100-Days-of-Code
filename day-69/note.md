# Today I Completed the Following Python Programming Task

## Word Score

## The Goal

Develop a Python function called `get_word_score(word)` that receives a word and returns its total score.

Every letter has a value based on its position in the alphabet:

| Letter | Value |
| ------ | ----: |
| `A`    |     1 |
| `B`    |     2 |
| `C`    |     3 |
| `...`  | `...` |
| `Z`    |    26 |

Uppercase and lowercase letters have the same value.

For example:

```text
A = 1
B = 2
C = 3
...
Z = 26
```

The score of a word is the sum of the values of all its letters.

## The Tests

The function should correctly handle examples such as:

```python
get_word_score("hi")
# 17
```

The letter values are:

```text
h = 8
i = 9
```

Therefore:

```text
8 + 9 = 17
```

Another example:

```python
get_word_score("hello")
# 52
```

The calculation is:

```text
h = 8
e = 5
l = 12
l = 12
o = 15
```

Therefore:

```text
8 + 5 + 12 + 12 + 15 = 52
```

The remaining tests are:

```python
get_word_score("hippopotamus")
# 169
```

```python
get_word_score("freeCodeCamp")
# 94
```

The last example also shows that uppercase and lowercase letters must be treated equally.

## My Approach

### 1. Created a Variable for the Total Score

I created a variable called `score` and initially set it to `0`.

```python
score = 0
```

This variable stores the total value of all letters in the word.

Every time the loop processes a letter, its value is added to `score`.

### 2. Converted the Word to Lowercase

Uppercase and lowercase letters must have the same value.

For example:

```text
A = 1
a = 1
```

To avoid handling uppercase and lowercase letters separately, I used the `.lower()` method.

```python
word.lower()
```

This converts all uppercase letters in the word to lowercase.

For example:

```python
"freeCodeCamp".lower()
```

becomes:

```text
"freecodecamp"
```

### 3. Iterated Through Every Character

I used a `for` loop to go through every character in the lowercase word.

```python
for char in word.lower():
```

During each iteration, `char` represents one letter.

For example, when the word is:

```text
"hi"
```

the loop processes:

```text
h
i
```

### 4. Used `ord()` to Get the Character Code

Python provides the built-in `ord()` function.

`ord()` returns the Unicode number of a single character.

For example:

```python
ord("a")
# 97
```

```python
ord("b")
# 98
```

```python
ord("c")
# 99
```

The lowercase letters are stored in consecutive order.

This means that the difference between two letter codes can be used to calculate a letter's position in the alphabet.

### 5. Calculated the Letter Value

To calculate the value of a letter, I subtracted the code of `"a"` from the code of the current character.

```python
ord(char) - ord("a")
```

For example, for the letter `"c"`:

```python
ord("c") - ord("a")
```

becomes:

```text
99 - 97 = 2
```

However, Python's calculated position starts at `0`:

```text
a = 0
b = 1
c = 2
```

The challenge requires the values to start at `1`:

```text
a = 1
b = 2
c = 3
```

Therefore, I added `1` to the result.

```python
ord(char) - ord("a") + 1
```

Now the values are correct:

```python
ord("a") - ord("a") + 1
# 1
```

```python
ord("b") - ord("a") + 1
# 2
```

```python
ord("c") - ord("a") + 1
# 3
```

```python
ord("z") - ord("a") + 1
# 26
```

### 6. Added Every Letter Value to the Score

For every character, I added its calculated value to `score`.

```python
score += ord(char) - ord("a") + 1
```

The `+=` operator adds a value to the current value of a variable.

This:

```python
score += letter_value
```

is equivalent to:

```python
score = score + letter_value
```

For the word `"hi"`, the loop works like this:

First character:

```text
char = "h"
```

The value of `"h"` is calculated:

```python
ord("h") - ord("a") + 1
```

```text
104 - 97 + 1 = 8
```

The score becomes:

```text
score = 0 + 8
score = 8
```

Second character:

```text
char = "i"
```

The value of `"i"` is:

```python
ord("i") - ord("a") + 1
```

```text
105 - 97 + 1 = 9
```

The score becomes:

```text
score = 8 + 9
score = 17
```

### 7. Returned the Final Score

After the loop has processed every character, I returned the final value of `score`.

```python
return score
```

## The Final Function

```python
def get_word_score(word):
    score = 0

    for char in word.lower():
        score += ord(char) - ord("a") + 1

    return score
```

## How the Function Processes `"hello"`

The function starts with:

```text
score = 0
```

The first letter is `"h"`:

```text
h = 8
score = 0 + 8
score = 8
```

The second letter is `"e"`:

```text
e = 5
score = 8 + 5
score = 13
```

The third letter is `"l"`:

```text
l = 12
score = 13 + 12
score = 25
```

The fourth letter is another `"l"`:

```text
l = 12
score = 25 + 12
score = 37
```

The final letter is `"o"`:

```text
o = 15
score = 37 + 15
score = 52
```

The function therefore returns:

```python
52
```

## Why This Solution Works

The function converts the word to lowercase so uppercase and lowercase letters are handled in the same way.

It then iterates through every character and uses `ord()` to obtain its Unicode number.

Because the lowercase letters have consecutive Unicode numbers, subtracting the code of `"a"` reveals the character's position relative to `"a"`.

Adding `1` converts the zero-based position into the required alphabet value.

The general process is:

1. Create a variable for the total score.
2. Convert the word to lowercase.
3. Iterate through every character.
4. Get the character's Unicode number with `ord()`.
5. Subtract the Unicode number of `"a"`.
6. Add `1` to get the correct alphabet value.
7. Add the letter value to the total score.
8. Return the final score.

This challenge helped me understand how characters can be represented by numbers, how the `ord()` function works, and how a repeated pattern can replace a long chain of `if` and `elif` statements.

