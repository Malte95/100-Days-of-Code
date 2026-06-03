Today I began the last certification project for the freeCodeCamps Python Certificate.
In this project I will solve the mathematical puzzle known as "Tower of Hanoi".
I began by declaring a function called "hanoi_solver", which takes an integer representing the total number of "disks".
I created four lists:
  - start_rod, which takes the total number from the input and sorts them from largest to smallest
  - help_rod: the middle rod (at the start)
  - end_rod: the end position of the disks. 
*Note the positioning of the rods shift, during the algorithm. 
  - moves: a list which stored the position after each movement, for this should be printed after the puzzle has been solved.
Because I have to store each step during the algorithm, I decided to creat a function, so that I don't have to repead myself.
The function is called "stored_position", it appends the current position of each disk in each step to the moves list.
