---
title: "Automation vs Manual Testing is the wrong conversation to be having"
published: true
originally posted: https://www.utest.com/articles/automation-vs-manual-testing-is-the-wrong-conversation-to-be-having
---

Most people I have worked with think of these as two different ways of testing, but I don't think they should be seen that way. Automation is not able to fully replicate what a human being can do and a human can't 100% replicate what a computer does. So instead of thinking of these two things as enemies, why can't they help each other out?

Let's go through an example for something as simple as clicking a button:

* Automation will be able to figure out if the button was pushed, what happened next, how long it took, what happens if you clicked the button many times over a short period of time.
* A human could tell you, did the button look good, was the experience pleasant, was there anything weird/funny/ugly going on the UI when you clicked the button, was the layout of the button correct, was the button easy to click on,

As you can see the capabilities of both approaches overlap which is a good a thing. Automation can help with manual testing, it can do all the boring stuff for you and allow you more time for testing new areas. Continuing the example above.

* Automation could be run on every build of the product giving you a basic feel that the button is working correctly.
* A human could infrequently check the button to make sure that the experience is still pleasant.

So next time someone asks you about automation vs manual, think more what they can do for each other, rather than pitting them against each other.
