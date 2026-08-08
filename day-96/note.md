# Daily Coding Challenge: Emoji Translator

Today, I completed a Python coding challenge about translating emojis into words.

## The Challenge

The function receives a string containing one or more emojis.

Each emoji represents a specific word according to the following table:

| Emoji | Word      |
| ----- | --------- |
| 👶    | `"baby"`  |
| 🐱    | `"cat"`   |
| 🐕    | `"dog"`   |
| 🐟    | `"fish"`  |
| 🥵    | `"hot"`   |
| 🧊    | `"ice"`   |
| 🪨    | `"rock"`  |
| 🦈    | `"shark"` |
| 🍲    | `"soup"`  |
| ⭐     | `"star"`  |

The function must translate every emoji into its corresponding word and return the result as a string.

The words must be separated by spaces.

For example:

```text
🪨⭐
```

should return:

```text
rock star
```

Another example:

```text
🧊🧊👶
```

should return:

```text
ice ice baby
```

The function also needs to work with different combinations of emojis, such as:

```text
🥵🐕
```

which becomes:

```text
hot dog
```

## My Approach

First, I created a dictionary called `emojis`.

The dictionary stores each emoji as a key and the corresponding word as its value:

```python
emojis = {
    "👶": "baby",
    "🐱": "cat",
    "🐕": "dog",
    "🐟": "fish",
    "🥵": "hot",
    "🧊": "ice",
    "🪨": "rock",
    "🦈": "shark",
    "🍲": "soup",
    "⭐": "star"
}
```

Then, I created an empty list called `words`.

```python
words = []
```

This list is used to collect the translated words.

Next, I used a `for` loop to go through every emoji in the input string:

```python
for emoji in s:
```

Because Python can iterate through the characters of a string, the variable `emoji` represents one emoji during each loop iteration.

For example, if the input is:

```text
🧊🧊👶
```

the loop processes:

```text
🧊
🧊
👶
```

one after another.

Inside the loop, I used the current emoji as a key to access its corresponding word from the dictionary:

```python
emojis[emoji]
```

For example:

```python
emojis["🧊"]
```

returns:

```text
ice
```

I then added each translated word to the `words` list using `.append()`:

```python
words.append(emojis[emoji])
```

After the loop finishes, the list might look like this:

```python
["ice", "ice", "baby"]
```

Finally, I used the `.join()` method to combine all words into one string:

```python
" ".join(words)
```

The string `" "` represents the separator between the words.

This transforms:

```python
["ice", "ice", "baby"]
```

into:

```text
ice ice baby
```

## My Solution

```python
def get_emoji_phrase(s):
    emojis = {
        "👶": "baby",
        "🐱": "cat",
        "🐕": "dog",
        "🐟": "fish",
        "🥵": "hot",
        "🧊": "ice",
        "🪨": "rock",
        "🦈": "shark",
        "🍲": "soup",
        "⭐": "star"
    }

    words = []

    for emoji in s:
        words.append(emojis[emoji])

    return " ".join(words)
```

## What I Learned

During this challenge, I practiced working with:

* Python dictionaries
* dictionary keys and values
* `for` loops
* iterating through strings
* accessing dictionary values with square brackets
* lists
* the `.append()` method
* the `.join()` method
* building a new string from multiple values

One important thing I learned was that Python can iterate directly through a string.

In this case:

```python
for emoji in s:
```

takes one emoji from the input string during every loop iteration.

I also learned how useful dictionaries are when there is a direct relationship between two values.

For example:

```python
"🪨": "rock"
```

means that I can use the emoji as a key and immediately access the corresponding word:

```python
emojis["🪨"]
```

which returns:

```text
rock
```

Another important part was understanding why I needed a list.

Instead of immediately trying to build the final string, I first collected all translated words inside `words`.

For example:

```python
["rock", "star"]
```

Afterwards, I used:

```python
" ".join(words)
```

to combine the list elements into one properly formatted string:

```text
rock star
```

I also improved the readability of my code by using descriptive variable names.

Instead of using a variable such as `i` inside the loop, I used:

```python
emoji
```

This makes it immediately clear what the variable represents.

The solution is also efficient because the function only needs to go through the input string once. Each emoji is translated and added to the list during a single loop iteration.

Overall, this was a useful exercise for improving my understanding of dictionaries, loops, lists, string iteration, dictionary lookups, `.append()`, and `.join()` in Python.

