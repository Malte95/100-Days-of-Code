Today I started implementing Dijkstra's Algorithm for the Aircraft Route Planner project.

### Goal

The objective is to calculate the shortest route between Airbus locations based on distance rather than simply checking whether a route exists.

### Progress

**1. Created the shortest_route() Method**

A new method was added to the Graph class:

```python
shortest_route(start, destination)
```

This method will eventually calculate the shortest path between two locations.

**2. Implemented Distance Tracking**

I introduced a distance dictionary that stores the currently known shortest distance to every location in the graph.

Initially:

* The start location is assigned a distance of 0.
* All other locations are assigned infinity.

Example:

```python
{
    "Hamburg-Finkenwerder": 0,
    "Toulouse": inf,
    "Mobile": inf
}
```

**3. Implemented Current Location Selection**

The algorithm now searches for the unvisited location with the smallest known distance.

During testing, the algorithm correctly selected Hamburg-Finkenwerder as the first location to process.

**4. Implemented Visited Tracking**

A visited list was added to prevent locations from being processed multiple times.

Example:

```python
["Hamburg-Finkenwerder"]
```

**5. Implemented Neighbor Discovery**

The algorithm successfully retrieved neighboring locations from the adjacency list.

Example:

```python
{
    "Toulouse": 1272
}
```

**6. Implemented First Distance Update**

The first distance calculation was successfully completed.

The route:

Hamburg-Finkenwerder → Toulouse

updated the distance dictionary from:

```python
{
    "Hamburg-Finkenwerder": 0,
    "Toulouse": inf,
    "Mobile": inf
}
```

to:

```python
{
    "Hamburg-Finkenwerder": 0,
    "Toulouse": 1272,
    "Mobile": inf
}
```

### Current Status

The algorithm can now:

* Initialize all route distances
* Select the next location to process
* Track visited locations
* Discover neighboring locations
* Update route distances

### Next Steps

The next milestone is to place these operations inside a loop so the algorithm can repeatedly process locations until the shortest route to the destination has been determined.
