Today I implemented the first graph traversal algorithm for the Aircraft Route Planner project.

## Goal

The objective was to determine whether a route exists between two Airbus locations, even when they are not directly connected.

A valid solution needed to:

* Verify that both locations exist.
* Explore the network automatically.
* Avoid infinite loops caused by bidirectional connections.
* Return whether a route exists between two sites.

## Approach

### 1. Designed the Route Search Interface

I introduced a new method:

```python
route_exists(start, destination)
```

The method accepts a start location and a destination location and determines whether a path exists between them.

### 2. Added Location Validation

Before performing any search, the graph verifies that both locations are registered in the network.

If one or both locations are missing, the method immediately returns an error message.

### 3. Implemented a Queue-Based Search

To traverse the graph, I implemented a Breadth-First Search (BFS) approach.

The algorithm begins with the start location inside a queue and explores neighboring locations level by level until either:

* The destination is found.
* No more locations remain to be explored.

### 4. Prevented Infinite Loops

Because the graph stores bidirectional connections, a route such as:

Hamburg ↔ Toulouse

could cause the search to repeatedly move back and forth between the same locations.

To prevent this, I introduced a `visited` list that keeps track of all previously explored locations.

Only unvisited neighbors are added to the search queue.

### 5. Implemented Route Detection

Whenever a location is removed from the queue, the algorithm checks whether it matches the destination.

If the destination is found, the search terminates immediately and returns:

```text
Route exists.
```

### 6. Implemented Failure Handling

If the queue becomes empty before reaching the destination, the search concludes that no valid route exists and returns:

```text
Route does not exist.
```

## Testing

I tested two scenarios:

### Existing Route

```text
Hamburg-Finkenwerder → Toulouse
```

Result:

```text
Route exists.
```

### Non-Existing Route

```text
Hamburg-Finkenwerder → Mobile
```

Result:

```text
Route does not exist.
```

Both tests produced the expected results.

## Current Project Status

The Aircraft Route Planner can now:

* Create Airbus locations
* Store locations in a graph structure
* Create bidirectional route connections
* Display all locations
* Display neighboring locations
* Search the network using Breadth-First Search (BFS)
* Determine whether a route exists between two locations

## Next Steps

The next milestone is implementing Dijkstra's Algorithm to calculate the shortest route between two Airbus sites based on distance.
