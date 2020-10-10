---
title: "Why we moved to CircleCI"
published: true
---

When I was on my last team as an iOS Software Developer we used Jenkins backed by Mac build minis to build our iOS app. Jenkins was picked because every other team in the organization used it. We had a dedicated DevOps teams handling the maintenance and up keep of the servers. This solution worked great for us when I started on the team. We had about 4 iOS developers and about 3 build machines. Not much emphasis was put on using the build machines so our build process was quite simple and we were only creating an ipa. This took around 35 minutes.

Over the time I was on the team it grew to over 10 iOS developers and we added more projects to build and more ways to build those projects. So our build time went up dramatically, of course it reared its ugly head when we were getting ready for a release or when we were completing a sprint. Worst case build times got up to over 6 hours because of queuing and rebuilding. This was completely unacceptable. We also introduced two tiered PRs which further worsened the problem.

DevOps made it there quarterly goal to bring down our build time to an optistimic 20 minutes. They investigated purchasing more Mac build minis but with our projected team growth and project growth they were estimating they would need at least 20 more. This was unacceptable as they were trying to move hardware management into the cloud. So they started investigating cloud based iOS solutions. The biggest hurdle for iOS in general is that you have to build on Mac hardware. You cannot use a virtual Mac machine. There are also various different types of solutions. For example you could rent some Mac machines and ssh into them and do what ever you want. And then there were some nearly completely hands off solutions where you just specify your git repository. Eventually the DevOps engineer found CircleCI. It wasn't perfect and there will still going to be some tradeoffs.

# Why to move?
- In terms of billing, you pay for the amount of time you use the build servers for. This incentivizes the team to make the builds as fast as possible.
- Great documentation around what the options in the configuration yaml file do.
- Popular, meaning if you have a problem most likely someone else has had it also, making it easier to solve.
- It would make hardware management someone else's problem.
- "Infinite" scaling, so if a bunch of developers put up pull-requests at the same time the builds would not get queued one after another, but be ran in parallel instead.
- Because of the infinite scaling our build time would be the slowest build job which was around 40 minutes.
- Every time software upgrades were needed DevOps would not have to connect to the build machines and upgrade them. This would've been especially problematic if we went to 20+ machines.

# Why not to move?
- This was not the CI system the rest of the company was using and iOS was already looked upon as an odd duck. This would only further that perception.
- It would be difficult to access private tooling. We were in the process of adding UI tests that needed different types of accounts. This required us to use some private APIs only accessible while securely tunnelled in. This wasn't realistically possible for us to do with CircleCI.
- Of course paying for CircleCI was going to be a drawback. Would the time saved paying for someone else taking care of it be less expensive then us doing it ourselves?
- The CircleCI configuration file was already pretty long when it was initially set it up (around 350 lines), and there was no obvious, simple path to take to split that up. There were lots of functions called that could have be placed in separate files. Yes, there are orbs, but that seemed overly complicated.
- Yes, we had a point of contact at CircleCI to talk to when issues came up. But this far worse then just slacking a DevOps person and ask them for help fixing it.

# The Decision

Even with the reasons not to move, the positives far out weighed the negatives and we transitioned over to CircleCI. It was great having so many more build machines available for pull-requests. You never had to wait hours for the build to complete.
