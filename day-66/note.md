# Today I Completed the Following Python Programming Task

## Issue Label Triage

## The Goal

Develop a Python function called `triage_issue(title, labels)` that updates the labels of an issue.

The function receives:

* an issue title
* an array of current labels

The function should then return an updated array of labels.

The rules are:

* If the issue doesn't have any labels and the title contains `"error"` or `"bug"`, add `"bug"` and `"needs triage"`.
* If the issue doesn't have any labels and the title contains `"feature"` or `"add"`, add `"enhancement"` and `"discussing"`.
* If the given labels contain `"needs triage"` and the title contains `"simple"` or `"easy"`, remove `"needs triage"` and add `"good first issue"`.
* If the given labels contain `"discussing"` and the title contains `"planned"` or `"next"`, remove `"discussing"` and add `"on the roadmap"`.
* Otherwise, if `"needs triage"` or `"discussing"` is present, remove it and add `"help wanted"`.
* If the title contains `"security"`, add `"critical"`.

## The Tests

The function needs to handle cases like:

* an empty label array with a bug-related title
* an empty label array with a feature-related title
* an issue with `"needs triage"` and an easy title
* an issue with `"discussing"` and a planned title
* an issue that still needs attention
* a security-related issue

These tests make sure the function works for new issues, existing labels, replacements, and security cases.

## My Approach

### 1. Understood the Label Rules

First, I read through the rules and separated them into different cases.

The task has two main situations:

* the issue has no labels yet
* the issue already has labels

This was important because the function should behave differently depending on whether the label array is empty or not.

### 2. Checked the Title for Important Words

Next, I checked whether the issue title contains certain words.

For bug-related issues, I checked for words like:

* `"bug"`
* `"error"`

For feature-related issues, I checked for words like:

* `"feature"`
* `"add"`

I also checked for special words like:

* `"security"`
* `"simple"`
* `"easy"`
* `"planned"`
* `"next"`

These words decide which labels should be added, removed, or replaced.

### 3. Checked the Current Labels

After checking the title, I checked the current labels.

The important labels were:

* `"needs triage"`
* `"discussing"`

I also checked whether the labels array was empty.

This helped me decide which part of the logic should run.

### 4. Created an Updated Labels List

Before changing the labels, I created a copy of the current labels.

This allowed me to build an updated label list without directly changing the original input.

The function then adds or removes labels from this copied list.

### 5. Handled Issues Without Labels

If the issue had no labels, I checked the title first.

If the title contained `"bug"` or `"error"`, I added:

* `"bug"`
* `"needs triage"`

If the title contained `"feature"` or `"add"`, I added:

* `"enhancement"`
* `"discussing"`

This handles new issues that need their first labels.

### 6. Handled Issues With Existing Labels

If the issue already had labels, I checked whether those labels should be replaced.

If the issue had `"needs triage"` and the title contained `"simple"` or `"easy"`, I removed `"needs triage"` and added:

* `"good first issue"`

This marks the issue as beginner-friendly.

### 7. Handled Planned Issues

Next, I checked whether the issue had the `"discussing"` label.

If the title contained `"planned"` or `"next"`, I removed `"discussing"` and added:

* `"on the roadmap"`

This means the issue is no longer only being discussed. It is now planned.

### 8. Added Help Wanted for General Cases

If the issue still had `"needs triage"` or `"discussing"`, but none of the more specific rules applied, I removed those labels.

Then I added:

* `"help wanted"`

This means the issue still needs attention from contributors.

### 9. Added the Security Label Separately

The security rule was handled separately because it can apply in addition to the other rules.

If the title contained `"security"`, I added:

* `"critical"`

This means a security-related issue can still receive normal labels, but it also gets marked as important.

## Why This Solution Works

The solution works because it follows the rules in the correct order.

First, it checks whether the issue has no labels.

If the issue has no labels, it adds the correct starting labels based on the title.

Then, if the issue already has labels, it checks whether `"needs triage"` or `"discussing"` should be replaced with a more specific label.

If no specific replacement applies, the function removes those temporary labels and adds `"help wanted"`.

Finally, it checks whether the issue is security-related.

If it is, the function adds `"critical"` as an extra label.

The general process is:

1. Check whether the issue has no labels.
2. Check the title for important words.
3. Check the current labels.
4. Add labels for new issues.
5. Replace labels for existing issues.
6. Add `"help wanted"` when no specific rule applies.
7. Add `"critical"` for security issues.
8. Return the updated labels.

This makes the function work for bug reports, feature requests, triage labels, discussion labels, beginner-friendly issues, roadmap issues, help wanted issues, and security-related issues.



