Today I completed the following coding challenge:

**The Goal:**

Given a 2D array representing a set of dominoes, return the longest valid chain.

A valid chain must meet these requirements:

-Each domino is a pair of numbers from 0–6 (e.g., [3, 2]).
-The second number of each domino must match the first number of the next domino in the chain.
-Any domino can be flipped (e.g., [3, 2] can be played as [2, 3]).
-The solution must explore all possibilities to guarantee finding the single longest valid chain.

**My Approach:**

**1.Outer Loop Strategy:** Since any domino could potentially be the perfect starting piece, I used a loop to test every single domino from the input array as the initial element of the chain—testing both its standard and flipped orientation.
**2.Recursive Backtracking:** I designed an inner helper function using recursion (Depth-First Search) to dynamically grow the chain from the current end piece (used[-1]).
**3.Immutability & Pure Functions:** To safely explore multiple branching paths without corrupting the state of parallel searches, I avoided mutating lists via .append(). Instead, I passed fresh, independent copies of the updated chain and the remaining available dominoes to each recursive branch.
**4.Global Record Tracking:** I utilized Python's nonlocal keyword to maintain a global maximum benchmark, updating the master record whenever a longer valid chain was successfully constructed.


