Today I expanded the Aircraft Route Planner network and improved the reliability of the shortest path algorithm.

### Objective

The goal was to create a more realistic Airbus production and logistics network while making the route calculation more robust when destinations cannot be reached.

### Progress

#### 1. Expanded the Airbus Network

Five additional Airbus locations were added to the project:

* Bremen
* Stade
* Broughton
* Getafe
* Filton

These locations were integrated into the graph structure and connected through realistic supply chain relationships.

The network now includes:

* Hamburg-Finkenwerder
* Toulouse
* Mobile
* Bremen
* Stade
* Broughton
* Getafe
* Filton

#### 2. Added New Route Connections

Additional transport routes were implemented between Airbus sites to create a more complex network with multiple possible paths.

Examples include:

* Filton ↔ Broughton
* Broughton ↔ Hamburg-Finkenwerder
* Broughton ↔ Toulouse
* Bremen ↔ Hamburg-Finkenwerder
* Stade ↔ Hamburg-Finkenwerder
* Getafe ↔ Toulouse
* Toulouse ↔ Mobile

This allows the shortest path algorithm to evaluate multiple route options instead of following a single linear chain.

#### 3. Improved Error Handling

A previously unhandled edge case was identified when a location existed in the network but had no connections to other sites.

In this situation, the algorithm could attempt to process a non-existent current location, resulting in an error.

The shortest route function was updated to safely detect unreachable destinations and return:

```text
Route does not exist.
```

instead of terminating with an exception.

### Testing

Several route scenarios were tested successfully:

```text
Filton -> Broughton -> Toulouse -> Mobile
Total Distance: 7660 km
```

```text
Hamburg-Finkenwerder -> Toulouse -> Mobile
Total Distance: 7432 km
```

An isolated test location was also added to verify that unreachable routes are handled correctly.

### Current Capabilities

The Aircraft Route Planner can now:

* Create and manage Airbus locations
* Create transport connections between sites
* Display neighboring locations and distances
* Check route availability using Breadth-First Search (BFS)
* Calculate shortest routes using Dijkstra's Algorithm
* Reconstruct complete routes
* Handle unreachable destinations safely

### Next Steps

The final major development phase will focus on building a graphical user interface (GUI) to make the route planner easier to use and interact with.

