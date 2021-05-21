---
layout: post
title: Keeping “Clean git history”
date: 2021-03-01
---

The first time I heard "keep your git history clean" I didn’t really understand what that meant or why it was important. Prior to my time at GDS, github just felt like a tool to save my progress. Though I had paired extensively at the coding bootcamp I attended, there wasn’t 
Time to really collaborate on a repository for an extended period and so the idea of git history was something that fell by the wayside. 

This attitude had to change as I joined GDS, as it turns out, the following is not considered a very professional or useful commit:

`git commit -m "this works now"`  

While I never actually pushed something that horrendous to a team repo, it was made clear to me in a series of heavily commented code reviews that my git record keeping could use some work. 

Github is one of those things that you feel you have a solid grasp of until the second you don't. Departing from the well trodden flow of git add, git commit and git push rapidly leads to migraine inducing mind mapping in which you try to visualise where things should be in the timeline of commits. 

This is where interactive rebase comes into the picture. Let's say I have a messy history full of  useful commits like “fixes test”, “stops the crashing” etc. I can do an interactive rebase in order to clean up this history to make something more presentable to my fellow devs. I would run something like this:

`git rebase -i HEAD~3 # where 3 is how many commits you want to squash via a rebase`  

When you run this command, you'll then go into interactive rebase mode. Once in interactive mode, you'll see a list of commits at the top (more specifically, a list the length of the number you specified above). At the far left of each commit you'll see the word "pick". This means this commit will be included in your git history. Your goal now is to go through each of these and decide which to keep (or "pick"), "squash", or "fixup" (same as "squash" except you remove the commit message).

`pick xxxxxxx Actual useful commit description`  
`pick xxxxxxx awsd`  
`pick xxxxxxx qwerty`  

The very first commit is the one I want, and even though I want the changes for the second and third commits, I don't want the message for the second on there (fixup, please). 

`pick xxxxxxx Actual useful commit`  
`fixup xxxxxxx awsd`  
`squash xxxxxxx qwerty`  

And, finally, when you're done you should see something like the following:

`example-repo $ git rebase -i HEAD~3`  
`Successfully rebased and updated refs/heads/master.`  

Doing a rebase like this and clearing up some of the more throwaway commits makes it much easier for other developers to follow what is going on in a PR, especially when time has elapsed since the work was done. A codebase full of bad git history would be impossibly hard to understand. 
