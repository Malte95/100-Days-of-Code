# Daily Coding Challenge: Morse Code Decoder

Today, I completed a Python coding challenge about decoding Morse code.

## The Challenge

The function receives a Morse code string and returns the decoded English message.

The rules are:

* Letters are separated by **one space**.
* Words are separated by **three spaces**.

Example:

```text
... --- ...   .... . .-.. .--.
```

Output:

```text
SOS HELP
```

## My Approach

First, I created a dictionary that maps each Morse code sequence to its corresponding letter.

Then, I processed the input string in two steps:

1. Split the Morse code into words using three spaces.
2. Split each word into individual Morse code letters.
3. Look up each Morse code sequence in the dictionary.
4. Store the decoded letters in a list.
5. Join the letters and words together to create the final message.

## My Solution

```python
def decode_morse(code):
    morse_code = {
        ".-": "A",
        "-...": "B",
        "-.-.": "C",
        "-..": "D",
        ".": "E",
        "..-.": "F",
        "--.": "G",
        "....": "H",
        "..": "I",
        ".---": "J",
        "-.-": "K",
        ".-..": "L",
        "--": "M",
        "-.": "N",
        "---": "O",
        ".--.": "P",
        "--.-": "Q",
        ".-.": "R",
        "...": "S",
        "-": "T",
        "..-": "U",
        "...-": "V",
        ".--": "W",
        "-..-": "X",
        "-.--": "Y",
        "--..": "Z"
    }

    letters = []

    for word in code.split("   "):
        for char in word.split():
            if char in morse_code:
                letters.append(morse_code[char])

        letters.append(" ")

    return "".join(letters).strip()
```

## What I Learned

During this challenge, I practiced working with:

* Python dictionaries and dictionary lookups
* `split()` with different separators
* nested `for` loops
* lists and `append()`
* joining strings with `join()`
* removing unnecessary whitespace with `strip()`
* correct indentation in Python

The biggest challenge was understanding how to handle letter separators and word separators differently.

Overall, this was a useful exercise for improving my understanding of string processing and data structures in Python.
