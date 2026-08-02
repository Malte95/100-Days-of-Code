# Daily Coding Challenge: Fibonacci Sequence

Today, I completed a Python coding challenge about generating a Fibonacci sequence.

## The Challenge

The function receives an array containing the first two numbers of a Fibonacci sequence and an integer representing the desired length.

It returns an array containing the sequence with exactly that length.

In a Fibonacci sequence, each new number is calculated by adding the two preceding numbers.

For example, when starting with `0` and `1`, the first ten numbers are:

```text
0, 1, 1, 2, 3, 5, 8, 13, 21, 34
```

The function also needs to handle special cases:

* If the length is `0`, return an empty array.
* If the length is `1`, return only the first starting number.
* The starting numbers are already part of the sequence.

## My Approach

First, I handled the special cases for sequence lengths of zero and one.

For longer sequences, I created a new list containing the two starting numbers.

Then, I repeated the following steps until the sequence reached the required length:

1. Access the last two numbers in the current sequence.
2. Add these two numbers together.
3. Append the result to the sequence.
4. Continue until the requested number of elements has been generated.

To access the final two elements of the list, I used negative indexes:

* `sequence[-1]` accesses the last number.
* `sequence[-2]` accesses the second-to-last number.

## My Solution

```python
def fibonacci_sequence(start_sequence, length):
    if length == 0:
        return []
    elif length == 1:
        return [start_sequence[0]]

    sequence = [start_sequence[0], start_sequence[1]]
    i = 1

    while i <= length - len(start_sequence):
        prev_num = sequence[-2]
        next_num = sequence[-1]
        number = prev_num + next_num
        sequence.append(number)
        i += 1

    return sequence
```

## What I Learned

During this challenge, I practiced working with:

* Python lists
* negative list indexes
* `while` loops
* variables and arithmetic operations
* adding elements with `append()`
* handling special cases with `if` and `elif`
* controlling the length of a generated sequence

The biggest challenge was making sure that each new number was calculated using the latest two numbers from the generated sequence.

At first, I used the original starting numbers during every loop iteration. This meant that the same result was calculated repeatedly. I solved this problem by accessing the last two values of the growing sequence with `sequence[-2]` and `sequence[-1]`.

I also needed to handle a requested length of one separately because the initial sequence normally contains two numbers.

Overall, this was a useful exercise for improving my understanding of loops, list indexing, edge cases, and sequence generation in Python.

