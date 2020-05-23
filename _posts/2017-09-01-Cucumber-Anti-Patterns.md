---
title: "Cucumber Anti-Patterns"
published: true
---

I stumbled upon an awesome [podcast](https://cucumber.io/blog/2016/05/09/cucumber-antipatterns) from the Cucumber guys about anti-patterns and have wrote my own summary about what they've said.### If the Gherkin is hard to understand it is bad documentation- If a person not on your project reads your scenarios and cannot explain back to you what it means, you've got a problem.
- If you came back the Gerkin 6 months later, or even a month later would you still understand what's going on? Is there not enough details? Is the wording not consistent? Is there not enough descriptions about what is going on? Is there too much details making it hard to understand what is going on?
### Writing the scenario after you've wrote the code- One big thing pushed for in BDD is creating a ubiquituous language. This is a set of commons words used between the three amigos(Business Person, Developer, and Tester). If the code and tests are wrote first then there is a good chance that you will have three different vocabularies used. This will make communication difficult between the three amigos.
- This is why it's so important that the 3 amgios meet together so they can hack out a common vocabulary. This will make dealing with subtle bugs much for obvious and understandable for all involved.### The scenario title contains too much information about what the lower level details in the scenario are doing- When the scenario is changed, chances are the title won't be updated, so the title will quickly become out of date.- The title needs to be wrote at a high enough level to convey it's meaning, not too little detail to make it overly generic and useless, and not to much detail making it difficult to change.### Rambling long scenario with too many (10+ steps)- What the essence of the test is lost in details.
- The scenario will be more complicated then needed and subsequently harder to maintain.- A scenario should only contain steps that are related and cannot be split out. If you can split them out, make multiple scenarios.### Too many incidental detailsFor example you want to check a calculation on a system where you need to log in first. An cumbersome scenario could have the following:

- Given: When I at the user login page
- And: When I type my username
- And: Enter my password
- And: Click login
- And: Go to the calculation page

A more concise scenario would read:

- Given: I am at the calculation page.

All the magic of logging in and getting to the correct page could be wrapped up in the one call. The focus on the steps is making them as business readable as possible. So this means in your lower levels you will have various methods simply calling other methods.### Not enough detailsExample:

- Given: I open the app
- When: I give the correct input
- Then: The correct output is shown

- This doesn't say anything useful and is the opposite of containing too much information.
- This scenario needs to have more detail added to it.### Too many given/when/then statements- The person has wrote a test and not documentation.
- The steps needed be pulled out into a more business readable format.### The scenarios are created by not all of the three amigos- If a business person creates the scenarios chances are the then step will contain impossible assertions.- If a tester or developer creates the scenarios they will be too low level and not be understandable by the business person.
- Who ever didn't write the scenarios won't care about them. This provides less value to the team and you will end up missing many important scenarios because of it.### Scenario doesn't provide any useful information- These types of scenarios are normally added early on in a project when you are just starting to stitch together some basic components. But once the system becomes more complicated they are no longer providing as much or any value.
- When was the last time the scenario failed? If the scenario has never failed how useful is it?- Ways to deal with the scenario are you could remove or enhance or push it down to a lower level.### Slow Scenario Outline testsMost of the time when you end up with a bunch of scenario outline tests that are shown on the UI, the UI is not what you are testing, the logic of the combinations of the tests are, so you should use the UI as little as possible. Just because you wrote a scenario doesn't mean it has to use the UI!

### Alot of Scenario Outlines
When you end up with a long list of possiblities in your scenario outlines chances are have combined multiple scenarios together. These should be split up.### Letting your Scenarios take longer and longer as you add more and more of them- Tagging and folders are the best to reduce the tests being ran without adding to much uncertainty into the quality of the product.
- Folders could be used to partition out major parts of the product.- A feature tag could be introduced to only run the current feature being worked on.- To decrease the continuous build machine runtime a smoke tag could be introduced to run on each build. Then what is not tagged could run overnight.### Testing the same thing over and over again
For example if your test setup always has the same steps for many tests. Is it really necessary to do those same steps over and over again?Sourced from:- [Cucumber Anti-Patterns - Cucumber Podcast](https://cucumber.io/blog/2016/05/09/cucumber-antipatterns)- [Cucumber anti-patterns (part one)](https://cucumber.io/blog/2016/07/01/cucumber-antipatterns-part-one)- [Cucumber anti-patterns (part two)](https://cucumber.io/blog/2016/08/31/cucumber-anti-patterns-part-two)- [Chapter 6 of the Cucumber for Java](https://pragprog.com/book/srjcuc/the-cucumber-for-java-book)- [Chapter 6 of the Cucumber Book](https://pragprog.com/book/hwcuc/the-cucumber-book)
