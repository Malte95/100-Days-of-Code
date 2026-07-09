# Today I Completed the Following Python Programming Task

## Issue Label Triage

## The Goal

The goal of this task was to develop a Python function called `triage_issue(title, labels)`.

The function receives:

* an issue title
* an array of current labels

The function should return an updated array of labels based on different rules.

## The Rules

If the issue does not have any labels, the function should add:

* `"bug"` and `"needs triage"` if the title contains `"error"` or `"bug"`
* `"enhancement"` and `"discussing"` if the title contains `"feature"` or `"add"`

Otherwise, if the given labels contain:

* `"needs triage"` and the title contains `"simple"` or `"easy"`, remove `"needs triage"` and add `"good first issue"`
* `"discussing"` and the title contains `"planned"` or `"next"`, remove `"discussing"` and add `"on the roadmap"`

Otherwise, if `"needs triage"` or `"discussing"` is present, remove it and add `"help wanted"`.

If the title contains `"security"`, add a `"critical"` label.

## My Approach

### 1. Created Boolean Variables for the Title

First, I created Boolean variables to make the title checks easier to understand.

For example, I checked whether the title contains words like:

* `"bug"`
* `"error"`
* `"feature"`
* `"add"`
* `"security"`
* `"simple"`
* `"easy"`
* `"planned"`
* `"next"`

This made the conditions easier to read later in the function.

### 2. Created Boolean Variables for the Labels

Next, I checked the current labels.

I created Boolean variables to check whether:

* `"needs triage"` is already in the labels
* `"discussing"` is already in the labels
* the labels array is empty

This helped separate the title logic from the label logic.

### 3. Made a Copy of the Labels

I created a copy of the labels array before changing it.

This is useful because I wanted to work with an updated version of the labels instead of directly changing the original list.

### 4. Checked If the Issue Has No Labels

The first main condition checks whether the issue has no labels.

If the labels array is empty and the title contains `"bug"` or `"error"`, I add:

* `"bug"`
* `"needs triage"`

If the labels array is empty and the title contains `"feature"` or `"add"`, I add:

* `"enhancement"`
* `"discussing"`

This handles new issues that do not have any labels yet.

### 5. Checked Existing Labels

If the issue already has labels, I checked whether it has `"needs triage"`.

If it also has a title containing `"simple"` or `"easy"`, I remove:

* `"needs triage"`

Then I add:

* `"good first issue"`

This means the issue is probably beginner-friendly.

### 6. Checked the Discussing Label

Next, I checked whether the issue has the `"discussing"` label.

If the title contains `"planned"` or `"next"`, I remove:

* `"discussing"`

Then I add:

* `"on the roadmap"`

This means the issue is no longer just being discussed. It is now planned.

### 7. Added Help Wanted for General Cases

If the issue still has `"needs triage"` or `"discussing"`, but none of the more specific rules apply, I remove those labels.

Then I add:

* `"help wanted"`

This handles issues that still need attention.

### 8. Added the Security Rule Separately

The security rule is special because it can apply in addition to the other rules.

So I checked it separately at the end.

If the title contains `"security"`, I add:

* `"critical"`

This means a security-related issue can still receive normal labels, but it also gets marked as critical.

## The Final Function

```python
def triage_issue(title, labels):
    title = title.lower()

    titleHasBugWord = "bug" in title or "error" in title
    titleHasFeatureWord = "feature" in title or "add" in title
    titleHasSecurity = "security" in title
    titleHasEasyWord = "simple" in title or "easy" in title
    titleHasRoadmapWord = "planned" in title or "next" in title

    hasNeedsTriage = "needs triage" in labels
    hasDiscussing = "discussing" in labels
    hasNoLabel = labels == []

    updatedLabels = labels[:]

    if hasNoLabel:
        if titleHasBugWord:
            updatedLabels.extend(["bug", "needs triage"])
        elif titleHasFeatureWord:
            updatedLabels.extend(["enhancement", "discussing"])
    else:
        if hasNeedsTriage and titleHasEasyWord:
            updatedLabels.remove("needs triage")
            updatedLabels.append("good first issue")
        elif hasDiscussing and titleHasRoadmapWord:
            updatedLabels.remove("discussing")
            updatedLabels.append("on the roadmap")
        elif hasNeedsTriage or hasDiscussing:
            if hasNeedsTriage:
                updatedLabels.remove("needs triage")
            if hasDiscussing:
                updatedLabels.remove("discussing")
            updatedLabels.append("help wanted")

    if titleHasSecurity:
        updatedLabels.append("critical")

    return updatedLabels
```

## Why This Solution Works

This solution works because it follows the rules in the correct order.

First, the function checks whether the issue has no labels.

If there are no labels, it decides whether the issue should start as a bug or as an enhancement.

If the issue already has labels, the function checks whether the existing labels should be replaced with more specific labels.

For example, `"needs triage"` can become `"good first issue"` if the title contains `"simple"` or `"easy"`.

Also, `"discussing"` can become `"on the roadmap"` if the title contains `"planned"` or `"next"`.

If none of the specific rules apply, the function removes `"needs triage"` or `"discussing"` and adds `"help wanted"`.

Finally, the function checks whether the title contains `"security"`.

If it does, the function adds `"critical"` as an extra label.

## Summary

The general process is:

1. Check the title for important words.
2. Check the current labels.
3. Create a copy of the labels.
4. Apply the correct label rule.
5. Add `"critical"` if the issue is security-related.
6. Return the updated labels.

This makes the function work for new issues, existing issues, triage labels, discussion labels, beginner-friendly issues, roadmap issues, help wanted issues, and critical security issues.


