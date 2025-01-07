---
title: Git Flow for Config Template Management
description: Just enough Git to manage config templates reliably
draft: false
tags:
  - git
  - opinion
date: 2025-01-07
---
# What is Gitflow
The term gitflow refers to the set of [[Git|git]] commands and code management practices a development team uses in one or more code bases.

There are several gitflows to chose from, theres the [original](https://nvie.com/posts/a-successful-git-branching-model/), [Github flow](https://docs.github.com/en/get-started/using-github/github-flow), [Atlassian](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) and [Gitlab flow](https://about.gitlab.com/topics/version-control/what-is-gitlab-flow/) to name just a few. They all achieve the same aim - managing code based. But how they do it have trade offs that may help or hinder the development team.
# Why a new one
For a lot of people doing network automation they are network engineers first and developers second, or may not even consider themselves developers at all. Yet we all want to get the benefits of [[Version Control Systems|version control]].

The purpose of this gitflow is to use as little of [[Git|git]] as possible while providing all the flexibility and control that one would need to manage configuration templates. The thinking being that [[Git|git]] is the tool, we want to dedicate as little brain space to it as possible so we can concentrate on the really important part - the configuration.

It is easy to get sucked into using a tool to it's maximal potential. This gitflow is specifically designed to fight against that. This gitflow is designed to reliably manage config templates without a deep knowledge of [[Git|git]]. Yes, *someone* should know [[Git|git]] deeply to troubleshoot when things go wrong. But not *everyone* needs to know [[Git|git]] beyond these basics to be productive.
# High level description
The gitflow can be summarised as follows:
- create a branch from master/main
- make changes to the template(s) across one or more commits
- once the change is finished create a PR
- summarise the change(s) in the PR description
- perform whatever review or CI jobs you need to be satisfied the change does what you want and not what you don't want
- squash merge the PR and delete the branch

# Detailed example
Here's how you would use [[Git|git]] to perform this flow:
```bash
git checkout -b <name>
# change template(s)
git add <template file path>
git commit -m "<some relevant message>"
git push
# change template(s)
git add <template file path>
git commit -m "<some relevant message>"
git push
# repeat until done
# create pull request
# update the PR description to properly reflect why the change was needed
# perform whatever review/checks
# select "delete branch on merge"
# when merging the PR chose "squash-merge" as the merge type
# now tag the commit on master/main with the version
git switch master
git tag <version name>
git push --tags
```
Creating the PR is not shown as there are multiple ways to do this. You can do this using your version control UI (e.g. github.com or gitlab.com). If you are using the [Github cli tool](https://cli.github.com/) you can create the PR and do the merge bits in the terminal also.

The key thing is to select "delete branch on merge" and to use "squash-merge" as the merge type.

Commit your changes regularly, like ever 15 mins or so. Don’t stress about what the commit message should be. Anything will do. It won’t be saved anywhere when you’re done. The important thing is you are free to `git commit` - and `git push` - as often as you like. And I'm recommending you do it more often than that!
# Rational
This flow uses very little of the [[Git|git]] CLI. If you include `git clone` (which you do only once) and `git pull` (which you may need to do often) we only need 6 [[Git|git]] commands. And only 3 of them regularly while making the template change.

Running `git add`, `git commit` and `git push` regularly is generally recommended. Not only does it ensure a backup of your work so far (computers are very reliable these days but you can never predict when one will fail) but you can also go back to a previous commit as a way of undoing changes (rather than smashing the delete key endlessly).

This flow treats the branch where the changes are being made as a playpen. You are free to do whatever you like here. Do not concern yourself with ensuring in the future you can tell with what changed where, when and why. That is handled in the PR. Just concentrate on what needs to be changed and feel free to save your work regularly.

Using "squash-merge" when merging the PR is key. It condenses all the branch commits to a single commit on the master/main branch. This gives you the clean history where each set of changes to the templates is atomic.

The master/main branch is your release branch. It supports multiple versions of the templates by tagging the PR merge commit with the version info. Managing multiple long lived branches is hard. Better to focus your efforts on running the network than managing [[Git|git]].

Deleting the branch on merge does mean you lose some history but I argue that history is of little value. It is better to have as few branches as possible (i.e. master/main plus any active template changes branches) than it is to have the repo littered with defunct branches that anyone will rarely every look at.
# What is not included
How you version the templates is left to the reader to decide. This gitflow does not depend on any versioning scheme so you are free to use whatever works best for you.

It is recommended that you have checks you perform whenever a template changes and that you automate those checks and integrate that into your PR using CI. What those checks are and how you integrate depends on which [[Git|git]] host you use and what checks you need to perform.

Concurrent changes is supported in this gitflow. Working this way does increase the chance of a merge conflict (where [[Git|git]] is unable to automatically integrate that change from another branch). But that is always the case with concurrent changes. If multiple people are working on multiple change branches at the same time then whoever finishes first merges to master/main. All the other branches then merge the new master/main into their branch. If there are merge conflicts, they are resolved in the change branch - taking care not to revert the new master/main branch changes. Repeat the process until all open change branches are merged to master/main.
# What about rebase
If you’re a `git rebase` advocate then by all means use it. But for the gitflow  described here it has no benefit over merging master into the branch. At the end everything gets squashed into a single commit and applied to the master/main branch. 

This gitflow does not advocate using `git rebase` as it is one more [[Git|git]] command to learn. The focus of this workflow is to provide maximum version control benefit with the least amount of [[Git|git]] knowledge.
# What about worktrees
You can use this gitflow with worktrees. Just manage your branches using `git worktree`, pretty much everything else about the gitflow remains the same.