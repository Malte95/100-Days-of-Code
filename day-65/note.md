# Today I Completed the Following Python Programming Task

## Issue Triage

## The Goal

Develop a Python function called `triage_issue(ms, message)` that decides what should happen with an issue.

The function receives:

* a number of milliseconds since the last post on the issue
* the last message posted on the issue

The function should then return one of three possible results:

```python
"leave it"
"close it"
"bump it"
```

The rules are:

* If the last message is less than 7 days ago, return `"leave it"`.
* If the last message is 7 or more days ago and the message contains `"bump"`, return `"close it"`.
* Otherwise, return `"bump it"`.

## The Tests

The function needs to pass the following tests:

```python
triage_issue(86400000, "Lets fix it")
# "leave it"
```

```python
triage_issue(1209600000, "still waiting")
# "bump it"
```

```python
triage_issue(864000000, "bump")
# "close it"
```

```python
triage_issue(604800000, "Do we still want this?")
# "bump it"
```

```python
triage_issue(604800000, "Bumping this")
# "close it"
```

```python
triage_issue(345600000, "I'll make a PR")
# "leave it"
```

## My Approach

### 1. Understood the 7-Day Limit

The task works with milliseconds.

Seven days in milliseconds are:

```python
604800000
```

So I used this number to check whether the last message was posted less than 7 days ago or 7 or more days ago.

### 2. Checked If the Message Is Less Than 7 Days Old

First, I checked whether `ms` is smaller than `604800000`.

```python
if ms < 604800000:
    return "leave it"
```

If this condition is true, the issue should not be changed.

For example:

```python
triage_issue(86400000, "Lets fix it")
```

returns:

```python
"leave it"
```

This is because `86400000` milliseconds is only 1 day.

### 3. Checked If the Message Is 7 or More Days Old

If the first condition is false, the message is at least 7 days old.

Then I checked whether `ms` is greater than or equal to `604800000`.

```python
elif ms >= 604800000:
```

This means the issue is old enough to either be bumped or closed.

### 4. Checked Whether the Message Contains “bump”

The task says that the word `"bump"` should be checked case-insensitively.

That means `"bump"`, `"Bump"`, and `"Bumping"` should all be treated correctly.

To do this, I used `.lower()` on the message.

```python
"bump" in message.lower()
```

This changes the message to lowercase before checking it.

For example:

```python
"Bumping this".lower()
```

becomes:

```python
"bumping this"
```

Then Python can find `"bump"` inside the message.

### 5. Returned “close it” When the Old Message Contains “bump”

If the issue is at least 7 days old and the message contains `"bump"`, the function returns:

```python
"close it"
```

The condition looks like this:

```python
elif ms >= 604800000 and "bump" in message.lower():
    return "close it"
```

For example:

```python
triage_issue(604800000, "Bumping this")
```

returns:

```python
"close it"
```

This is because the message is exactly 7 days old and contains `"bump"`.

### 6. Returned “bump it” in All Other Cases

If the message is at least 7 days old but does not contain `"bump"`, the function should return:

```python
"bump it"
```

This is handled with `else`.

```python
else:
    return "bump it"
```

For example:

```python
triage_issue(604800000, "Do we still want this?")
```

returns:

```python
"bump it"
```

This is because the issue is old enough, but the last message does not contain `"bump"`.

## The Final Function

```python
def triage_issue(ms, message):
    if ms < 604800000:
        return "leave it"
    elif ms >= 604800000 and "bump" in message.lower():
        return "close it"
    else:
        return "bump it"
```

## Why This Solution Works

The function follows the rules in the correct order.

First, it checks whether the issue is too recent.

If it is less than 7 days old, the function immediately returns:

```python
"leave it"
```

If the issue is 7 or more days old, the function then checks the message.

If the message contains `"bump"`, the issue should be closed.

Otherwise, the issue should be bumped.

The general process is:

1. Check if the issue is less than 7 days old.
2. If yes, return `"leave it"`.
3. If no, check whether the message contains `"bump"`.
4. If it does, return `"close it"`.
5. Otherwise, return `"bump it"`.

This makes the function work for recent issues, old issues, messages with `"bump"`, and messages without `"bump"`.

