---
title: Version control
description: 
draft: true
tags: 
date: 2024-10-12
---
If you have a working git workflow then use that. If you don’t, or are unhappy with the one you have here is what I suggest. 

Whenever you want to make a change create a branch. Commit your changes regularly, like ever 15 mins or so. Don’t stress about what the commit message should be. Anything will do. It won’t be saved anywhere when you’re done. 

Once the change you want to make is done create a PR so the branch you created will be merged to the master/main branch. Take care to accurately describe what the change is using the title and description. This will be stored in your git log and is what you will use to know what changed when. 

At this stage reviews of the work is done. Using the PR page you can record comments and discussions about the change. If you have any CI tooling you can also run it here. 

When merging the PR into master/main make sure to use the squash merge option only. By doing this all the temporary commits in the branch will “disappear” meaning just one atomic commit will be pushed to master/main. 

Apply a git tag to that new commit on master/main with the new version and then do whatever is necessary to release. 

If there is more than one change happening at the same time be sure to merge master/main into your branch so that your branch contains only the changes you are working on. 

What this workflow gives you is atomic, concurrent changes. Where people can experiment and work freely within their branch. But when it comes to recording the work done it appears in the git history as if it was done perfectly in one go. You can easily see all the changes made for a single “feature”. 

## what about rebase
If you’re a rebase advocate then by all means use it. But for the workflow I describe it has no benefit over merging master into the branch. At the end everything gets squashed into a single commit and applied to the master/main branch. 

I don’t advocate using it for this workflow as it is one more git command to learn. The focus of this workflow is to provide maximum version control benefit with the least amount of git knowledge. 