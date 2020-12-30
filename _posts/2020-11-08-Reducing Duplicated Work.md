---
title: "Reducing Duplicated Work"
published: true
---

I'm currently working on the SDK team at IMS and we are working on how can we work more efficiently. One really interesting problem we are trying to solve is how can we reduce the amount of duplicated work we are doing. Currently we have two apps we maintain, a private app that was originally meant for integration testing and a public app meant to show customers how to use the APIs we produce. Over the years the line between these two apps has blurred considerably to a point now were they are virtually the same. This seems like a prime candidate to reduce our duplicated work by providing only one sample app, but there are various hurdles for us to overcome in order to make it happen.

# Hurdle 1 - Private info

Our integration app has baked into it various keys and values that we use when testing the app. We don't want these in the external app / shared in our public repo. For the public app they keys and values have to be entered every time you do a fresh install. It has been suggested that we could put those values out in there own repo and not publish it. Then have a public empty repo that doesn't have the values. This has not been tried as of yet, but seems like a possible solution.

# Hurdle 2 - Private Frameworks

The frameworks we share with our customers do not have the source code and instead imports the binary modules. When we are building these frameworks internally we have all the source code. So in order to create a unified project we would have to change the frameworks the project uses from the local version to the built version. I think this is possible with Swift Package Manger, but am not 100% sure. More investigation is needed her.

# Hurdle 3 - Manage the transition to SPM

Our team in the process of moving to to SPM. The project historically used Carthage. This might make it easier for the internal dependent frameworks to swap out the internal frameworks as binary modules so we don't expose any internal source code. More investigation is needed here too. Probably be best to create a sample project and see if it works.

# Hurdle 4 - Getting Project Management to Buy into the identical

Yes, this will make us faster in the future, but it's hard to sell this to a Project Manager. We've struggled to get it prioritized over new feature development and bug fixes. Various team members have pointed out a couple of instances were we spent a bunch of time working on both apps and it would've been faster to just do one, but it wasn't significant enough to have the priority of getting this done bumped up. Honestly, this ends up being somebody tackles on weekend or downtime or never gets done. It's perfectly normal for things to not get done, the list of things to do for most companies is infinite.

# Hurdle 5 - How is testing going to be done?

Obviously we should test the unified app with the public and private frameworks, but how often? How are we going to inject the private keys and values for testing. How will this truly replicate how the framework is being used in the real world?

# What to do?

This is still in the planning stage and is viewed as low priority. It's currently easier to patch both apps then merge them into one. I'm hoping one day there will only be one app. This all might be a moot point as the possibility of using one of the internally developed apps as a test app has surfaced. And this might be an easier course of action then trying to merge the two apps.
