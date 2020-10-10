---
title: "How We Reduced our Build Time Warnings"
published: true
---

When I started on the iOS team at my previous employer our main project had a reputation for having an absolutely ludicrous amount of warnings in it. Even the CEO had commented on how bad it was. Important note, he was the creator of the app. We had over 35,000 warnings. It was so much noise that when compiling in Xcode and when looking through the log files made it took much harder to do anything. We all found that this was a huge annoyance and wanted to fix it, but at the time were were a small team of 4 iOS devs. And we were being way too ambitious for what we could get done for our sprints. So the warnings stayed at the 35,000 mark for many months.

By luck a break through came and it was the fact that when we were compiling our CocoaPods project they were contributing the lions share to the warning total. CocoaPods has a flag that you can turn on to disable showing warnings, but we were overwriting it to show all the warnings. After fixing that the warnings dropped to under 5,000. Still a lot but much, much better.

The next big discovery was that one CocoaPods project was producing a large majority of the remaining warnings and this project should've had it's warnings ignored. After some great investigation done by one of the Ads developers he found that when we imported the framework in the pch(pre-compiled header) file the warnings were not ignored, so after adding a "pragma clang diagnostic ignored" around the header the warnings dropped another huge amount to under a 1,000. 35 times less then when I started.

We now had a list of somewhat legitimate list of warnings. A great piece of information was added around this time that in a Pull-Request the amount of warnings was now shown. This was great as we could now see on a PR by PR basis what the warning count was. Jira tickets were also created to investigate all the categories of warnings shown in Xcode and fix them if it was easy and spin off more Jira's if it was not. One of the Co-Ops then took it upon himself along side one of the growth team developers to tackle these. They were able to widdle the list down to around 600.

It was great to have warnings in each PR but it was dificult to tell on a PR by PR basis how they were changing. I took it upon myself to write a new tool to compare them. This tool produced a html table stating which new warnings were added and which ones were fixed. Now no one had anymore execuses to be adding warnings. This helped our warning total get under 200.

And that's a quick recap of how we as a team drastically brought our warnings count down to a reasonable level. The remaining warnings looked to be tricky to fix and required expert knowledge in some deep dark corners of the codebase. It was so much nicer worked in a cleaner code base. Investigating compile time failures on CircleCI and in Xcode was much easier. And not seing the constant stream of visual warnings in Xcode was awesome.
