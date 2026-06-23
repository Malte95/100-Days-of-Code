Today I continued the development of the Aircraft Route Planner project and implemented the first graph traversal algorithm.

### The Goal:

Provide the ability to determine whether a route exists between two Airbus locations, even when they are not directly connected.

A valid solution must meet these requirements:

* Validate that both locations exist.
* Search through the network automatically.
* Prevent infinite loops caused by bidirectional connections.
* Return a clear result when a route exists.
* Return a clear result when no route exists.

### My Approach:

**1. Reviewed the Graph Structure**

I revisited the graph architecture and analyzed how locations and route connections are stored inside the adjacency list.

This helped me understand how a graph traversal algorithm can move from one location to another by following neighboring connections.

**2. Designed the Route Search Interface**

I introduced a new method:

```python
route_exists(start, destination)
```

The method accepts a start location and a destination location and checks whether a path exists between them.

**3. Implemented Location Validation**

Before starting the search, the graph verifies that both locations exist.

If one or both locations are missing, the method immediately returns an error message instead of attempting an invalid search.

**4. Implemented a Queue-Based Search Strategy**

I implemented a Breadth-First Search (BFS) approach.

The search starts at the origin location and explores neighboring locations one level at a time.

A queue is used to keep track of locations that still need to be explored.

This allows the algorithm to systematically search the entire network.

**5. Implemented Visited Location Tracking**

Because the graph stores bidirectional connections, locations can reference each other.

Without additional protection, the algorithm could repeatedly move back and forth between the same locations.

To prevent this, I introduced a `visited` list that stores all previously explored locations.

Only unvisited neighbors are added to the search queue.

**6. Implemented Route Detection**

Whenever a location is removed from the queue, the algorithm checks whether it matches the destination.

If the destination is found, the search immediately returns:

```text
Route exists.
```

This allows the algorithm to stop as soon as a valid path has been discovered.

**7. Implemented Failure Handling**

If the queue becomes empty before the destination is found, the algorithm concludes that no valid route exists.

In that case, the method returns:

```text
Route does not exist.
```

This ensures that every search request produces a meaningful result.

**8. Tested the BFS Implementation**

I tested the algorithm using connected and disconnected Airbus locations.

Example:

```text
Hamburg-Finkenwerder → Toulouse
```

Result:

```text
Route exists.
```

Example:

```text
Hamburg-Finkenwerder → Mobile
```

Result:

```text
Route does not exist.
```

The tests confirmed that the BFS implementation correctly explores the graph and identifies valid routes.

### Current Project Status:

The Aircraft Route Planner can now:

* Create Airbus locations
* Store locations inside a graph
* Create bidirectional route connections
* Prevent duplicate locations
* Prevent duplicate connections
* Display all available locations
* Display neighboring locations with route distances
* Search the network using Breadth-First Search (BFS)
* Determine whether a route exists between two locations

The project is now ready for the next major milestone:

* Shortest-path calculations using Dijkstra's Algorithm
* Route reconstruction
* Interactive console menu
* Graphical user interface (GUI)

