Today I completed the following coding challenge:

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
