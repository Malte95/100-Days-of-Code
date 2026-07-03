# Today I Completed Two Python Coding Challenges

## 1. Record Migration

### The Goal

Develop a Python function called `migrate_record(schema, record)` that fills missing properties in a record using values from a schema.

A valid solution must meet these requirements:

* Add properties from the schema when they are missing from the record.
* Keep all properties that already exist in the record.
* Do not overwrite existing record values with schema values.
* Return the completed record with both the existing and missing fields.

For example:

```python
migrate_record(
    {"username": "", "posts": 0},
    {"verified": True}
)
```

should return:

```python
{"username": "", "posts": 0, "verified": True}
```

If the record already contains values for the same keys, those values must remain unchanged:

```python
migrate_record(
    {"username": "", "posts": 0},
    {"username": "camper", "posts": 5}
)
```

should return:

```python
{"username": "camper", "posts": 5}
```

### My Approach

#### Understood the Priority of the Record

I first analyzed which dictionary should have priority when both dictionaries contain the same key.

The schema contains default values, while the record contains the actual existing data. Therefore, the values from the record must always take priority.

For example, if the schema contains:

```python
{"username": ""}
```

and the record contains:

```python
{"username": "camper"}
```

the final result must keep:

```python
{"username": "camper"}
```

because the record value already exists and must not be overwritten.

#### Learned How to Combine Dictionaries

I learned that Python dictionaries can be combined using the `.update()` method.

The `update()` method adds new keys from one dictionary into another dictionary. When both dictionaries contain the same key, the value from the dictionary added later replaces the previous value.

This is useful for the migration task because the schema values can be added first and the record values can be applied afterward.

#### Started With the Schema Values

I used the schema as the starting point because it contains all default fields that may be required in the final record.

For example:

```python
{"username": "", "posts": 0}
```

This ensures that the result contains every property defined by the schema.

#### Added the Existing Record Values Afterwards

After starting with the schema values, I added the record values.

Because the record values are added afterward, they replace matching schema values when necessary.

This solves both required cases:

* Missing fields are taken from the schema.
* Existing record fields are preserved.

#### Checked Overlapping Keys

I tested the important case where both dictionaries contain the same keys.

For example:

```python
schema = {"username": "", "posts": 0}
record = {"username": "camper", "posts": 5}
```

The final result must keep `"camper"` and `5`, rather than replacing them with the default schema values.

### Completed the Challenge

The final function successfully combines default schema values with an existing record while preserving all existing record data.

This work helped me practice dictionaries, dictionary keys and values, the `.update()` method, merge order, and understanding which values should have priority when combining data.

---

## 2. Duplicate Character Count

### The Goal

Develop a Python function called `duplicate_character_count(str1, str2)` that counts how often characters from the first string appear in the second string.

A valid solution must meet these requirements:

* Go through the characters of `str1`.
* Check whether each character appears in `str2`.
* Count how often that character occurs in `str2`.
* Count each distinct character from `str1` only once.
* Return the final total.

For example:

```python
duplicate_character_count("hello", "hola")
```

should return:

```python
3
```

The matching characters are:

* `h` appears once in `"hola"`
* `l` appears once in `"hola"`
* `o` appears once in `"hola"`

The character `l` appears twice in `"hello"`, but it should only be processed once.

### My Approach

#### Created a Counter Variable

I started by creating a variable called `count` with the value `0`.

This variable stores the total number of matching character occurrences found in the second string.

#### Used a For Loop to Process the First String

I used a `for` loop to go through every character in `str1`.

For each character, I checked whether it appears in `str2`.

The Python expression:

```python
char in str2
```

returns `True` when the character exists in the second string and `False` when it does not.

#### Used the `.count()` String Method

I learned that checking:

```python
char in str2
```

only tells me whether a character exists at least once.

However, the challenge requires counting how often the character occurs.

To solve this, I used:

```python
str2.count(char)
```

This returns the exact number of times a character appears in the second string.

For example:

```python
"aaab".count("a")
```

returns:

```python
3
```

#### Added Character Counts Instead of Replacing Them

During the first attempt, I used an assignment that replaced the old value of `count`.

I recognized that this would only keep the count from the most recently processed matching character.

For example, with:

```python
str1 = "ab"
str2 = "aaab"
```

the function needs to calculate:

```python
3 + 1 = 4
```

Therefore, I changed the logic so that each new occurrence count is added to the existing total.

#### Tracked Characters That Were Already Processed

The next issue was repeated characters in `str1`.

For example, `"hello"` contains the character `l` twice. Without additional logic, the function would count the `l` in `"hola"` twice.

To prevent this, I created a list called `seen`.

This list stores the characters that have already been processed.

Before counting a character, I check whether it is already in `seen`.

* If the character has already been processed, it is skipped.
* If it has not been processed, it can be counted and then added to `seen`.

#### Used `continue` Instead of `break`

I learned the difference between `break` and `continue`.

`break` ends the complete loop immediately.

This was not correct for the challenge because the function still needs to check later characters after finding a duplicate.

For example, in `"hello"`, the second `l` should be skipped, but the final `o` must still be checked.

Using `continue` allows the function to skip only the current repeated character and continue with the rest of the loop.

#### Tested the Final Logic

I tested the function with several examples:

```python
duplicate_character_count("hello", "hola")
```

should return:

```python
3
```

```python
duplicate_character_count("merhaba", "xin chao")
```

should return:

```python
2
```

```python
duplicate_character_count(
    "hello world",
    "hello to everyone around the world"
)
```

should return:

```python
26
```

### Completed the Challenge

The final function successfully counts each distinct character from the first string and adds up how often those characters appear in the second string.

This work helped me practice loops, strings, the `in` operator, the `.count()` method, counters, lists, repeated-character handling, and the difference between `break` and `continue`.

