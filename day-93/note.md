# Daily Coding Challenge: Magic Square Solver

Today, I completed a Python coding challenge about finding the missing number in a 3x3 magic square.

## The Challenge

The function receives a 3x3 grid containing eight numbers and one missing number.

The missing number is represented by `0`.

A magic square is a grid in which:

* every row has the same sum
* every column has the same sum
* both diagonals have the same sum

The function must calculate the missing number and return it if the completed grid is a valid magic square.

If no number can make all rows, columns, and diagonals equal, the function must return:

```python
"impossible"
```

For example:

```python
grid = [
    [2, 7, 6],
    [9, 0, 1],
    [4, 3, 8]
]
```

The complete first row has the sum:

```text
2 + 7 + 6 = 15
```

The complete third row also has the sum:

```text
4 + 3 + 8 = 15
```

Therefore, the target sum of the magic square is `15`.

The incomplete middle row currently has the sum:

```text
9 + 0 + 1 = 10
```

To reach the target sum of `15`, the missing number must be:

```text
15 - 10 = 5
```

After replacing the `0` with `5`, the grid becomes:

```python
[
    [2, 7, 6],
    [9, 5, 1],
    [4, 3, 8]
]
```

Every row, column, and diagonal now has the sum `15`, so the function returns:

```python
5
```

However, calculating a possible missing number is not enough.

For example:

```python
grid = [
    [12, 17, 16],
    [19, 0, 10],
    [14, 13, 18]
]
```

The first row has the sum `45`, so the calculated missing number would be:

```text
45 - 29 = 16
```

This makes every row equal to `45`.

However, the columns and diagonals do not all have the same sum. Therefore, the grid is not a valid magic square, and the function must return:

```python
"impossible"
```

## My Approach

First, I created a copy of the grid:

```python
grid = [row[:] for row in grid]
```

This prevents the function from changing the original grid that was passed into it.

Next, I created two variables for the position of the missing number:

```python
zero_row = None
zero_column = None
```

The missing number has both a row position and a column position.

I then used two nested `for` loops to go through every cell in the grid:

```python
for row_index, row in enumerate(grid):
    for column_index, cell in enumerate(row):
```

The outer loop goes through the rows.

The inner loop goes through the individual cells inside each row.

Using `enumerate()` gives me both the value and its index.

The following variables are available during the loops:

| Variable       | Meaning                          |
| -------------- | -------------------------------- |
| `row_index`    | Index of the current row         |
| `row`          | Current row                      |
| `column_index` | Index of the current column      |
| `cell`         | Value stored in the current cell |

I checked whether the current cell contained `0`:

```python
if cell == 0:
```

When the `0` was found, I saved its row and column indexes:

```python
zero_row = row_index
zero_column = column_index
```

Next, I needed to determine the target sum of the magic square.

Because only one row contains the missing number, the other two rows are complete.

I went through the rows and selected the first row whose index was different from `zero_row`:

```python
for row_index, row in enumerate(grid):
    if row_index != zero_row:
        target_sum = sum(row)
        break
```

The `break` statement stops the loop after the first complete row has been found.

The sum of this complete row becomes the target sum.

Next, I calculated the missing number.

The sum of the row containing the `0` can be calculated with:

```python
sum(grid[zero_row])
```

Because adding zero does not change a sum, this gives me the total of the two known numbers.

I subtracted this value from the target sum:

```python
missing_number = target_sum - sum(grid[zero_row])
```

I then placed the calculated number into the grid:

```python
grid[zero_row][zero_column] = missing_number
```

At this point, the grid was complete.

However, I still needed to verify whether it was actually a valid magic square.

I created an empty list for the row sums:

```python
row_sums = []
```

I then went through every row and added its sum to the list:

```python
for row in grid:
    row_sums.append(sum(row))
```

For example, the result could be:

```python
[15, 15, 15]
```

Next, I calculated the column sums.

I created an empty list:

```python
column_sums = []
```

A 3x3 grid has the column indexes:

```text
0, 1, 2
```

I used `range(3)` to visit these three column indexes:

```python
for column_index in range(3):
```

At the beginning of each column, I created a variable starting at zero:

```python
column_sum = 0
```

I then went through all three rows while keeping the same column index:

```python
for row_index in range(3):
    column_sum += grid[row_index][column_index]
```

For the first column, Python accesses:

```text
grid[0][0]
grid[1][0]
grid[2][0]
```

For the second column, it accesses:

```text
grid[0][1]
grid[1][1]
grid[2][1]
```

For the third column, it accesses:

```text
grid[0][2]
grid[1][2]
grid[2][2]
```

