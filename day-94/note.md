# Daily Coding Challenge: Food Chain

Today, I completed a Python coding challenge about constructing a food chain from a collection of predator-prey relationships.

## The Challenge

The function receives a list containing predator-prey pairs.

Each pair contains two strings:

```python
[predator, prey]
```

The first animal is the predator, and the second animal is its direct prey.

For example:

```python
[
    ["wolf", "deer"],
    ["deer", "grass"]
]
```

This represents the following food chain:

```text
wolf → deer → grass
```

The function must return the complete food chain as a list of strings, beginning with the apex predator and ending with the animal or organism that does not prey on anything else.

For this example, the result is:

```python
["wolf", "deer", "grass"]
```

The apex predator is the animal that appears as a predator but never appears as prey.

The pairs may also be provided in a different order.

For example:

```python
[
    ["rabbit", "grass"],
    ["fox", "rabbit"],
    ["eagle", "fox"]
]
```

Even though the pairs do not begin with the apex predator, the function must still return:

```python
["eagle", "fox", "rabbit", "grass"]
```

## My Approach

First, I created an empty dictionary called `food_map`.

This dictionary stores each predator and its direct prey:

```python
food_map = {}
```

For example, the following pairs:

```python
[
    ["wolf", "deer"],
    ["deer", "grass"]
]
```

produce this dictionary:

```python
{
    "wolf": "deer",
    "deer": "grass"
}
```

The predator is used as the dictionary key, while the prey is used as its value.

I also created an empty set called `prey_set`:

```python
prey_set = set()
```

This set stores every animal that appears as prey.

I then used a `for` loop to unpack each pair into the variables `predator` and `prey`:

```python
for predator, prey in pairs:
```

For example, the pair:

```python
["wolf", "deer"]
```

provides:

```python
predator = "wolf"
prey = "deer"
```

Inside the loop, I added the predator-prey relationship to `food_map`:

```python
food_map[predator] = prey
```

I also added the prey to `prey_set`:

```python
prey_set.add(prey)
```

After processing all pairs, I searched for the apex predator.

The apex predator must be a key in `food_map`, because it hunts another animal. However, it must not appear in `prey_set`, because nothing else hunts it.

I used another loop to check every predator:

```python
for candidate in food_map:
    if candidate not in prey_set:
        apex_predator = candidate
        break
```

The variable `candidate` represents the animal currently being checked.

Once I found an animal that was not inside `prey_set`, I stored it as the apex predator.

The `break` statement stops the loop because the apex predator has already been found.

Next, I created the result list and added the apex predator as its first element:

```python
food_chain = [apex_predator]
```

I also created a variable called `current_predator`:

```python
current_predator = apex_predator
```

This variable keeps track of the current animal in the chain.

I then used a `while` loop to follow the predator-prey relationships:

```python
while current_predator in food_map:
```

The loop continues as long as the current animal exists as a key in `food_map`. This means that the current animal has prey.

Inside the loop, I found the current predator's prey:

```python
current_prey = food_map[current_predator]
```

I added that prey to the food chain:

```python
food_chain.append(current_prey)
```

Finally, I made the prey the new current predator:

```python
current_predator = current_prey
```

This allows the loop to continue moving down the food chain.

For example:

```text
orca → seal → salmon → herring → shrimp → plankton
```

When `plankton` becomes the value of `current_predator`, the loop checks whether `"plankton"` is a key in `food_map`.

Because plankton does not prey on another organism in the provided relationships, it is not a key in the dictionary. The condition becomes false, and the loop ends automatically.

## My Solution

```python
def get_food_chain(pairs):
    food_map = {}
    prey_set = set()
    apex_predator = ""

    for predator, prey in pairs:
        food_map[predator] = prey
        prey_set.add(prey)

    for candidate in food_map:
        if candidate not in prey_set:
            apex_predator = candidate
            break

    food_chain = [apex_predator]
    current_predator = apex_predator

    while current_predator in food_map:
        current_prey = food_map[current_predator]
        food_chain.append(current_prey)
        current_predator = current_prey

    return food_chain
```

## What I Learned

During this challenge, I practiced working with:

* Python lists
* nested lists
* unpacking list elements
* dictionaries
* dictionary keys and values
* sets
* the `.add()` method
* `for` loops
* `while` loops
* the `in` and `not in` operators
* the `.append()` method
* the `break` statement
* following relationships stored in a dictionary

One of the main challenges was identifying the apex predator.

I learned that I could separate the animals into two groups:

* Animals that appear as predators
* Animals that appear as prey

The apex predator appears in the first group but not in the second group.

Using a set for all prey animals made it easy to check whether a predator had previously appeared as prey:

```python
if candidate not in prey_set:
```

I also learned why a dictionary is useful for this challenge.

The dictionary creates a direct connection between each predator and its prey:

```python
food_map[predator] = prey
```

This means I can quickly find the next animal in the chain by using the current predator as a key:

```python
current_prey = food_map[current_predator]
```

Another important part was understanding the `while` loop.

The loop continues only while the current animal is a predator stored in `food_map`:

```python
while current_predator in food_map:
```

During each iteration, the prey becomes the new current animal. Eventually, the loop reaches an animal that is not a predator. Because that animal is not a key in the dictionary, the loop ends.

I also learned that the order of the original pairs does not matter. Once all relationships have been stored in the dictionary, the function can begin with the apex predator and follow each connection in the correct order.

Overall, this was a useful exercise for improving my understanding of dictionaries, sets, loops, membership checks, list construction, and how to represent relationships between data in Python.

