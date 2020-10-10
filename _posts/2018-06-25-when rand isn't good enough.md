---
title: "When rand isn't good enough"
published: false
---

When I was at my previous employer I had the opportunity to implement the usage of a new library into the ap. This meant adding some new calls into your app and adding the library via Cocoapods.
The most important part was we had to be 100 percent sure that we only sent one request out a very small percentage of the time. This was a high volume call and we were going to be charged hundreds of thousands of dollars if this call went crazy. I needed to figure out a strategy to guarantee this behaviour.

The simplest strategy and for what has worked in the past was that
successful calls would be determined by a dice roll. The dice roll generated a number between 1 and an configurable number, if the roll was 1 is succeed, else it failed. Seemed pretty straight forward so added an Int.random(in: 0...max) call and called it done. But I wanted some unit tests to be sure my assumptions were correct. So I wrote a test which would call the function a ton of times expecting only a maximum amount of passes. This is what that code looked like.

```swift
func testDiceRoll() {
    // Arrange
    var passed = 0
    for _ in 0..<500 {
        // Act
        if diceRollSucceded() {
            passed += 1
        }
    }

    // Assert
    XCTAssertTrue(passed >= 0, "There should be more then zero results")
    XCTAssertTrue(passed <= 10, "There shouldn't be more then 10 passes, there was \(passed)")
}
```

 But it failed, there were way more passes then I was expecting. So I Google searched and couldn't find anything helpful. So I looked into more complicated random functions. I ended up landing on [GKShuffledDistribution](https://developer.apple.com/documentation/gameplaykit/gkshuffleddistribution). What was great about this choice is that the distribution would be uniformly distributed across the values, which as I found out rand is not. So the problem with rand was the values were clustering too much around the value of 1 causing too many passes. After I replaced the code, the test passed. I even bumped the max from 500 to 500,000 and it still passed. Finally I had the confidence that this function was stable and it wouldn't have too many positives. This was great to have the comfort and security of the unit test to ensure I wasn't going to cost the company oodles of money.
