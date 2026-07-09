Today I Completed the Following Python Programming Task

Issue Label Triage

The Goal

Develop a Python function called triage_issue(title, labels) that updates the labels of an issue based on the issue title and the current labels.

The function receives:

an issue title
an array of current labels

The function should then return an updated array of labels.

The rules are:

If the issue does not have any labels, add:

"bug" and "needs triage" if the title contains "error" or "bug"
"enhancement" and "discussing" if the title contains "feature" or "add"

Otherwise, if the given labels contain:

"needs triage" and the title contains "simple" or "easy", remove "needs triage" and add "good first issue"
"discussing" and the title contains "planned" or "next", remove "discussing" and add "on the roadmap"

Otherwise, if "needs triage" or "discussing" is present, remove it and add "help wanted".

If the title contains "security", add a "critical" label.

The Tests

The function should work for cases like these:

triage_issue("bug in login", [])

# ["bug", "needs triage"]

triage_issue("add dark mode", [])

# ["enhancement", "discussing"]

triage_issue("simple login bug", ["bug", "needs triage"])

# ["bug", "good first issue"]

triage_issue("next dashboard update", ["enhancement", "discussing"])

# ["enhancement", "on the roadmap"]

triage_issue("login issue", ["needs triage"])

# ["help wanted"]

triage_issue("security bug in login", [])

# ["bug", "needs triage", "critical"]

My Approach

1. Created Boolean Variables for the Title

First, I created several Boolean variables to make the conditions easier to understand.

Instead of writing all checks directly inside the if-statements, I stored the results in variables.

For example:

titleHasBugWord checks whether the title contains "bug" or "error".

titleHasFeatureWord checks whether the title contains "feature" or "add".

titleHasSecurity checks whether the title contains "security".

titleHasEasyWord checks whether the title contains "simple" or "easy".

titleHasRoadmapWord checks whether the title contains "planned" or "next".

This made the code easier to read because each variable describes one clear condition.

2. Created Boolean Variables for the Labels

Next, I checked the current labels.

I created variables for the important label states:

hasNeedsTriage checks whether "needs triage" is already in the labels.

hasDiscussing checks whether "discussing" is already in the labels.

hasNoLabel checks whether the labels array is empty.

This helped separate the title checks from the label checks.

3. Made a Copy of the Labels

I created a copy of the labels array before changing it.

This is important because I wanted to return an updated version of the labels without directly changing the original array.

I used a copied list and then added or removed labels from that copy.

4. Checked If the Issue Has No Labels

The first main rule checks whether the issue has no labels.

If the labels array is empty and the title contains "bug" or "error", I add:

"bug"
"needs triage"

If the labels array is empty and the title contains "feature" or "add", I add:

"enhancement"
"discussing"

This handles new issues that do not have any labels yet.

5. Checked Existing Labels

If the issue already has labels, I checked the existing labels.

If the issue has "needs triage" and the title contains "simple" or "easy", I remove:

"needs triage"

Then I add:

"good first issue"

This means the issue is probably beginner-friendly.

6. Checked Discussing Labels

Next, I checked whether the issue has the "discussing" label.

If the title contains "planned" or "next", I remove:

"discussing"

Then I add:

"on the roadmap"

This means the issue is no longer just being discussed. It is now planned.

7. Added Help Wanted for Unresolved Labels

If the issue still has "needs triage" or "discussing", but none of the more specific rules apply, I remove those labels.

Then I add:

"help wanted"

This handles issues that still need attention but do not match the more specific categories.

8. Added the Security Rule Separately

The security rule is special because it can apply in addition to the other rules.

So I checked it separately at the end.

If the title contains "security", I add:

"critical"

This means a security issue can still receive the normal labels, but it also gets marked as critical.

The Final Function

def triage_issue(title, labels):
title = title.lower()

```
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

Why This Solution Works

The function follows the rules in the correct order.

First, it checks whether the issue has no labels.

If there are no labels, the function decides whether the issue should start as a bug or an enhancement.

If the issue already has labels, the function checks whether the issue can be moved into a more specific category.

For example, "needs triage" can become "good first issue" if the title contains "simple" or "easy".

Also, "discussing" can become "on the roadmap" if the title contains "planned" or "next".

If neither of those specific cases applies, the function removes "needs triage" or "discussing" and adds "help wanted".

Finally, the function checks whether the title contains "security".

If it does, the function adds "critical" as an extra label.

The general process is:

Check the title for important words.
Check the current labels.
Create a copy of the labels.
Apply the correct label rule.
Add "critical" if the issue is security-related.
Return the updated labels.

This makes the function work for new issues, existing issues, triage labels, discussion labels, beginner-friendly issues, roadmap issues, help wanted issues, and critical security issues.

