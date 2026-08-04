# Daily Coding Challenge: Game Theory

Today, I completed a Python coding challenge about calculating the scores of two players based on their strategies in a game.

## The Challenge

The function receives two strings of equal length representing the strategies of two players.

Each string can only contain the following letters:

| Letter | Meaning   |
| ------ | --------- |
| `C`    | Cooperate |
| `D`    | Defect    |

Each character represents one round of the game.

The characters at the same position in both strings are compared to determine how many points each player receives.

The scoring rules are:

| Player 1 | Player 2 | Player 1 Score | Player 2 Score |
| -------- | -------- | -------------: | -------------: |
| `C`      | `C`      |              3 |              3 |
| `D`      | `D`      |              1 |              1 |
| `C`      | `D`      |              0 |              5 |
| `D`      | `C`      |              5 |              0 |

For example:

```python
p1 = "CCDD"
p2 = "CDDD"
```

The rounds are evaluated individually:

| Round | Player 1 | Player 2 | Scores |
| ----: | -------- | -------- | ------ |
|     1 | `C`      | `C`      | `3, 3` |
|     2 | `C`      | `D`      | `0, 5` |
|     3 | `D`      | `D`      | `1, 1` |
|     4 | `D`      | `D`      | `1, 1` |

The final result is:

```python
[5, 10]
```

The first number represents Player 1’s total score, while the second number represents Player 2’s total score.

## My Approach

First, I created two variables to store the players’ scores:

```python
player1 = 0
player2 = 0
```

Both variables start at zero because neither player has earned any points before the game begins.

Next, I used a `for` loop with `range()` to go through every position in the first strategy string:

```python
for i in range(0, len(p1)):
```

The variable `i` represents the current index.

For example, when the two strings are:

```python
p1 = "CCDD"
p2 = "CDDD"
```

the loop visits the indexes:

```text
0, 1, 2, 3
```

During each loop iteration, I used the same index to access the current strategy of both players:

```python
p1[i]
p2[i]
```

This allows the function to compare the two players’ decisions from the same round.

I then used an `if`, `elif` structure to check all four possible combinations.

If both players cooperate, they each receive three points:

```python
if p1[i] == "C" and p2[i] == "C":
    player1 += 3
    player2 += 3
```

If both players defect, they each receive one point:

```python
elif p1[i] == "D" and p2[i] == "D":
    player1 += 1
    player2 += 1
```

If Player 1 cooperates while Player 2 defects, Player 2 receives five points:

```python
elif p1[i] == "C" and p2[i] == "D":
    player2 += 5
```

If Player 1 defects while Player 2 cooperates, Player 1 receives five points:

```python
elif p1[i] == "D" and p2[i] == "C":
    player1 += 5
```

After every round has been evaluated, I placed both final scores inside a list:

```python
scores = [player1, player2]
```

Finally, I returned the list:

```python
return scores
```

## My Solution

```python
def play_game(p1, p2):
    player1 = 0
    player2 = 0

    for i in range(0, len(p1)):
        if p1[i] == "C" and p2[i] == "C":
            player1 += 3
            player2 += 3
        elif p1[i] == "D" and p2[i] == "D":
            player1 += 1
            player2 += 1
        elif p1[i] == "C" and p2[i] == "D":
            player2 += 5
        elif p1[i] == "D" and p2[i] == "C":
            player1 += 5

    scores = [player1, player2]

    return scores
```

## What I Learned

During this challenge, I practiced working with:

* strings
* string indexes
* the `len()` function
* the `range()` function
* `for` loops
* `if` and `elif` statements
* logical operators such as `and`
* comparison operators
* the `+=` operator
* lists
* returning multiple results inside a list
* accumulating values over multiple loop iterations

The biggest challenge was creating the correct `range()` for the loop.

At first, I tried to include too many values inside `range()` and used zero as the step value.

However, `range()` can only receive up to three values:

```text
range(start, stop, step)
```

The step value also cannot be zero because Python would not know how to move from one number to the next.

Because both strategy strings have the same length, I only needed to loop from zero to the length of one string:

```python
range(0, len(p1))
```

I learned that the stop value is not included. Therefore, if the string contains four characters, the generated indexes are:

```text
0, 1, 2, 3
```

These are exactly the indexes required to access every character in the string.

I also practiced comparing characters from two different strings using the same index:

```python
p1[i]
p2[i]
```

This ensures that the function compares the decisions belonging to the same round.

Another important lesson was understanding score accumulation.

Using:

```python
player1 += 3
```

is equivalent to:

```python
player1 = player1 + 3
```

This keeps the player’s previous score and adds the points from the current round.

I also learned that adding zero is unnecessary.

For example:

```python
player1 += 0
```

does not change the score, so the line can simply be removed. Only the player receiving points needs to be updated.

Overall, this was a useful exercise for improving my understanding of loops, indexes, conditional logic, string comparison, score accumulation, and returning multiple values from a Python function.
