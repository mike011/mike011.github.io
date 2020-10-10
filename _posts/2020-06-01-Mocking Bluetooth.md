---
title: "How we added testing to our Bluetooth Layer"
published: true
---

We had a ton of of logic in our Bluetooth layer with very few tests, and some time before the next set of requirements was going to be asked for. So as a way for me to learn and potentially better structure the code, I tasked myself with helping fill in the missing unit tests. The Bluetooth layer was the most exciting and interesting layer so I dove right in. Well the first huge problem I ran into was that every object from the iOS CoreBluetooth framework could not be initiated. We relied directly on classes and wanted to instead use protocols to allow for easy mocking to make it possible to unit test. I remembered a simple trick. Here is an example of the steps we went through. You start by creating a protocol for the class you want to mock and override any fields or functions your implementation needs.
```swift
public CentralManager {
	var status: CBManagerState { get }
	func connect(_ peripheral: CBPeripheral, options: [String : Any]?)
}
```
Then you add an extension to the class you could not init to conform your class to that protocol
```swift
extension CBCentralManager: CentralManager {
}
```
Next up is to change your implementation to use the protocol. And now you can create a mock.
```swift
public MockCBCentralManager: CentralManager {
	var status: CBManagerState = .poweredOn
	func connect(_ peripheral: CBPeripheral, options: [String : Any]?) {
	}
}
```
Finally in your unit test you can now inject the mock and be able to use the mock to verify the correct behaviour. This is great for when your class doesn't expose much, the mock can really help make sure the correct functions or variables are being changed or called. Also for the iOS simulator you cannot interact with Bluetooth. So this helps keeps the unit tests isolated and running super quick.

Thanks for reading this article. With this approach we were able to quickly ramp up the tests for our Bluetooth layer. We are hoping to use this in the future to inject data for integration tests. Only time will tell.
