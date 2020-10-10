---
title: "Why we picked SwiftLint"
published: false
---

I'm a huge fan of clean code and have seen at many places I've worked how it helps make dealing with the source code easier. In the past at places I've worked we've used [CheckStyle](https://checkstyle.sourceforge.io), [PMD](https://pmd.github.io), and [FindBugs](http://findbugs.sourceforge.net). I always pushed to have more rules turned on. Not all the rules and looking back it was a litte overkill in some circumstances, especially those around documentaiton comments, but that was 15 years ago.

So why did we pick to use [SwiftLint](https://github.com/realm/SwiftLint)? It came down to we had a code base with alot of legacy code with nearly no unit tests. Many people had wrote code in the code base over short periods of time. I think the longest tenured person was about two and a half years. This meant there were many different styles of code wrote and many different areas nobody had any clue what was going on. Well an easy way to become familiar with those areas was to clean up the code. By turning on SwiftLint this would allow us to clean up the code and understand it a little better.

How'd we go about turning on SwiftLint? We first turned it using Cocoapods and had the default rule set. This produced hundres of errors and thousands of warnings. After some tuning (disabling) of the errors and warnings we got it down to an approachable amount. Then as a team we tackled the errors so we could turn SwiftLint on. The warnings were in categories that were logged in our bug tracking system and then put in our backlog. Over the next year these warnings were fixed and when they were enabled as errors. This greatly helped from new hires accidenally adding more warnings.

What was the benefit of this? We ended up with a unified, cleaner code base in which everyone helped out on. This made the code feel owned by the team in the teams style. Later we turned to SwiftFormat to make the layout of the code identical throughout the codebase.

This strategy we ended up using greatly helped the developers. Project Management was cool with it too becaue we didn't stop new feature development or bug fixes but were able to do it peace-meal and slowly but surely make the code base better. Also with turning warnings into errors this made sure we didn't slide back either. We also eventually changed it so in Xcode it would only show you the warnings for the code you touched. Originally were were going to set this as an error, but it was too cumbersome with false positives. I strongly recommend setting your project up with SwiftLint and turning up those warnings.
