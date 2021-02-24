---
title: "How we improved our Code Coverage Numbers"
published: true
---

# Introduction

This is a story of how at a previous company we took our iOS code coverage from under 10% to around 50%. The app had been in the App Store and actively developed without having a signficant amount of tests for 8 years, so there was tons of challenges involved.

When I started working on the app we didn't even measure the code coverage. So the first thing was to massage in the necessary steps in the CI and found out the code coverage was about 8%. This was depressing, especially as a believer in the benefits of having a parachute of tests above you. So many holes, not feeling confident about the changes I made at all. One big reason was developers looked at this small number and thought why bother, it's so low I can't make a positive difference, where to start, it's hard to write test, it takes too long, I don't want do it, it's not needed, it's not a priority, it's not worth the effort, the tests won't catch anything, etc...

On the brighter side the coverage number did slowly creep up quarter by quarter. This was mostly helped by new developers that joined the team who were interested in writing tests. It also helped that as we updated features we removed old untested Objective-C code. But still the coverage only got to around 25%. Which was an amazing accomplishment and well earned, but still not enough to plug those holes in the parachute.

It's important to note that we, as the developers were driving this number, not management. There was some talk about 95% coverage, but obviously that was totally unrealistic. Thankfully it wasn't pushed or mandated or we would've started writing tests to solely improve coverage, instead of testing the logic of the code.

# Improvement Strategies

When talking to some other developers the idea came up to only make the code coverage only reflect what we thought was testable. What's the point of showing coverage for code that we never intending on testing? Listed below are some of the types of changes we did to get the coverage higher.

## Ignored ViewControllers

This was probably the most controversial as we had a lot of classic Massive View Controllers sitting around that did all the things. Many parts of these classes could've and should've been tested. But the cost of trying to add tests to these classes was really high given how tightly coupled everything in the files were. We were planning on in the future to not extend them, but create new testable classes to replace them with.

## Ignored Views

Similar problem to the ViewControllers with doing way more then they were supposed to. But this was about improving going forward and views should really only contain view logic code which can be tested manually or by UI tests.

## Ignored All Objective-C Code

All new code was in Swift which would mostly have unit tests. We wanted this code to die and spend as little time in it as possible.

## Ignored All Third-Party Code

We had manually copied various libraries into our codebase because we had to make changes to them or they weren't actively supported anymore. So we would ignore these files. Not the best plan in my opinion.

## On a per PR basis make it Obvious How the Code Coverage Changed

A comment was added to the PR showing the code coverage in main versus the developer's PR. You could click into a split view showing the exact differences between the files in the pR and in main. This was great to add tests for areas you 'forgot' too. See the [CodeCoverageCompare](https://github.com/mike011/CodeCoverageCompare) tool for how that was done.

## Trending on a per Quarter Basis of How the Code Coverage was Changing

This was helpful for summing up the quarters efforts and as they went up motivating the team to keep them going up.

## Splitting of testable chunks of the codebase

All of our backend service calls were in Objective-C and written in a tightly coupled fashion. This made it very difficult to add a test without calling the backend. The level of effort to fix this code was super high and instead of trying to translate the code into Swift the decision was made to rewrite it in Swift. This new project was lead by a senior developer who was very passionate about testing and pushed the coverage numbers in the 90%.

# Conclusion

As you can see we implemented many different strategies to get our code coverage numbers higher. This helped this number represent the current state of the codebase instead of over the whole history of it. We still had lots of coverage to gain, but the number was slowly creeping up when I left the project.