After calculating one complete column, I added its sum to the list:

```python
column_sums.append(column_sum)
```

Next, I calculated the two diagonal sums.

I created two variables:

```python
diagonal_1 = 0
diagonal_2 = 0
```

The first diagonal goes from the top-left corner to the bottom-right corner:

```text
grid[0][0]
grid[1][1]
grid[2][2]
```

The row and column indexes are identical, so I accessed the values with:

```python
grid[index][index]
```

The second diagonal goes from the top-right corner to the bottom-left corner:

```text
grid[0][2]
grid[1][1]
grid[2][0]
```

When the row index increases, the column index decreases.

Because the final column index is `2`, I calculated the column position with:

```python
2 - index
```

Both diagonal sums were calculated inside one loop:

```python
for index in range(3):
    diagonal_1 += grid[index][index]
    diagonal_2 += grid[index][2 - index]
```

I then combined all eight sums into one list:

```python
all_sums = row_sums + column_sums + [diagonal_1, diagonal_2]
```

This list contains:

* three row sums
* three column sums
* two diagonal sums

Finally, I used `all()` to check whether every sum was equal to the first sum in the list:

```python
if all(current_sum == all_sums[0] for current_sum in all_sums):
```

If every sum was equal, the completed grid was a valid magic square, so I returned the missing number:

```python
return missing_number
```

Otherwise, I returned:

```python
return "impossible"
```

## My Solution

```python
def solve_magic_square(grid):
    grid = [row[:] for row in grid]

    zero_row = None
    zero_column = None

    for row_index, row in enumerate(grid):
        for column_index, cell in enumerate(row):
            if cell == 0:
                zero_row = row_index
                zero_column = column_index

    target_sum = None

    for row_index, row in enumerate(grid):
        if row_index != zero_row:
            target_sum = sum(row)
            break

    missing_number = target_sum - sum(grid[zero_row])
    grid[zero_row][zero_column] = missing_number

    row_sums = []

    for row in grid:
        row_sums.append(sum(row))

    column_sums = []

    for column_index in range(3):
        column_sum = 0

        for row_index in range(3):
            column_sum += grid[row_index][column_index]

        column_sums.append(column_sum)

    diagonal_1 = 0
    diagonal_2 = 0

    for index in range(3):
        diagonal_1 += grid[index][index]
        diagonal_2 += grid[index][2 - index]

    all_sums = row_sums + column_sums + [diagonal_1, diagonal_2]

    if all(current_sum == all_sums[0] for current_sum in all_sums):
        return missing_number

    return "impossible"
```

## What I Learned

During this challenge, I practiced working with:

* nested lists
* nested `for` loops
* the `enumerate()` function
* row and column indexes
* the `range()` function
* the `sum()` function
* copying nested lists
* finding a specific value inside a grid
* calculating row sums
* calculating column sums
* calculating diagonal sums
* storing values inside lists
* the `append()` method
* the `break` statement
* the `all()` function
* comparison expressions
* validating a calculated result

The biggest challenge was understanding how to access every row, column, and diagonal in the grid.

Rows were the easiest part because each inner list already represents one complete row:

```python
for row in grid:
    sum(row)
```

Columns were more difficult because they are not stored as separate lists.

To calculate a column, I had to keep the column index the same while changing the row index:

```python
grid[row_index][column_index]
```

This helped me better understand how two-dimensional list indexes work.

The first index selects the row, and the second index selects the column:

```text
grid[row][column]
```

I also learned how diagonal indexes follow patterns.

For the first diagonal, the row and column indexes are the same:

```text
[0][0]
[1][1]
[2][2]
```

For the second diagonal, the row index increases while the column index decreases:

```text
[0][2]
[1][1]
[2][0]
```

This can be represented with:

```python
grid[index][2 - index]
```

Another important lesson was that calculating the missing number does not prove that the square is valid.

A calculated number may make all rows equal while the columns or diagonals still have different sums.

Therefore, I had to validate all eight lines after inserting the missing number.

I also learned that values calculated before changing the grid become outdated.

The row, column, and diagonal sums must be calculated after the missing number has been inserted. Otherwise, the sums still include the original `0`.

The `all()` function was useful for checking the final result:

```python
all(current_sum == all_sums[0] for current_sum in all_sums)
```

This checks whether every value inside `all_sums` is equal to the first value.

If even one sum is different, `all()` returns `False`, and the function returns `"impossible"`.

Overall, this was a challenging exercise because it combined several concepts at once.

It improved my understanding of nested loops, two-dimensional indexes, grid traversal, row and column calculations, diagonal patterns, result validation, and working with nested lists in Python.

