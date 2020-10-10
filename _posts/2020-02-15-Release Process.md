---
title: "Release Process"
published: false
---

How we Released the iOS App at TextNow

When I started in December of 2017 on the iOS team at TextNow we did releases at best once every two weeks and had a Jira Confluence doc explaining how to do it. It was very daunting and intimidating to do a release. There were many steps with long terse sometimes conflicting descriptions. I appreciated having the documentation but it felt very intimidating to do. We were using Git Flow for our branching strategy. We used a Jenkins job that ran a local copy of Fastlane to upload a build to TestFlight. It was actually ignoring the Fastlane code in Git and copying over it's own!

After being lead through a release and doing numerous myself I started to understand all the moving parts necessary to do a release and it's not as overly complicated as I originally dreamt it up to be.

# Diagram of the following

Essentially the steps were to cut a release a branch off of master calling it release/Y.X, setting the new version of the release, then pushing that up to GitHub. After it was in GitHub you would run the Jenkins jobs to create a debug and release build which were sent off to the external testing team. After the testing team came back local QA went over the results and would work with the team to decide if the bugs were release gating. If the release was good another Jenkins job was ran which pushed a build up to Testflight where the build would pushed out to a group of internal and external testers. Then after about a week if there wasn't any Testflight feedback and Crashlytics looked good we would take the Testflight build and start the app store release process with it. After Apple approved we do a phased 7 day roll out. All in all from the time the build was cut off of develop and the build was released to the app store it took about a week.

Over time we smoothed out this process by moving away from Git Flow to Trunk Based Development.

Trunk Based Development to Octopus merging.
