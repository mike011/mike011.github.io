---
title: "Alamofire Retry Policy"
published: true
---

[Alamofire](https://github.com/Alamofire/Alamofire) has an awesome feature called [RetryPolicy](https://alamofire.github.io/Alamofire/Classes/RetryPolicy.html). This is one of the reasons why you'd pick Alamofire over using a plan old URLSession. RetryPolicy intercepts requests so that it can provide the ability to automatically retry when a request fails.

RetryPolicy uses a fancy thing called exponential backoff. Exponential backoff is when every subsequent attempt will be spaced out a little farther then the previous attempt. This is great for when a connection goes down and stops you from hammering away at the server. This would effectively be doing a Denial-of-Service(DoS) attack by preventing the server from coming back up as it would be flooded with the pile of requests created.

In Alamofire exponential backoff has two variables that can be configured. They are ```exponentialBackoffBase``` and ```exponentialBackoffScale``` and are used in the formula (exponentialBackoffBase) <sup>(retryCount * exponentialBackoffScale)</sup>. By default the base is 2 and the backoff is 0.5. And the result is in seconds.

![](/assets/RetryPolicy/RetryPolicy.png)

As you can see from the graph the amount of time waiting for the retry quickly increases. At 15 retries it's going to wait for 30 minutes. Better remember to keep those objects alive.

For RetryPolicy there is a ton of default behaviour provided for you such as what http methods are considered retriable, what http status codes should be retried, and as previously mentioned the base, and the scale. You can even specify a retry policy not just per request, but even one for the whole session. For the Session how it works is when you create the Session you specify the retry policy. The default retry policy will most of the time be sufficient. But you can specify a ton of variables and parameters if you want. If instead you want to specify a retry per request you just pass it in when creating the request.

One interesting thing I found out while fiddling around was setting the amount of times the retry policy would try, disconnecting my wifi, and then finding out what happens if they all fail. Well it's pretty straight forward, the closure is called only once at the end for the failure.

This has been a short overview of how RetryPolicy works for Alamofire. It comes jam packed with a bunch of options, but most of the time the default behaviour should be sufficient.
