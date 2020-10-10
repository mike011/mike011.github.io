---
title: "The importance of a solid CI pipeline"
published: true
---

I've worked at multiple software companies and have seen how they treat there CI pipeline. It's been interesting to see how it can really help or hinder in developing code. This blog is a summary of those experiences.

# What happens when people don't care?

- Build failures are ignored as being CI issues. So the build always fails so no one cares, so why both even investigating it, it will just fail for a new reason. This is a pretty pessimistic view, but I've worked with teams in this rut.
- Lots of developer time is waisted trying to build. You never know did I break master or was master already broken and you have to spend hours looking into when it last built correctly and what has changed since then.
- There is a lot of well it works on my machine. Maybe that person forgot to push a file, or didn't a pull another file that is breaking the build, or they have a perfect set of compatible libraries on there computer.

At the end of the day it's chaos and you might as well not be running any CI as it's not providing any value.

# Steps to start with

When working on teams that were having problems these are some of the strategies we as a team took to make things better.

- Make the build job as simple as possible. Sometimes people will overcomplicate a build script or make it do a lot of things. What's better do a lot of things and fail a lot or do a few things and pass a large majority of the time? I would lean towards the last as it provides values to everyone when the build passes consistently
- Make it robust and when it fails as obvious as possible. You are never going to get a build that will pass 100% of the time. CI's just aren't there as there are too many reasons it can fail. So the best strategy is to provide informative logging at critical points so when the build fails the logs will provide helpful information making solving the issue easier.
- Make sure the build passes for a set period of time. This is similar to what you want for tests. You want it to pass not just once, but a large majority of the time. Run the build job over and over again. Make it as simple as possible.
- Then with team buy in make that job mandatory.
- Help out whenever there is a failure to make sure the first time the build fails the mandatory flag is removed because "it was a CI issue"
- Work with the team to identify other points that the CI could help with. This includes steps such as linting, formatting, running tests, error log reporting, and build asset creation
- Slowly over time add more and more. This greatly helps raise the quality of the product you are delivering is that you now have a safety net of jobs that have to pass all the time.
