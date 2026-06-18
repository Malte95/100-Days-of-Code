Today I completed the design and architecture phase of the Aircraft Route Planner project.

The Goal:

Create a well-structured software design before writing any implementation code. The project should simulate a network of Airbus production and engineering sites while providing a practical environment to learn graph data structures and routing algorithms.

A valid solution must meet these requirements:

* Model Airbus locations as nodes in a graph.
* Represent routes between locations as weighted connections.
* Support route analysis between two locations.
* Provide a foundation for BFS, DFS, and Dijkstra's algorithm.
* Follow a clean and maintainable software architecture.
* Remain focused on learning data structures and algorithms rather than external integrations.

My Approach:

1. Defined the Project Scope: I established the primary use case for the application by modeling the workflow of an Airbus logistics planner who needs to analyze routes between Airbus sites.

2. Identified Core Features: I defined the minimum viable product (MVP), including location management, route management, neighbor discovery, route existence checks, and shortest-path calculation.

3. Established Project Boundaries: To keep the project focused and realistic, I explicitly excluded real flight schedules, weather systems, databases, external APIs, maps, and real-time data integration.

4. Designed the Graph Architecture: After evaluating multiple approaches, I selected an undirected weighted graph because routes between Airbus sites should be traversable in both directions and distances must be stored for route optimization.

5. Designed the Object Model: I created a Location class responsible for storing site information such as name, country, and site type. A separate Graph class was chosen to manage the network structure and all routing relationships.

6. Selected the Adjacency List Data Structure: I decided to represent the network using an adjacency list because it provides efficient graph traversal and serves as an ideal foundation for BFS, DFS, and Dijkstra implementations.

7. Simplified the Initial Design: During the architecture review process, I evaluated the need for a dedicated Connection class. After analyzing the responsibilities of each component, I removed the Connection class because the adjacency list already stores all route and distance information.

8. Designed the Airbus Network: I selected an initial network consisting of eight Airbus locations:

* Hamburg-Finkenwerder
* Bremen
* Stade
* Toulouse
* Getafe
* Broughton
* Filton
* Mobile

9. Defined the Route Network: I designed a connected route network between all locations and assigned realistic distance values to each connection. Additional routes were introduced to ensure that multiple valid paths exist, making shortest-path algorithms meaningful.

10. Established the Development Roadmap: I created a phased implementation plan that begins with the graph data model and progresses through graph traversal algorithms (BFS and DFS), shortest-path calculations using Dijkstra's algorithm, and an optional future GUI using CustomTkinter.

Current Project Status:

The design phase is complete.

The project architecture, software requirements, graph model, location network, routing structure, and development roadmap have been finalized. The project is now ready to enter the implementation phase, beginning with the Location and Graph classes.
