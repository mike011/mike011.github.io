---
title: "Mono Repo for the Win"
published: false
---

This is a quick article about how having one repository contain multiple projects for our team was a win.

When I started on the iOS team at TextNow we had multiple repositories that were used to build our main project. We had a phone, messaging, assets, and the main repo.

# The Good

If you wanted to do some project specific work it was quick and easy to do. You just needed to open that project and get your work done. The compile time was great and there was even a small set of unit and UI tests.

# The Bad

We used commit hashes to tag the repo so the main repo knew what to use. This was confusing and easy to break, especially when you tried to rebase changes back into master.

# The Ugly

The worst problem was that we didn't have a clean separation between the modules and this overlap made some pretty nightmare commits where you had to open two PRs, one for the framework and one for the main repo. Then you had to hope nobody else put in any conflicting code while you did this as it would break your PR. This was really cumbersome and really brought our productivity down.

# The Solution

We were a super small team of 4 devs so we rolled all the code into one a repo. This worked great as we no longer needed commit hashes to tag the repo at a specific version or multiple PRs when effecting the framework and main repo.

# Conclusion

One repo for the win. This was great. But why? Really the seperate project could've worked but because the project code was not cleanly seperated from the other projects it didn't work. If we would've used VIPER or RIBs it would've made this possible.

# Fast-Forward

The team grew and grew and eventually a new services framework was created. This had a beautiful protocol layer which kept each side cleanly isolated from each other. So this was pulled out into it's own Carthage framework and pulled in at a specific version number.
