Today I completed the following coding challenge:

**The Goal:**

Define a function that takes an integer argument and returns a logical value True or False depending on if the integer is a prime.

**A valid prime number:**

 -Is a natural number greater than 1.
 
 -Has no positive divisors other than 1 and itself.
 
 -Must be handled efficiently to avoid timeouts for numbers up to 2^31.

**My Approach:**

1.First, I handled edge cases by checking if the number was less than 2.

2.I declared a variable called limit to store the square root of the number, 
as any divisor larger than the square root would have a corresponding partner smaller than it.

3.Finally, I used a loop and the modulo operator to check if the number is divisible by any integer from 2 up to this limit. 
If a divisor is found, the function returns False; otherwise, it returns True.


I did another coding challenge:

**The Goal:**

Define a function that takes a string argument and returns an object (JavaScript) or dictionary (Python) mapping each character to the number of times it 

appears.Example:get_frequency("test") should return {"t": 2, "e": 1, "s": 1}.

**My Approach:**

1.Initialization: I started by creating an empty dictionary called result to store the character counts as key-value pairs.

2.Iteration: I used a for loop to iterate through each character in the input string s.

3.Logic: For each character, I implemented a conditional check:

  1.If the character was already present in the dictionary, I incremented its value by 1.
  
  2.If it was not present, I initialized it with a value of 1.
  
4.Return: Finally, the function returns the completed dictionary.
