---
title: "What is Calabash?"
published: true
---

![](https://upload.wikimedia.org/wikipedia/commons/a/a2/Courge_encore_verte.jpg)
It's a veggie!But more importantly for BDD it's a mobile cross platform testing framework used with Cucumber to allow for automation on both Android and iOS.Currently I'm focused on learning Calabash-iOS so I thought this would be a good time to write an article about exactly what Calabash-iOS is.Let start by going over the steps about how it works.+ In the Cucumber world you write features that are parsed by a Ruby library+ The library calls the appropriate framework to execute the tests, in our case Calabash.+ Calabash then uses JSON to talk to the HTTP server running on the device.+ The server then translates the JSON to comamnds.
+ The Calabash app then talks to your app.+ The results are then passed all the way back to the client

Or in picture form![](https://image.slidesharecdn.com/calabash-131223002917-phpapp02/95/calabash-for-iphone-apps-4-638.jpg?cb=1387758704)My goal is to write tests for a Swift iOS application.# Summary

Well not soon after I started writing the blog post above I got hired as a Senior Automation Engineer and the team had recently retired using Calabash. So I didn't end up using it :(
