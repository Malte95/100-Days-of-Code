# Today I completed the following Python programming task:

# Bucket Fill

## The Goal

Develop a Python function called `bucket_fill(grid, pos, new_value)` that replaces a starting cell and all connected cells with the same value.

A valid solution must meet these requirements:

* Receive a 2D grid.
* Receive a starting position in the format `[row, col]`.
* Receive a new value.
* Find the value at the starting position.
* Replace the starting cell and all connected cells with the same original value.
* Only treat cells as connected if they touch horizontally or vertically.
* Do not treat diagonal cells as connected.
* Return the updated grid.

For example:

```python
bucket_fill([["R", "G"], ["R", "G"]], [0, 1], "B")
```

should return:

```python
[["R", "B"], ["R", "B"]]
```

# My Approach

## 1. Understood the Starting Position

The function receives a position called `pos`.

This position contains two numbers:

```python
[row, col]
```

The first number represents the row.

The second number represents the column.

For example:

```python
pos = [1, 2]
```

means:

```python
row = 1
col = 2
```

This allows the function to find the correct starting cell in the grid.

## 2. Found the Original Value

After finding the row and column, I used them to get the value at the starting position.

```python
old_value = grid[row][col]
```

This value is important because the function must only replace cells that have the same original value as the starting cell.

For example:

```text
Y G G
Y Y Y
B Y R
```

If the starting position contains `Y`, the function should follow the connected `Y` cells.

It should not replace every value in the grid.

## 3. Checked the Special Case

I checked whether the old value is already the same as the new value.

For example:

```python
old_value = "B"
new_value = "B"
```

If both values are the same, the function can immediately return the grid.

This is important because otherwise the function could repeatedly visit the same cells.

## 4. Created a List of Positions to Check

I created a list called `to_check`.

At the beginning, this list contains only the starting position.

```python
to_check = [pos]
```

This list keeps track of all positions that still need to be checked.

## 5. Used a While Loop

I used a `while` loop to continue working while there are still positions in `to_check`.

Inside the loop, I removed one position from the list.

```python
current_pos = to_check.pop()
```

Then I separated the position into a row and column.

```python
row = current_pos[0]
col = current_pos[1]
```

This allows the function to move through the grid step by step.

## 6. Checked Whether the Cell Has the Original Value

Before changing a cell, I checked whether it still has the same value as `old_value`.

If the current cell has a different value, the function skips it.

This is important because neighboring cells may contain other values.

For example:

```text
Y G
Y Y
```

If the function starts on a `Y`, it should not change the `G`.

## 7. Replaced the Current Cell

When the current cell has the original value, I replaced that cell with `new_value`.

The function changes one matching cell at a time.

For example:

```text
Y
```

can become:

```text
B
```

## 8. Checked the Four Possible Neighbors

For every matching cell, I checked the four possible directions.

Above:

```python
[row - 1, col]
```

Below:

```python
[row + 1, col]
```

Left:

```python
[row, col - 1]
```

Right:

```python
[row, col + 1]
```

These are the only directions allowed in this task.

Diagonal cells do not count as connected.

## 9. Checked the Grid Boundaries

Before adding a neighbor to `to_check`, I checked whether the neighbor exists inside the grid.

For example:

* A cell above the first row does not exist.
* A cell below the last row does not exist.
* A cell left of the first column does not exist.
* A cell right of the last column does not exist.

This prevents errors from trying to access positions outside the grid.

## 10. Used a General Solution

The final function does not depend on specific letters such as `Y`, `B`, or `G`.

It also does not depend on one specific grid size.

Instead, it always follows the same general process:

1. Start at the given position.
2. Find the original value.
3. Add the starting position to the list of positions to check.
4. Take one position from the list.
5. Replace the value if it matches the original value.
6. Add valid neighbors to the list.
7. Continue until there are no positions left to check.

This makes the solution work for different grids, different values, different starting positions, and different connected shapes.
