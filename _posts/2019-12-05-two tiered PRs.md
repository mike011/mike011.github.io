---
title: "Two Tiered PRs"
published: false
---

When a new [developer](https://www.stencia.com/blog) started on our team he proposed we chagned how we do our pull-request reviews.

#Old System

We had being doing one pull-request review for every feature, chore, and bug fix. This had to have two reviewers, one developer and one QA. This allowed the developer to review the code and the QA to test the PR before it got into master. This worked great when the team was small as it kept mastre stable. QA was able to test just what was in the pull-request and the developer was also able to review a small amount of code. The drawbacks came when there was developer feedback or QA feeeback that fundadmentally changed the PR. This would waste the other person's time if they had reviewed it becuase now they'd have to review it again. But this was pretty rare.


#Proposal

It was proposed we would start having multiple pull-request reviews. Developer only ones into an intermediate branch and developer and QA reviews into master. For example for a feature branch that would give us the ability to have longer running branches. Not really long, like a sprint or maybe mulitple sprints. So we could have developer only reviews into the branch. The code reviews code be kept really small and focused. And when the feature was ready a pull-request into master would be created that would have one developer to review the commit message and one QA to test the completed feature. We agreed as a team to try this out and it went pretty smooth adopting it, so we decided to keep it.

#Several Months Later

So after trying this out for a while we found some parts we really liked and other parts that weren't as nice. For example some developers would put up really small reviews and expected near instaneous feedback as they would be blocked on doing more work until the review was done. This would break the flow of the other developers doing there work. There was also the opposite problem that this gave some developer the ability to spend days on a PR before putting a review. So you end up with this large review you end up rubber stamping. With having more reviews meant more builds on the CI system, this cost the company more money. We found some way to save money on this but, fundamentally we were building more.

Also some feature branches were around longer then I was comfortable with. I'm a big fan of getting the code into master as quick as possible and hiding it behind a feature flag. But the team preferred not having dead / not fully tested code released. All in all these
were minor issues and we ended up staying with this system.

For smaller stuff like a simple configuration file fix or improvement this process seemed overkill, but we valued being consistent across all types of branches over instead of each one having it's own rules.

#Summary

This really helped developers focus on the code and QA focus on testing in the second review. It definitely was a net win.
