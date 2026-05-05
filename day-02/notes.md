Today I did the Adjacency List to Matrix Converter Lab.
I defined a function called "adjacency_list_to_matrix" 
which takes a dictionary representing a list of an unweighted graph as its argument. 
In the first step I declared a variable called n which stores the length of the dictionary.
Then I created a list variable called matrix.
By using a for-loop I aappended rows to the matrix list, every row contains 0 at this point.
Using another for-loop I iterated over each neighbor in the dictionary and added a 1 
to the matrix if ther´s an edge between the node and the neighbor.
Lastly I printed ever row using yet another for-loop and returned the matrix.


