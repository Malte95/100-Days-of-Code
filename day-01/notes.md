Today I continued with the freeCodeCamp Python Certification. I build a Shortest Path Algorithm.
I implemented a graph algorithm to find the shortest paths between nodes using an adjacency matrix. 
The matrix represents a weighted graph where each value corresponds to the distance between two nodes, 
and "INF" is used to indicate that no direct connection exists.

The function "shortest_path" applies a variation of Dijkstra’s algorithm. I initialize distances, 
track visited nodes, and iteratively select the node with the smallest known distance. 
Then I update the distances to neighboring nodes if a shorter path is found.

Additionally, I store the actual paths taken and print both the shortest distance and the corresponding path from the start node to all other nodes 
(or to a specific target node, if provided).

In summary, today I programmed a shortest path algorithm that calculates and displays optimal routes in a weighted graph.


