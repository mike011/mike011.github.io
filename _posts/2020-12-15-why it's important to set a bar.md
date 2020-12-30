---
title: "Why it's important to set a bar"
published: true
---

Recently in a job interview a question came up to the usefulness of running warning tools that were completely disabled from producing any warnings. This might seem like a waste of time, but I'm a huge fan of doing this. Why? Well that's what this article is all about.

# Background

I'm a huge fan of clean code and having the build system do all it can to make sure the code stays clean going forward. In the past in Eclipse with Java I've used tools such as PMD and Checkstyle. On top of the build warnings that were normally produced these tools would produce additional warnings for things such as formatting, import ordering, and common anti-patterns. They helped while developing new code to make it match the rest of the source base and keep the quality bar high. This also helped us not slowly add more and more warnings to the code base. Nobody starts a project with a 1000+ warnings, it only gets there over time of adding a small amount per commit, or not fixing deprecated warnings when new versions come out.

# Why?

## Easy of Running

If you have the tools running then whenever it doesn't work, you'll know about it immediately. This is really helpful for when one day if you want to add some checks, it will simply be editing the rules file to allow that happen.

## Subtle nudge to Improve Quality

This encourages engineers to enable some rules themselves and fix them. These kind of tasks are great to tackle when you just want a break from what you are working on, but still want to make the product better. At a previous place of employment one of the senior engineers categorized a bunch of warnings into similar groups and logged tickets for them to get fixed. Then over the next 3 months or so most of the tickets were picked up and the warnings were fixed.

## Do you want to waste your time fixing the same bugs?

You are standing on the shoulders of others who've come before you and you can use there expertise to your advantage. A lot of the more useful rules were created to fix common bugs, do you really want to fix the same bugs people fixed, 5, 10, 15 years ago?

## Clarity, Making it easy on your Brain

You end up reading code much more then writing code. With having the code formatted the same way in each and every file it reduces the cognitive load on your brain of trying to figure things out. It also removes the question when you are adding new code to a file of how to format it.

## Less Nitpicking on PRs

It removes the discussion in pull request reviews along the nit-pickier lines of where brackets should go, and when to add new lines, and how variables and functions should be named, etc. Also when you add a new file, which format should it go in, is no longer a question.

# Arguments Against

## High Risk, Low Reward

Sometimes when turning one rule on it will create hundreds or even thousands of warnings. The poor soul will then have to go all the locations and fix them all. QA hates these kinds of changes as they are low risk but can be stretched across the whole project. You can sometimes mob program these and split the work up across multiple people. Also you could edit the rules files to only apply the rule to specific files.

## Change History Investigation

If you are making large formatting changes to the code the argument is it will make it impossible to find out who made changes to what lines before the format. But, I hardly ever see anybody go back to figure out why someone did something 5 years ago.  

## Waste of Time

Isn't this just busy work? I really dislike this argument and view the points above to prove it's not.

## Customer Benefit

This is a tough selling point to a product manager, so I'm going to change the source code around and not produce any new functionality, but potentially break existing functionality. I've found trying to make the changes as small as possible, has been really helpful. Saying the task is going to take half a day is a lot less intimidating then saying a week. Also partially doing this work as a part of other tasks is a strategy I've seen been successful. For example, when you are changing a file, you fix all the warnings in it.

# Conclusion

A small project at work I was on many years ago had about 5000 lines of code and as team we ended up adding a bunch of additional checks when we were compiling. This really helped everyones productivity and made the code base feel like it was ours as a team. Not a bunch of individually owned components put together to create a product. This also made it easier to onboard new team members. I really think it's a great idea to have tools running and ready waiting for the day to be turned on and help you writing cleaner code.
