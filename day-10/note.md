Today I completed the following coding challenges:

**The Goal:**

Define a function that takes a positive integer argument and determines whether it is a narcissistic number. 
A number is narcissistic if the sum of each of its digits raised to the power of the total number of digits equals the number itself.

Example: 153 has 3 digits, and \(1^3 + 5^3 + 3^3 = 153\), so it is narcissistic.

**My Approach:**

1.Initialization: 

I created an empty list called digits to store individual digits and a total variable set to 0 to keep track of the final sum.

2.Mathematical Extraction: 

I defined an inner helper function called digits_from_number that uses a while loop with the modulo operator (% 10) and integer division (// 10) to extract the digits from right to left mathematically.

3.Exponent Calculation: 

Once the helper function finished and the list was populated, I determined the exponent (power) by measuring the length of the digits list.

4.Summation & Verification: 

I used a for loop to iterate through the extracted digits, raising each to the calculated power and adding it to the total. Finally, I checked if the total matches the original number, returning True or False accordingly.


**The Goal:**

Write a method that takes an array of consecutive (increasing) letters as input and returns the missing letter in the array. The input array will always be valid, containing letters of only one case, with exactly one letter missing, and a minimum length of 2.

Example: ['a','b','c','d','f'] -> 'e' or ['O','Q','R','S'] -> 'P'

**My Approach:**

**1.Initialization:**I initialized a tracker variable called prev_num and assigned it the ASCII value of the first character in the array using Python's built-in ord() function.

**2.Sequential Iteration:**I used a for loop to iterate through each character in the input array to check the mathematical progression of the letters.

**3.Gap Detection:**Inside the loop, I calculated the difference between the ASCII value of the current character and prev_num. If the difference is greater than 1, it indicates that the consecutive order is broken and the missing letter has been found.

**4.Character Conversion & Update:**Once the gap is detected, I subtract 1 from the current ASCII value and convert it back to a character using chr() to return the missing letter. If no gap is found, I update prev_num with the current character's ASCII value for the next iteration.
