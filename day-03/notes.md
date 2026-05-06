Today I finished the Breadth-First Search Algorithm from yesterday.
I added an else-block after my if-statement in the while loop.
Inside the else-block there are two if-statements, one to check if open parantheses are less then pairs,
if true I append a new tuple to the queue list, and another one to check if closing parantheses are less then opening parantheses,
if true I alos append a new tuple to the queue list. 
At the end I testet my program by calling the gen_parantheses function with two cases, one with 3 pairs and one with 5 pairs.
_______________________________________________________________________________________________________________________________________________________________________________
After that, I completed the Depth-First Search Algorithm Lab. 
First, I searched on the internet to understand what this algorithm actually does and how it works. 
After that, I implemented it in my function called dfs. I created two lists: one for the visited elements and another one for the stack. 
Then I used a while loop to repeatedly pop the last element from the stack and store it in the current variable (last-in-first-out).
After that, I appended it to the visited list. In a for loop, I iterated over the current row in the adjacency matrix and used an 
if statement to check whether there is an edge to another node and whether it had not been visited yet. 
If both conditions were true, I appended the node to the stack.
