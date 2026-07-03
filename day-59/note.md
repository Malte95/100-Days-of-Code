**Today I completed the following Python programming task:**

1. Maximum Stock Profit

**The Goal**

Develop a Python function called `get_max_profit(prices, budget)` that calculates the maximum possible profit from buying and selling stocks over a given period.

A valid solution must meet these requirements:

* Receive a list of daily stock prices.
* Receive a budget in dollars.
* Buy only whole shares.
* Buy before selling.
* Consider only selling prices that come after the chosen buying price.
* Calculate the maximum possible profit.
* Return the result as a string with two decimal places.

For example:

`get_max_profit([5, 6], 50)`

should return:

`"10.00"`

**My Approach**

**1.Analyzed the Buying and Selling Rules**

I first focused on the most important rule: I can only sell a stock after buying it.

This means I cannot simply choose the lowest price and the highest price from the entire list. The selling price must always appear later in the list than the buying price.

For example:

`[4, 9, 3, 8]`

Although `3` is the lowest price and `9` is the highest price, I cannot buy at `3` and sell at `9` because `9` happens earlier in the list.

**2.Used Each Price as a Possible Buying Price**

I used a loop to go through every price in the list.

Each price was treated as a possible buying price.

For every possible buying price, I only checked the prices that appear after it in the list. These later prices were possible selling prices.

**3.Applied Nested Loops**

I used nested loops to compare possible buying and selling prices.

The outer loop selects a buying price.

The inner loop checks all prices after that buying price.

This ensures that selling can only happen after buying.

For example:

If the prices are:

`[10, 4, 7, 3, 8, 6]`

and the buying price is `4`, the possible selling prices are:

`[7, 3, 8, 6]`

**4.Calculated the Number of Shares**

For every possible buying price, I calculated how many whole shares can be bought with the available budget.

For example:

If the budget is `45` and the buying price is `4`:

`45 // 4 = 11`

This means I can buy 11 whole shares.

The `//` operator is important because it rounds down and prevents buying fractional shares.

**5.Calculated the Profit**

After finding a possible selling price that is higher than the buying price, I calculated the profit.

First, I calculated the profit from one share:

`sell_price - buy_price`

Then, I multiplied this by the number of shares that could be bought.

For example:

Buy price: `3`
Sell price: `8`
Budget: `45`

Number of shares:

`45 // 3 = 15`

Profit per share:

`8 - 3 = 5`

Total profit:

`15 × 5 = 75`

**6.Stored the Best Profit**

I created a variable called `best_profit` and started it at `0`.

Every time I calculated a possible profit, I compared it with the current best profit.

If the new profit was higher, I stored it as the new best profit.

This allows the function to keep track of the highest possible profit while checking all valid buying and selling combinations.

**7.Validated the Logic With Example Inputs**

I checked the logic with the following example:

`get_max_profit([10, 4, 7, 3, 8, 6], 45)`

The best choice is:

Buy at `3`
Sell later at `8`
Buy `15` shares
Make a profit of `75`

The expected result is:

`"75.00"`

**8.Formatting the Result**

The task requires the result to be returned as a string with exactly two decimal places.

For example:

`75` must become:

`"75.00"`

This ensures that the final result follows the required money format.

