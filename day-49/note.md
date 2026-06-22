Today I continued the development of the Aircraft Route Planner project and implemented neighbor visualization functionality for the graph network.

### The Goal:

Provide users with the ability to inspect direct route connections between Airbus locations while continuing to build the foundation required for future graph traversal algorithms.

A valid solution must meet these requirements:

* Validate requested locations.
* Retrieve neighboring locations from the graph.
* Display route distances.
* Generate readable output for users.
* Prepare the project for future BFS and Dijkstra implementations.

### My Approach:

**1. Reviewed the Adjacency List Structure**

I revisited the graph architecture and analyzed how neighboring locations and route distances are stored within the adjacency list.

The adjacency list stores:

* Neighbor locations as dictionary keys
* Route distances as dictionary values

This structure is well suited for graph traversal algorithms.

**2. Designed the Neighbor Display Feature**

I defined the requirements for a new `show_neighbors()` method.

The method accepts a location name and returns all directly connected locations together with their route distances.

**3. Implemented Location Validation**

Before retrieving neighbors, the graph now verifies that the requested location exists.

If the location cannot be found, the method returns an appropriate error message instead of attempting to access invalid data.

**4. Accessed Neighbor Information Through the Adjacency List**

I implemented logic that retrieves the neighbor dictionary associated with a specific location.

This reinforces the graph architecture and mirrors the access pattern that future traversal algorithms will use.

**5. Learned and Applied Dictionary Iteration**

I explored the difference between:

* `keys()`
* `values()`
* `items()`

The final implementation uses `items()` to access both the neighboring location name and the route distance simultaneously.

**6. Implemented Dynamic Output Generation**

I created a list-based formatting approach that builds output dynamically for any number of neighbors.

Each route is formatted as:

`Location Name (Distance km)`

This allows the method to scale automatically as the network grows.

**7. Implemented User-Friendly Output Formatting**

The final output includes a descriptive header and a clean list of neighboring locations, improving readability and usability.

Example output:

Neighbors of Hamburg-Finkenwerder

Toulouse (1272 km)
Bremen (90 km)

### Current Project Status:

The Aircraft Route Planner can now:

* Create locations
* Store locations inside a graph
* Create route connections
* Prevent duplicate locations
* Prevent duplicate connections
* Display all available locations
* Display neighboring locations with route distances

The project is now ready for the next major milestone:

* Route existence checks using Breadth-First Search (BFS)
* Graph traversal
* Shortest-path calculations using Dijkstra's Algorithm
* User interface development
