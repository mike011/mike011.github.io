---
title: "What is Calabash?"
published: true
---



 In the Cucumber world you write features that are parsed by a Ruby library
 The library calls the appropriate framework to execute the tests, in our case Calabash.
 Calabash then uses JSON to talk to the HTTP server running on the device.
 The server then translates the JSON to commands.
+ The Calabash app then talks to your app.
 The results are then passed all the way back to the client

Or in picture form

Well not soon after I started writing the blog post above I got hired as a Senior Automation Engineer and the team had recently retired using Calabash. So I didn't end up using it :(