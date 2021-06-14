# Migration to AEPTarget

This document is a reference comparison of ACPTarget (2.x) APIs against their equivalent APIs in AEPTarget (3.x) for an iOS mobile application implementation.

The AEPTarget extension is implemented purely in Swift and is compatible with the AEPCore swift SDK. To ensure a smooth transition from the ACPTarget SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application.  If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## Swift

### Public classes

| Type                   | AEP (3.x)        | ACP (2.x)               |
| ---------------------- | :--------------- | :---------------------- |
| Primary Class (Module) | Target           | ACPTarget               |
| Class                  | TargetRequest    | ACPTargetRequestObject  |
| Class                  | TargetPrefetch   | ACPTargetPrefetchObject |
| Class                  | TargetOrder      | ACPTargetOrder          |
| Class                  | TargetParameters | ACPTargetParameters     |
| Class                  | TargetProduct    | ACPTargetProduct        |

### API usages

{% tabs %}
{% tab title="AEP (3.x)" %}

**clearPrefetchCache**

```swift
Target.clearPrefetchCache()
```

**clickedLocation**

{% hint style="info" %}

The API is named `locationClickedWithName` in the ACPTarget SDK.

{% endhint %}

```swift
Target.clickedLocation(_ name: "mboxName", targetParameters: targetParameters) 
```

**extensionVersion**

```swift
Target.extensionVersion
```

**getThirdPartyId**

```swift
Target.getThirdPartyId({id, err in
    // read Target thirdPartyId
})
```

**getTntId**

```swift
Target.getTntId({ id, err in
	// read target's tntId        
})
```

**prefetchContent**

```swift
Target.prefetchContent([
	TargetPrefetch(name: "mboxName1", targetParameters: TargetParameters1),
	TargetPrefetch(name: "mboxName2", targetParameters: TargetParameters2),
	],
	with: globalTargetParameters
	){ error in
		// do something with the callback response
}
```

**registerExtension**

{% hint style="info" %}
Registration occurs by passing `Target` to the `MobileCore.registerExtensions` API in addition to the other extensions registered.
{% endhint %}

```swift
MobileCore.registerExtensions([..., Target.self])
```

**resetExperience**

```swift
Target.resetExperience()
```

**retrieveLocationContent**

```swift
let request1 = TargetRequest(mboxName: "logo", defaultContent: "BlueWhale", targetParameters: TargetParameters1) 	 { _ in
		// do something with the received content
	}
let request2 = TargetRequest(mboxName: "logo", defaultContent: "red", targetParameters: TargetParameters2) 
	{ _ in
		// do something with the received content
	}
Target.retrieveLocationContent([request1, request2], with: globalTargetParameters)
```

**setPreviewRestartDeepLink**

```swift
if let url = URL(string: "myapp://HomePage") {
	Target.setPreviewRestartDeepLink(url)
}
```

**setThirdPartyId**

```swift
Target.setThirdPartyId("third-party-id")
```

{% endtab %}

{% tab title="ACP (2.x)" %}

 **clearPrefetchCache**

```swift
ACPTarget.clearPrefetchCache()
```

**locationClickedWithName**

{% hint style="info" %}

The API is named `clickedLocation` in the AEPTarget SDK.

{% endhint %}

```swift
ACPTarget.locationClicked(withName: "mboxName", targetParameters: targetParameters)
```

**extensionVersion**

```swift
ACPTarget.extensionVersion()
```

**getThirdPartyId**

```swift
ACPTarget.getThirdPartyId({ id in
    // read Target thirdPartyId
})
```

**getTntId**

```swift
ACPTarget.getTntId({ id in
	// read target's tntId        
}
```

**prefetchContent**

```swift
ACPTarget.prefetchContent([
	ACPTargetPrefetchObject.init(name: "mboxName1", targetParameters: TargetParameters1),
	ACPTargetPrefetchObject.init(name: "mboxName2", targetParameters: TargetParameters2),
	],
	with: globalTargetParameters
	){ callback in
		// do something with the callback response
}
```

**registerExtension**

```swift
ACPTarget.registerExtension()
```

**resetExperience**

```swift
ACPTarget.resetExperience()
```

**retrieveLocationContent**

```swift
let request1 = ACPTargetRequestObject.init(mboxName: "logo", targetParameters: TargetParameters1, defaultContent: "BlueWhale") 
	{ content in
		// do something with the received content
	}
let request2 = TargetRequest(mboxName: "logo", targetParameters: TargetParameters2, defaultContent: "red") 
	{ content in
		// do something with the received content
	}
Target.retrieveLocationContent([request1, request2], with: globalTargetParameters)
```

**setPreviewRestartDeepLink**

```swift
if let url = URL(string: "myapp://HomePage") {
	ACPTarget.setPreviewRestartDeepLink(url)
}
```

**setThirdPartyId**

```swift
ACPTarget.setThirdPartyId("third-party-id")
```

{% endtab %}
{% endtabs %}

## Objective-C

### Public classes

| Type                   | AEP (3.x)               | ACP (2.x)               |
| ---------------------- | :---------------------- | :---------------------- |
| Primary Class (Module) | AEPMobileTarget         | ACPTarget               |
| Class                  | AEPTargetRequestObject  | ACPTargetRequestObject  |
| Class                  | AEPTargetPrefetchObject | ACPTargetPrefetchObject |
| Class                  | AEPTargetOrder          | ACPTargetOrder          |
| Class                  | AEPTargetParameters     | ACPTargetParameters     |
| Class                  | AEPTargetProduct        | ACPTargetProduct        |

