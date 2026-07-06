# Today I Completed the Following Python Programming Task

## Lowercase Words

## The Goal

Develop a Python function called `get_lowercase_words(s)` that returns only the words that are entirely lowercase.

The lowercase words must:

* stay in their original order
* have one space between each word
* be returned as one string

For example:

```python
get_lowercase_words("hello GOOD world")
```

should return:

```python
"hello world"
```

## The Tests

The function needs to pass the following tests:

```python
get_lowercase_words("hello GOOD world")
# "hello world"
```

```python
get_lowercase_words("these are all lowercase")
# "these are all lowercase"
```

```python
get_lowercase_words("less is NoT more")
# "less is more"
```

```python
get_lowercase_words("DonT eat pizza every OTHER day")
# "eat pizza every day"
```

```python
get_lowercase_words(
    "the Super quick AND snEaky brown fox Leapt anD jumped over aNd AROUND the lazy SloW dog"
)
# "the quick brown fox jumped over the lazy dog"
```

## My Approach

### 1. Split the String into Individual Words

The function receives a string called `s`.

First, I used `split()` to separate the sentence into individual words.

```python
words = s.split()
```

For example:

```python
s = "hello GOOD world"
```

becomes:

```python
["hello", "GOOD", "world"]
```

This allows the function to check every word separately.

### 2. Created an Empty List

Next, I created an empty list called `lowercase`.

```python
lowercase = []
```

This list is used to store only the words that are completely lowercase.

### 3. Checked Every Word with a For Loop

I used a `for` loop to go through every word in the list.

```python
for word in words:
```

For example, the function checks these words one after another:

```python
"hello"
"GOOD"
"world"
```

### 4. Used `islower()` to Check the Words

For each word, I used the `islower()` method.

```python
if word.islower():
```

This checks whether all letters in the word are lowercase.

For example:

```python
"hello".islower()  # True
"world".islower()  # True
"GOOD".islower()   # False
```

Only the words that return `True` should be kept.

### 5. Added Lowercase Words to the List

When a word is entirely lowercase, I added it to the `lowercase` list.

```python
lowercase.append(word)
```

After checking this sentence:

```python
"hello GOOD world"
```

the list becomes:

```python
["hello", "world"]
```

The word `"GOOD"` is not added because it contains uppercase letters.

### 6. Joined the Words with Spaces

At the end, I used `" ".join(lowercase)` to combine the lowercase words.

```python
result = " ".join(lowercase)
```

The space before `.join()` is important.

It makes sure there is one space between each word.

For example:

```python
["hello", "world"]
```

becomes:

```python
"hello world"
```

### 7. Returned the Result

Finally, I returned the finished string.

```python
return result
```

## The Final Function

```python
def get_lowercase_words(s):
    words = s.split()
    lowercase = []

    for word in words:
        if word.islower():
            lowercase.append(word)

    result = " ".join(lowercase)

    return result
```

## Why This Solution Works

The function follows the same general process for every input:

1. Receive a sentence.
2. Split it into words.
3. Check every word with `islower()`.
4. Keep only words that are completely lowercase.
5. Join the remaining words with spaces.
6. Return the final string.

This makes the function work for short sentences, long sentences, mixed uppercase words, and sentences where every word is lowercase.

