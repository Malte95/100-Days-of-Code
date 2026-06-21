Today I continued the development of the Aircraft Route Planner project and expanded the graph functionality beyond basic location management.

### The Goal:

Extend the graph architecture to support route connections between Airbus sites and provide functionality for displaying all available locations in the network.

A valid solution must meet these requirements:

* Support connections between locations.
* Store route distances.
* Prevent duplicate connections.
* Validate that locations exist before creating routes.
* Display all available locations in the graph.
* Maintain compatibility with future BFS, DFS, and Dijkstra implementations.

### My Approach:

**1. Reviewed the Graph Architecture**

I revisited the adjacency-list design and verified how locations and route connections are stored inside the graph structure.

The project now uses:

* `locations` for storing Location objects
* `adjacency_list` for storing route connections and distances

This structure provides a strong foundation for future graph algorithms.

**2. Designed the Connection System**

Before implementation, I analyzed which information is required to create a route connection:

* Start location
* Destination location
* Distance

This design mirrors how real-world transportation and logistics networks are modeled.

**3. Implemented Connection Validation**

I added logic to verify that both locations exist before a connection can be created.

If either location is missing, the system now returns:

```text
One or both locations do not exist.
```

This prevents invalid routes from being added to the graph.

**4. Implemented Duplicate Connection Protection**

I added validation to prevent duplicate connections from being created.

The graph now checks whether a destination already exists within the neighbor list of the start location before adding a new route.

If a duplicate is detected, the system returns:

```text
Connection already exists.
```

**5. Implemented Bidirectional Route Storage**

Because the project uses an undirected graph, connections are automatically stored in both directions.

Example:

```text
Hamburg-Finkenwerder ↔ Toulouse
```

creates entries for:

```text
Hamburg-Finkenwerder → Toulouse
Toulouse → Hamburg-Finkenwerder
```

This ensures that future graph traversal algorithms can correctly navigate the network from either location.

**6. Implemented Connection Success Feedback**

The graph now confirms successful route creation through a dedicated success message:

```text
Connection added successfully.
```

This improves usability and simplifies debugging.

**7. Studied Graph Traversal Foundations**

I explored how future algorithms such as BFS and Dijkstra will access neighboring nodes through the adjacency list.

I learned how dictionary keys represent neighboring locations and how Python's `.keys()` method can be used to retrieve available neighbors from a given node.

**8. Implemented Location Listing**

I created the `show_all_locations()` method.

The method dynamically retrieves all location names from the graph and returns a formatted list of available Airbus sites.

Example output:

```text
Available Locations

Hamburg-Finkenwerder
Toulouse
Mobile
```

**9. Applied Dynamic String Generation**

I used Python's `join()` method together with dictionary keys to generate formatted output without hardcoding any location names.

This allows the system to scale automatically as new locations are added.

### Current Project Status:

The Aircraft Route Planner can now:

* Create Airbus locations
* Store locations inside a graph
* Prevent duplicate locations
* Create route connections
* Prevent duplicate connections
* Validate route creation requests
* Store distances between locations
* Display all available locations

The project is now ready for the next development phase:

* Show neighboring locations
* Route existence checks
* Breadth-First Search (BFS)
* Depth-First Search (DFS)
* Dijkstra shortest-path algorithm

