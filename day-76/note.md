# Today I Completed the Following Python Programming Task

## Elevator Stops

## The Goal

Develop a Python function called `elevator_stops(current_floor, stops)` that determines the order in which an elevator should visit requested floors.

The function receives:

* the elevator’s current floor
* an array of requested floors

The function should return an array containing the floors in the order the elevator should visit them.

The rules are:

* The elevator should travel the minimum possible number of floors.
* Floors must be visited when the elevator first passes them.
* If traveling upward first and downward first result in the same distance, the elevator should go upward first.
* If there are no requested floors, return an empty array.

## The Tests

The function needs to handle cases like:

* an elevator with requested floors both above and below its current position
* an elevator where going downward first is the shortest route
* an elevator where going upward first is the shortest route
* an elevator where all requested floors are above the current floor
* an elevator where all requested floors are below the current floor
* a larger collection of requested floors on both sides of the current floor

For example:

* Starting on floor `5` with requests `[2, 8, 3, 9]` should return `[3, 2, 8, 9]`.
* Starting on floor `6` with requests `[2, 10, 8, 3, 1, 9]` should return `[8, 9, 10, 3, 2, 1]`.
* Starting on floor `1` with requests `[4, 8, 3, 6, 9]` should return `[3, 4, 6, 8, 9]`.
* Starting on floor `12` with requests `[6, 10, 7, 3, 1, 4]` should return `[10, 7, 6, 4, 3, 1]`.
* Starting on floor `11` with requests `[2, 8, 23, 5, 12, 10, 6, 9, 19]` should return `[10, 9, 8, 6, 5, 2, 12, 19, 23]`.

These tests make sure the function correctly compares both possible directions and visits floors in the correct order.

## My Approach

### 1. Handled an Empty Stops Array

First, I checked whether the `stops` array was empty.

If there were no requested floors, the function immediately returned:

```python
[]
```

This avoids running the rest of the logic when the elevator has nowhere to go.

### 2. Divided the Requested Floors Into Two Groups

Next, I separated the requested floors based on their position relative to the elevator’s current floor.

The two groups were:

* floors at or below the current floor
* floors above the current floor

The floors at or below the current floor were stored in the `downs` list.

The floors above the current floor were stored in the `ups` list.

This made it easier to create the two possible elevator routes.

### 3. Sorted the Downward Floors

The downward floors were sorted in descending order.

For example, if the elevator was on floor `11` and the requested lower floors were:

```python
[2, 8, 5, 10, 6, 9]
```

They were sorted as:

```python
[10, 9, 8, 6, 5, 2]
```

This is important because the elevator must visit floors when it first passes them.

When moving downward, it must therefore visit the highest requested floor first and continue toward the lowest one.

### 4. Sorted the Upward Floors

The upward floors were sorted in ascending order.

For example, if the requested upper floors were:

```python
[23, 12, 19]
```

They were sorted as:

```python
[12, 19, 23]
```

When the elevator moves upward, it should visit the closest higher floor first and continue toward the highest requested floor.

### 5. Created a Downward-First Route

After sorting the floors, I created one possible route where the elevator travels downward first.

The route was created by combining:

```python
downs + ups
```

This means the elevator:

1. visits all requested floors below its current position
2. reaches the lowest requested floor
3. changes direction
4. visits all requested floors above its starting position

This route was stored in `path_down_first`.

### 6. Created an Upward-First Route

I also created another possible route where the elevator travels upward first.

The route was created by combining:

```python
ups + downs
```

This means the elevator:

1. visits all requested floors above its current position
2. reaches the highest requested floor
3. changes direction
4. visits all requested floors below its starting position

This route was stored in `path_up_first`.

### 7. Created a Distance Calculation Function

To determine which route was shorter, I created a helper function called `calculate_distance`.

The function starts from the elevator’s current floor.

It then loops through every floor in a possible route.

For each stop, it calculates the distance using:

```python
abs(stop - current)
```

The `abs()` function returns the positive difference between the current position and the next stop.

This distance is added to the total distance.

After that, the current position is updated to the new stop.

The process continues until every requested floor has been visited.

### 8. Calculated the Distance of Both Routes

I used the helper function to calculate the total distance for both possible paths.

The downward-first distance was calculated with:

```python
dist_down = calculate_distance(path_down_first)
```

The upward-first distance was calculated with:

```python
dist_up = calculate_distance(path_up_first)
```

This allowed me to compare the total number of floors traveled for both routes.

### 9. Selected the Shorter Route

After calculating both distances, I compared them.

If the upward-first route was shorter, the function returned `path_up_first`.

If the downward-first route was shorter, the function returned `path_down_first`.

The comparison was:

```python
if dist_up <= dist_down:
```

Using `<=` instead of only `<` also handles the tie-breaking rule.

If both routes have the same total distance, the function returns the upward-first route.

## Why This Solution Works

The solution works because an elevator can minimize its travel distance by choosing one of two main routes:

* travel downward first and then upward
* travel upward first and then downward

While traveling in one direction, the elevator visits every requested floor that it passes.

That is why the downward floors are sorted from highest to lowest and the upward floors are sorted from lowest to highest.

The function creates both valid routes and calculates the exact distance required for each one.

It then returns the route with the smaller total distance.

If both routes require the same distance, the function follows the rule that the elevator should go upward first.

The general process is:

1. Return an empty array if there are no stops.
2. Separate the requested floors into upward and downward floors.
3. Sort the downward floors in descending order.
4. Sort the upward floors in ascending order.
5. Create a downward-first route.
6. Create an upward-first route.
7. Calculate the total distance of both routes.
8. Compare the two distances.
9. Go upward first if the distances are equal.
10. Return the selected route.

This makes the function work for requested floors above the elevator, below the elevator, or on both sides of its current position.

