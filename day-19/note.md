I started today session by reading about Abstraction.
Then I began the Discount Calculator. A program that will will determine the best price for a customer based on multiple discount rules.
I created a Product class to represent items with a name and price, and an abstract DiscountStrategy base class that defines a common interface for all discount types. 
Based on this, I implemented multiple discount strategies:
- PercentageDiscount – applies a percentage-based reduction
- FixedAmountDiscount – subtracts a fixed amount from the price
- PremiumUserDiscount – gives a special discount for premium users
The DiscountEngine takes a list of strategies and determines the best possible price by checking which discounts are applicable and selecting the lowest result.
What I did:
- Applied the Strategy Pattern to make discounts easily extendable
- Used abstract base classes (ABC) to enforce a consistent interface
- Implemented multiple independent discount rules
- Built a system that dynamically selects the optimal price for a user

