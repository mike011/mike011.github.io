---
title: "Core Data versus SQLite"
published: true
---

Recently on my new team we had the discussion about should we use SQLite or Core Data going forward. The code has a mix of the two storage types and we want to consolidate onto one moving forward. This article is a summary of the pros and cons of each type.

# Core Data for the win

Apple has been pushing this platform for years and is very well supported, mature, and widely used. You also get the benefit of only having to worry about objects and the nitty gritty details. You also have great Xcode support including a UI to add, modify, delete, and update your current data model. Also going to a new version is trivial.

# SQLite is powerful

You have a clear view into exactly what is happening in the database. This makes it obvious when something goes wrong where to fix the issue and less of the system trying to help you. This approach is also very flexible, you could have the same database schema for an Android, desktop, or web app.

# Core Data has drawbacks

When something goes wrong with Core Data it feels like you are looking at a black box and it can be very difficult to figure out the root cause of the problem. Recently we changed our database model and forgot to bump the version. This caused the database to have to be regenerated from scratch. It wasn't obvious from the logs or calls why this was happening.

# SQLite has drawbacks too

"With great power comes great responsibility" is a famous quote and this is how I feel about SQLite. You have so much control over what you are doing, but the consequences of those decisions could be really painful. Also you'd have to worry about things such how to structure your data to make queries as efficient and narrow as possible. And most places I've worked use Core Data an job requirements I've looked at ask for it, so when hiring new developers they'd more likely have experience with Core Data then with SQLite.

# Conclusion

We are still in discussions, I need to spend so more time figuring out exactly what Core Data is doing and what SQLite is doing to better come up with my own opinion. Also given the legacy nature of the app I'm working on a solution could be years in the making, or never happen, and that's fine. Sometimes it's not worth the effort or it's just better for you to spend your time on other more pressing manors. That being said having one storage type would simplify things going forward. So really it's all about costs and benefits.
