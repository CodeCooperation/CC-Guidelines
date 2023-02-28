# Things you already know

We use Github Flow. It’s a way of working + a branching model to build and deploy software.

## Branches

- 🔒 : means theses branches are **protected** and should not be edited

- ✅ : means theses branches are **open** for you to develop into

### 🔒 master

- It’s our main branch.

- :warning: This branch **MUST NOT** BE USED IN ANY CASE

### 🔒 develop

- This is the branch were we will test our code.

- :warning: We **SHOULD NOT** commit to this branch!

- ⚠️ Only accepts PRs

### ✅ feature

- It’s all the branches related to a feature (or ticket)

- the naming of theses branches should be related to a Jira ticket.

- ex: feature/SPF-112

### ✅ hotfix

- Hotfix is a set of special branches for fixing bugs **that are in production**

- Using the same naming strategy as feature: ex hotfix/BZ-48

### 🔒 release

- This branche only marks the different releases of our software

# Before you start

Make a feature branch from DEV or DEVELOP.

Name your branch feature/[JIRA_ISSUE_ID]

If it’s a bug ifx, name it bug/[JIRA_ISSUE_ID]

# Working on your branch

Make commits that individually work. If your commit is partial, mark the title of the commit with **[WIP] (for Work In Progress)**

Push your code as soon as you can : **early and often**

multiple times a day is reecommended

- Make incremental, small changes
  
- Keep commits atomic (a single unit of work)
  
- Write descriptive commit messages
  

# You finished your feature… now what?

Now we should be able to merge your feature branch into dev, but wait:

```
development: -- A -- B -- C -- D -- M2
                      \         \  /
feature:               E -- F -- M1
```

While you were busy working, someone already changed DEV.

So you MUST first: merge DEV → feature/[…]

Resolve any conflicts.

Make sure your feature is still working

# Opening a Pull request

In Github, you will have a button (Open a pull request)

From your feature branch → develop

When you open a pull request, you can already see if there are any conflicts.

Keep in mind that a PR with conflicts will most likely be **rejected**. With a comment explaining why.

# After you open a pull request

**DO NOT MERGE YOUR PR BY YOURSELF**

The reason we have PRs, is that we validate each others code.

This validation is mainly done by:

- The techlead or the CTO.
  
- Another developer(s) from the same team (can take up to 20 minutes), and don’t be afraid of rejecting a PR if it does not follow the rules (naming, zero-conflicts policy, bad code, code smells, bugs etc..):
  

#### PR Checklist

* [ ] Follows best practices for the programming language and platform being used, such as using appropriate data structures, avoiding global variables, and using efficient algorithms.

* [ ] The project compiles without warnings 

* [ ] All tests run fault-free (eg. Unit test Coverage of new Code of >80%)

* [ ] Static code analysis without errors (bugs)

* [ ] The technical documentation is available and up to date 

* [ ] No warning/errors in both consoles (front and back)

* [ ] No known security issues

* [ ] The code is well-organized, readable, and maintainable.

* [ ] Ensure that the code follows the agreed-upon formatting and style guidelines.

## If (everything === “checked”), then:

# {

## 👍 Everything is good:

Merge pull request into DEV (you will have to wait, or ask another team member to do it)

Do not remove the feature branch (keep it)

Make a comment briefely highlighting what you reviewed

## 👎 Something is bad:

Refuse to merge the PR,

Leave a comment (the developer responsible will receive a notification)

And he/she will fix the code, and **make another PR**

**DO NOT REOPEN A CLOSED PULL REQUEST**

# }

We do this to keep a good quality of code, and to give you feedbacks on your code.
