---
title: "Circle Saving Money"
published: true
---

This is a story of how we as a company reduced our CircleCI usage without sacrificing build quality.

# Background

Our team switched from Jenkins over to CircleCI because we went through a huge growth from 3 iOS developers to 10. This was overwhelming our Mac minis and instead of buying more minis it was decided we would move to CircleCI. With more developers came more projects and more unit and UI tests which meant longer buid times. This is primarily because we have a mono repo and when a dev puts up a PR everything was getting built. We also moved to a two tiered PR system which increased the amount of builds.

# The Problem

The company I worked for had purchased a set amount of credits from CircleCI and at the time it was forecasted to last us a year. CircleCI subtracts from the credits by how much time you use the build machine for. Per PR we were now getting up to over 4 hours of total build time. CircleCI contacted us and said that our credits where nearly gone. The first question from the Devops team was why were we going through so many credits? Easy answer was we were building more often. The next question was could we build less? I'm a big fan of making CI do alot of work so you have a really good snapshot of what the state of your projects are in. I didn't like this idea, but we couldn't think of any other reasonable ideas.

# Building When Not Needed

So I took a deeper look into exactly what we were building. I was pretty familiar with all the projects as I helped set most of them up, but hadn't looked at them all together. And a really important finding was we were building projects when there was a relastically a zero percent chance of them legitimally failing. I then created a tree diagram of the dependency mapping between projects. It looked like something like this.

![](/assets/Circle_Saving_Money/tree.png)

 And as you can can see if the parent project had a code change the child project shouldn't fail as all dependencies pointed down. So I wrote a new build step that would map the files in the pull request to the projects they would build. So when each project built it checked if it needed to build or it would early exit if it didn't. Unfortunatley given how jobs are configured in CircleCI I couldn't figure out a way to make it so the job wouldn't be called at all.

# Ruby

We needed Ruby in order for Fastlane to work. And one of the first steps of the build was to install all the gems needed for Ruby. Because CircleCI started from a clean build everytime there was no easy way around this. We tried caching the data for Circle but this took as much time as just installing the gems. This would take anywhere from 30 seconds to 5 minutes. So instead we stored all the Ruby gems in our repo. This added a ton of files to it, but saved us so much build time it was worth it. It also nailed down the build environment even further given that it was now guaranteed the same gems would be used. This wasn't perfect as build machine needed different gems then the local machine. So we were not able to run fastlane getting code coverage from the local machine anymore. No one complained about this, so it was an acceptable trade off

# Caching

Another thing that was done was to be very aggressive when possible with caching the contents of the build related files. Normally this would be faster then syncing from the repo. We added caching in as many places as possible. This really helped the post build jobs run really quickly. Or if the build had to be run again it would build much faster the second time around.

# Sync less

It was also investigated syncing only the branch from the repo as we had used this trick in the past in Jenkins. But this wasn't feasable as syncing from the repo is nested deep inside of CircleCI and if we wanted to customize it we would have really go against the grain of how CircleCI worked. So we stopped this effort.

# Summary

With these savings place our average build time came down dramatically to under 1 hour from 4. This also helped make the Pull Requests more focused on only the relevant builds. So when failures happened developers were more keen to investigating them.

# Follow Up

The DevOps teams wrote a credit monitoring system that would show show how many CircleCI credits where being used. You could filter by who and in what branches the credits were being used. This was great becuase it was planned to have a notification if our rate suddenly increased or became significantly above planned.
