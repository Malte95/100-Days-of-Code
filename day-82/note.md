# Today I Completed the Following Python Programming Task

## Cell Signal Locator

## The Goal

Develop a Python function called `find_signal(grid)` that receives a two-dimensional grid containing exactly three cell tower readings and determines the exact coordinates `[row, col]` of the hidden mobile phone.

The grid consists of rows and columns. Each cell contains either a `0` (no tower) or a positive integer. A positive integer represents a cell tower and indicates the exact number of steps to the phone, measured in a straight line: horizontal, vertical, or diagonal. 

The function must return the `[row, col]` of the single cell that satisfies the exact distance requirements from all three towers simultaneously. There is always exactly one unique solution.

### How Distance and Directions Work

If a cell tower has a value of `3`, the phone is located exactly 3 steps away from that tower. The search is limited to **8 linear directions** (similar to a Queen's movement in chess):

*   **Horizontal:** Left or right
*   **Vertical:** Up or down
*   **Diagonal:** Top-left, top-right, bottom-left, or bottom-right

Cells that fall outside the boundaries of the grid are invalid and must be ignored.

## The Code

```python
def find_signal(grid):
    # 1. Created a List for Found Towers
    found_towers = []

    # 2. Scanned the Grid Using Nested Loops
    for r in range(len(grid)):
        for c in range(len(grid[r])):
            # 3. Isolated Cells Containing Towers
            if grid[r][c] > 0:
                distance = grid[r][c]
                found_towers.append([r, c, distance])

    # 4. Created a Container for All Possible Coordinates
    all_possible_positions = []

    # 5. Iterated Through the Found Towers
    for tower in found_towers:
        t_r, t_c, d = tower
        tower_positions = []

        # 6. Defined the 8 Geometric Directions
        directions = [
            [t_r, t_c - d], [t_r, t_c + d],
            [t_r - d, t_c], [t_r + d, t_c],
            [t_r - d, t_c - d], [t_r + d, t_c + d],
            [t_r - d, t_c + d], [t_r + d, t_c - d]
        ]

        # 7. Filtered Out Coordinates Beyond Grid Boundaries
        for pos_r, pos_c in directions:
            if 0 <= pos_r < len(grid) and 0 <= pos_c < len(grid[0]):
                tower_positions.append((pos_r, pos_c))
        
        # 8. Grouped Each Tower's Potential Positions
        all_possible_positions.append(tower_positions)

    # 9. Converted Lists to Sets for Fast Comparison
    set1 = set(all_possible_positions[0])
    set2 = set(all_possible_positions[1])
    set3 = set(all_possible_positions[2])

    # 10. Found the Intersection and Returned the Solution
    result_set = set1 & set2 & set3
    result = result_set.pop()

    return [result[0], result[1]]
```

## My Approach

### 1. Created a List for Found Towers
I initialized an empty list called `found_towers` to store the coordinates and distance values of the three active cell towers.

### 2. Scanned the Grid Using Nested Loops
I used two nested `for` loops to iterate through every cell in the grid row by row, and column by column. The outer loop handles the row index `r`, while the inner loop handles the column index `c` within that specific row. Using `len(grid[r])` ensures the function safely handles non-square grids.

### 3. Isolated Cells Containing Towers
Inside the nested loops, I checked whether the value of the current cell was greater than `0`. If a tower is found, its row index `r`, column index `c`, and its `distance` value are saved as a sublist inside `found_towers`.

### 4. Created a Container for All Possible Coordinates
I initialized an empty list called `all_possible_positions` to collect the valid target cells for each individual tower.

### 5. Iterated Through the Found Towers
I used a `for` loop to process each of the three discovered towers one by one. I unpacked the tower's components into `t_r` (tower row), `t_c` (tower column), and `d` (distance). I also created a temporary list `tower_positions` to store the valid coordinates specifically for the current tower.

### 6. Defined the 8 Geometric Directions
For each tower, I mapped out the algebraic formulas for all 8 possible straight-line paths using its row `t_r`, column `t_c`, and distance `d`. This covers horizontal, vertical, and the four diagonal endpoints in a single step.

### 7. Filtered Out Coordinates Beyond Grid Boundaries
I looped through the 8 calculated target coordinates and verified whether they actually resided within the grid boundaries. The condition `0 <= pos_r < len(grid)` ensures the row index is valid. The condition `0 <= pos_c < len(grid[0])` ensures the column index is valid. Valid coordinates are stored as immutable tuples `(pos_r, pos_c)` inside `tower_positions`.

### 8. Grouped Each Tower's Potential Positions
Once all 8 directions for a single tower were checked, its list of valid target cells was appended to the main container. After the loop completes, `all_possible_positions` contains exactly three nested lists—one list of possible coordinates for each tower.

### 9. Converted Lists to Sets for Fast Comparison
To find the single coordinate shared by all three towers, I converted each tower's list of valid positions into a Python `set`. Sets allow for highly efficient comparison operations compared to standard lists.

### 10. Found the Intersection and Returned the Solution
I used the bitwise AND operator (`&`) to find the mathematical intersection of the three sets. The `result_set` contains only the coordinate pairs that appear in all three sets. Because the challenge guarantees exactly one solution, I extracted the element using `.pop()`. Finally, the function unpacks the row and column into a standard list format and returns it.

