---
title: "Cucumber Anti-Patterns"
published: true
---


- If you came back the Gerkin 6 months later, or even a month later would you still understand what's going on? Is there not enough details? Is the wording not consistent? Is there not enough descriptions about what is going on? Is there too much details making it hard to understand what is going on?

- This is why it's so important that the 3 amigos meet together so they can hack out a common vocabulary. This will make dealing with subtle bugs much for obvious and understandable for all involved.
- The scenario will be more complicated then needed and subsequently harder to maintain.

- Given: When I at the user login page
- And: When I type my username
- And: Enter my password
- And: Click login
- And: Go to the calculation page

A more concise scenario would read:

- Given: I am at the calculation page.

All the magic of logging in and getting to the correct page could be wrapped up in the one call. The focus on the steps is making them as business readable as possible. So this means in your lower levels you will have various methods simply calling other methods.

- Given: I open the app
- When: I give the correct input
- Then: The correct output is shown

- This doesn't say anything useful and is the opposite of containing too much information.
- This scenario needs to have more detail added to it.
- The steps needed be pulled out into a more business readable format.
- Who ever didn't write the scenarios won't care about them. This provides less value to the team and you will end up missing many important scenarios because of it.
- When was the last time the scenario failed? If the scenario has never failed how useful is it?

### A Lot of Scenario Outlines
When you end up with a long list of possibilities in your scenario outlines chances are have combined multiple scenarios together. These should be split up.
- Folders could be used to partition out major parts of the product.
For example if your test setup always has the same steps for many tests. Is it really necessary to do those same steps over and over again?