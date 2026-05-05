Today I did the Adjacency List to Matrix Converter Lab.
I defined a function called "adjacency_list_to_matrix" 
which takes a dictionary representing a list of an unweighted graph as its argument. 
In the first step I declared a variable called n which stores the length of the dictionary.
Then I created a list variable called matrix.
By using a for-loop I aappended rows to the matrix list, every row contains 0 at this point.
Using another for-loop I iterated over each neighbor in the dictionary and added a 1 
to the matrix if ther´s an edge between the node and the neighbor.
Lastly I printed ever row using yet another for-loop and returned the matrix.

After that I started the Bread-First Search Algorithm. 
I created a function called gen_parentheses which takes the parameter "pairs" as an argument.
In the first step I check if pairs is an integer. Then I check if pairs is greater then 0, 
because a pair is at least one.
Then I declared a list called queue which holds a tuple inside of it, containing three elements:
- current string being build
- open parantheses used so far
- closing parantheses used so far
In a while loop I first print the queue list, then I unpack the tuple inside of it into three variables:
current, opens_used, closes_used and pop the first element to implement the first-in-first-out behavior.
Then I check if the length of current is twice the length of pairs, because each paranthese has an opening and closing paranthese,
and if so I append the current to the results list. 