### API usages

{% tabs %}
{% tab title="AEP (3.x)" %}

**clearPrefetchCache**

```objc
[AEPMobileTarget clearPrefetchCache];
```

**clickedLocation**

{% hint style="info" %}

The API is named `locationClickedWithName` in the ACPTarget SDK.

{% endhint %}

```objc
[AEPMobileTarget clickedLocation:@"mboxName" withTargetParameters: targetParameters];
```

**extensionVersion**

```objc
[AEPMobileTarget extensionVersion];
```

**getThirdPartyId**

```objc
[AEPMobileTarget getThirdPartyId:^(NSString * _Nullable thirdPartyId, NSError * _Nullable error) {
  // read thirdPartyId
}];
```

**getTntId**

```objc
[AEPMobileTarget getTntId:^(NSString * _Nullable tntId, NSError * _Nullable error) {
  // read tntId
}];
```

**prefetchContent**

```objc
AEPTargetPrefetchObject *prefetch1 = [[AEPTargetPrefetchObject alloc] initWithName:@"mbox1" targetParameters:nil];
AEPTargetPrefetchObject *prefetch2 = [[AEPTargetPrefetchObject alloc] initWithName:@"mbox2" targetParameters:nil];
[AEPMobileTarget prefetchContent: @[prefetch1, prefetch2] withParameters: parameters callback:^(NSError * _Nullable error) {
	// do something with the callback response
}];
```

**registerExtension**

{% hint style="info" %}
Registration occurs by passing `Target` to the `MobileCore.registerExtensions` API in addition to the other extensions registered.
{% endhint %}

```objc
[AEPMobileCore registerExtensions:@[..., AEPMobileTarget.class] completion:^{
	// registration complete
}];
```

**resetExperience**

```swift
[AEPMobileTarget resetExperience];
```

**retrieveLocationContent**

```objc
AEPTargetRequestObject *request1 = [[AEPTargetRequestObject alloc] initWithMboxName:@"mbox1" defaultContent:@"defaultContent" targetParameters:nil contentCallback:^(NSString * _Nullable content) {
  // do something with the received content
}];
AEPTargetRequestObject *request2 = [[AEPTargetRequestObject alloc] initWithMboxName:@"mbox2" defaultContent:@"defaultContent2" targetParameters:nil contentCallback:^(NSString * _Nullable content) {
  // do something with the received content
}];
[AEPMobileTarget retrieveLocationContent:@[request1, request2] withParameters: globalTargetParameters];
```

**setPreviewRestartDeepLink**

```objc
[AEPMobileTarget setPreviewRestartDeepLink:[NSURL URLWithString:(@"myapp://HomePage")]];
```

**setThirdPartyId**

```objc
[AEPMobileTarget setThirdPartyId:"third-party-id"];
```

{% endtab %}

{% tab title="ACP (2.x)" %}

**clearPrefetchCache**

```objc
[ACPTarget clearPrefetchCache];
```

**locationClickedWithName**

{% hint style="info" %}

The API is named `clickedLocation` in the AEPTarget SDK.

{% endhint %}

```objc
[ACPTarget locationClickedWithName:@"mboxName" targetParameters: targetParameters];
```

**extensionVersion**

```objc
[ACPTarget extensionVersion];
```

**getThirdPartyId**

```objc
[ACPTarget getThirdPartyId:^(NSString * _Nullable thirdPartyId) {
  // read third party id
}];
```

**getTntId**

```objc
[ACPTarget getThirdPartyId:^(NSString * _Nullable tntId) {
  // read tntId
}];
```

**prefetchContent**

```objc
ACPTargetPrefetchObject *prefetch1 = [ACPTargetPrefetchObject targetPrefetchObjectWithName:@"mbox1"
                                                                       targetParameters:nil];
ACPTargetPrefetchObject *prefetch2 = [ACPTargetPrefetchObject targetPrefetchObjectWithName:@"mbox2"
                                                                       targetParameters:nil];
[ACPTarget prefetchContent:@[prefetch1, prefetch2] withParameters: parameters callback:^(NSError * _Nullable error) {
   // do something with the callback response
}];
```

**registerExtension**

```objc
[ACPTarget registerExtension];
```

**resetExperience**

```swift
[ACPTarget resetExperience];
```

**retrieveLocationContent**

```objc
ACPTargetRequestObject *request1 = [ACPTargetRequestObject targetRequestObjectWithName:@"mbox1" targetParameters:nil defaultContent:@"defaultContent" callback:^(NSString * _Nullable content) {
  // do something with the received content
}];
ACPTargetRequestObject *request2 = [ACPTargetRequestObject targetRequestObjectWithName:@"mbox2" targetParameters:nil defaultContent:@"defaultContent" callback:^(NSString * _Nullable content) {
  // do something with the received content
}];
    
[ACPTarget retrieveLocationContent:@[request1, request2] withParameters: globalTargetParameters];
```

**setPreviewRestartDeepLink**

```objc
[ACPTarget setPreviewRestartDeeplink:[NSURL URLWithString:(@"myapp://HomePage")]];
```

**setThirdPartyId**

```objc
[ACPTarget setThirdPartyId:"thirdPartyId"];
```

{% endtab %}
{% endtabs %}