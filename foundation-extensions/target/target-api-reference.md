# Target API Reference

This document contains usage information for the public functions and classes in `AEPTarget`.

## prefetchContent
This API sends a prefetch request to your configured Target server with the prefetch objects array and the specified target parameters. 

### Swift 

#### Syntax 

```swift
static func prefetchContent(_ prefetchArray: [TargetPrefetch], with targetParameters: TargetParameters? = nil, _ completion: ((Error?) -> Void)?)
```

  - *prefetchArray* - is an array of `TargetPrefetch` objects for various mbox locations.
  - *targetParameters* - is the configured `TargetParameters` for the prefetch request.
  - If the prefetch is successful, `completion` is invoked with a nil value. If the prefetch is not successful, an error message is returned.

#### Example

```swift
        let TargetParameters1 = TargetParameters(
            parameters: ["status": "platinum"],
            profileParameters: ["age": "20"],
            order: TargetOrder(id: "ADCKKIM", total: 344.30, purchasedProductIds: ["34", "125"]),
            product: TargetProduct(productId: "24D3412", categoryId:"Books")
        )
            
        let TargetParameters2 = TargetParameters(
            parameters: ["userType": "Paid"],
            profileParameters: nil,
            order: TargetOrder(id: "ADCKKIM", total: 344.30, purchasedProductIds: ["id1", "id2"]),
            product: TargetProduct(productId: "764334", categoryId:"Online")
        )
        
        let globalTargetParameters = TargetParameters(
            parameters: ["status": "progressive"],
            profileParameters: ["age": "20-32"],
            order: TargetOrder(id: "ADCKKBC", total: 400.50, purchasedProductIds: ["34", "125"]),
            product: TargetProduct(productId: "24D334", categoryId:"Stationary")
        )
        Target.prefetchContent(
            [
                TargetPrefetch(name: "mboxName1", targetParameters: TargetParameters1),
                TargetPrefetch(name: "mboxName2", targetParameters: TargetParameters2),
            ],
            with: globalTargetParameters
        ){ error in
            // do something with the callback response
        }
```

### Objective C

#### Syntax 

```objectivec
+ (void) prefetchContent: (nonnull NSArray<AEPTargetPrefetchObject*>*) targetPrefetchObjectArray 
         withParameters: (nullable AEPTargetParameters*) targetParameters 
         callback: (nullable void (^) (NSError* _Nullable error)) completion;
```

  - *prefetchObjectArray* : is an array of `TargetPrefetch` objects for various mbox locations.
  - *targetParameters* : is the configured `TargetParameters` for the prefetch request.
  - If the prefetch is successful, `completion` is invoked with a nil value. If the prefetch is not successful, an error message is returned.

#### Example

```objectivec
    NSDictionary *mboxParameters1 = @{@"status":@"platinum"};
    NSDictionary *profileParameters1 = @{@"age":@"20"};
    AEPTargetProduct *product1 = [[AEPTargetProduct alloc] initWithProductId:@"24D3412" categoryId:@"Books"];
    AEPTargetOrder *order1 = [[AEPTargetOrder alloc] initWithId:@"ADCKKIM" total:[@(344.30) doubleValue] purchasedProductIds:@[@"34", @"125"]];

    AEPTargetParameters *targetParameters1 = [[AEPTargetParameters alloc] initWithParameters:mboxParameters1 profileParameters:profileParameters1 order:order1 product:product1 ];

    NSDictionary *mboxParameters2 = @{@"userType":@"Paid"};
    AEPTargetProduct *product2 = [[AEPTargetProduct alloc] initWithProductId:@"764334" categoryId:@"Online"];
    AEPTargetOrder *order2 = [[AEPTargetOrder alloc] initWithId:@"ADCKKIM" total:[@(344.30) doubleValue] purchasedProductIds:@[@"id1",@"id2"]];
    AEPTargetParameters *targetParameters2 = [[AEPTargetParameters alloc] initWithParameters:mboxParameters2 profileParameters:nil order:order2 product:product2 ];

    // Creating Prefetch Objects
    AEPTargetPrefetchObject *prefetch1 = [[AEPTargetPrefetchObject alloc] initWithName: @"logo" targetParameters:targetParameters1];
    AEPTargetPrefetchObject *prefetch2 = [[AEPTargetPrefetchObject alloc] initWithName: @"buttonColor" targetParameters:targetParameters2];
    

    // Creating prefetch Array
    NSArray *prefetchArray = @[prefetch1,prefetch2];

    // Creating Target parameters
    NSDictionary *mboxParameters = @{@"status":@"progressive"};
    NSDictionary *profileParameters = @{@"age":@"20-32"};
    AEPTargetProduct *product = [[AEPTargetProduct alloc] initWithProductId:@"24D334" categoryId:@"Stationary"];
    AEPTargetOrder *order = [[AEPTargetOrder alloc] initWithId:@"ADCKKBC" total:[@(400.50) doubleValue] purchasedProductIds:@[@"34", @"125"]];

    AEPTargetParameters *targetParameters = [[AEPTargetParameters alloc] initWithParameters:mboxParameters
    profileParameters:profileParameters
    order:order
    product:product];

    // Target API Call
    [AEPMobileTarget prefetchContent:prefetchArray withParameters:targetParameters callback:^(NSError * _Nullable error){
    // do something with the callback response
    }];
```

## retrieveLocationContent

This API sends a batch request to the configured Target server for multiple mbox locations.

For mbox locations in the Target requests list that are not already prefetched, this API sends a batch request to the configured Target server. The content for the mbox locations that have been prefetched in a previous request are returned from the SDK, and no additional network request is made. Each Target request object in the list contains a callback function, which is invoked when content is available for its given mbox location.

### Swift 

#### Syntax 

```swift
static func retrieveLocationContent(_ requestArray: [TargetRequest], with targetParameters: TargetParameters? = nil)
```

  - *requestArray* : an array of `TargetRequest` objects to retrieve content
  - *targetParameters* : a `TargetParameters` object containing parameters for all locations in the requests array

#### Example

```swift
        let TargetParameters1 = TargetParameters(
            parameters: ["status": "platinum"],
            profileParameters: ["age": "20"],
            order: TargetOrder(id: "ADCKKIM", total: 344.30, purchasedProductIds: ["34", "125"]),
            product: TargetProduct(productId: "24D3412", categoryId: "Books")
        )

        let TargetParameters2 = TargetParameters(
            parameters: ["userType": "Paid"],
            profileParameters: nil,
            order: TargetOrder(id: "ADCKKIM", total: 344.30, purchasedProductIds: ["id1", "id2"]),
            product: TargetProduct(productId: "764334", categoryId: "Online")
        )

        let globalTargetParameters = TargetParameters(
            parameters: ["status": "progressive"],
            profileParameters: ["age": "20-32"],
            order: TargetOrder(id: "ADCKKBC", total: 400.50, purchasedProductIds: ["34", "125"]),
            product: TargetProduct(productId: "24D334", categoryId: "Stationary")
        )

        let request1 = TargetRequest(mboxName: "logo", defaultContent: "BlueWhale", targetParameters: TargetParameters1) { _ in
            // do something with the received content
        }
        let request2 = TargetRequest(mboxName: "logo", defaultContent: "red", targetParameters: TargetParameters2) { _ in
            // do something with the received content
        }
        Target.retrieveLocationContent([request1, request2], with: globalTargetParameters)
```

### Objective C

#### Syntax 

```objectivec
+ (void) retrieveLocationContent: (nonnull NSArray<AEPTargetRequestObject*>*) requests
         withParameters: (nullable AEPTargetParameters*) parameters;
```

  - *requests* : an array of `AEPTargetRequestObject` objects to retrieve content
  - *parameters* : a `AEPTargetParameters` object containing parameters for all locations in the requests array 

#### Example

```objectivec
    NSDictionary *mboxParameters1 = @{@"status":@"platinum"};
    NSDictionary *profileParameters1 = @{@"age":@"20"};
    AEPTargetProduct *product1 = [[AEPTargetProduct alloc] initWithProductId:@"24D3412" categoryId:@"Books"];
    AEPTargetOrder *order1 = [[AEPTargetOrder alloc] initWithId:@"ADCKKIM" total:[@(344.30) doubleValue] purchasedProductIds:@[@"34", @"125"]];

    AEPTargetParameters *targetParameters1 = [[AEPTargetParameters alloc] initWithParameters:mboxParameters1 profileParameters:profileParameters1 order:order1 product:product1 ];

    NSDictionary *mboxParameters2 = @{@"userType":@"Paid"};
    AEPTargetProduct *product2 = [[AEPTargetProduct alloc] initWithProductId:@"764334" categoryId:@"Online"];
    AEPTargetOrder *order2 = [[AEPTargetOrder alloc] initWithId:@"ADCKKIM" total:[@(344.30) doubleValue] purchasedProductIds:@[@"id1",@"id2"]];
    AEPTargetParameters *targetParameters2 = [[AEPTargetParameters alloc] initWithParameters:mboxParameters2 profileParameters:nil order:order2 product:product2 ];
    
    AEPTargetRequestObject *request1 = [[AEPTargetRequestObject alloc] initWithMboxName: @"logo" defaultContent: @"BlueWhale" targetParameters: targetParameters1 contentCallback:^(NSString * _Nullable content) {
        // do something with the received content
        }];
    AEPTargetRequestObject *request2 = [[AEPTargetRequestObject alloc] initWithMboxName: @"logo" defaultContent: @"red" targetParameters: targetParameters2 contentCallback:^(NSString * _Nullable content) {
        // do something with the received content
        }];
    // Create request object array
    NSArray *requestArray = @[request1,request2];

    // Creating Target parameters
    NSDictionary *mboxParameters = @{@"status":@"progressive"};
    NSDictionary *profileParameters = @{@"age":@"20-32"};
    AEPTargetProduct *product = [[AEPTargetProduct alloc] initWithProductId:@"24D334" categoryId:@"Stationary"];
    AEPTargetOrder *order = [[AEPTargetOrder alloc] initWithId:@"ADCKKBC" total:[@(400.50) doubleValue] purchasedProductIds:@[@"34", @"125"]];

    AEPTargetParameters *targetParameters = [[AEPTargetParameters alloc] initWithParameters:mboxParameters
                                                                          profileParameters:profileParameters
                                                                                      order:order
                                                                                    product:product];
    [AEPMobileTarget retrieveLocationContent: requestArray withParameters: targetParameters];
```
## setThirdPartyId

This API sets the custom visitor ID for Target.

    This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when the resetExperience API is used.

### Swift 

#### Syntax 

```swift
static func setThirdPartyId(_ id: String)
```

  - *id* : a `String` that contains the custom visitor ID to be set in Target.

#### Example

```swift
Target.setThirdPartyId("third-party-id")
```

### Objective C

#### Syntax 

```objectivec
+ (void) setThirdPartyId: (nullable NSString*) thirdPartyId;
```

  - *thirdPartyId* : a NSString that contains the custom visitor ID to be set in Target.

#### Example

```objectivec
[ACPTarget setThirdPartyId:@"third-party-id"];
```

## getThirdPartyId

This API gets the custom visitor ID for Target. If no `third-party` ID was previously set, or if the ID was reset by calling resetExperience API, it will have a `null` value.

### Swift 

#### Syntax 

```swift
static func getThirdPartyId(_ completion: @escaping (String?, Error?) -> Void)
```

  - *completion* : invoked with the `thirdPartyId` value. If no `third-party` ID was set, this value will be `nil`.

#### Example

```swift
ACPTarget.getThirdPartyId({id, err in
    // read Target thirdPartyId
})
```

### Objective C

#### Syntax 

```objectivec
+ (void) getThirdPartyId: (nonnull void (^) (NSString* __nullable thirdPartyId, NSError * _nullable error)) completion;
```

  - *completion* : invoked with the `thirdPartyId` value. If no `third-party` ID was set, this value will be `nil`.

#### Example

```objectivec
    [AEPMobileTarget getThirdPartyId:^(NSString *thirdPartyID, NSError *error){
        // read Target thirdPartyId
    }];
```

## getTntId

This API gets the Target user identifier. Target returns the tntId with a successful call to `prefetchContent`, which is then persisted in the SDK.

    This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when the resetExperience API is used.

### Swift 

#### Syntax 

```swift
static func getTntId(_ completion: @escaping (String?, Error?) -> Void)
```

  - *completion* : invoked with the `tntId` value. If no Target ID was set, this value will be `nil`.

#### Example

```swift
    Target.getTntId { id, err in
        // read target's tntId        
    }
```

### Objective C

#### Syntax 

```objectivec
+ (void) getTntId: (nonnull void (^) (NSString* __nullable thirdPartyId, NSError * _nullable error)) completion;
```

  - *completion* : invoked with the `tntId` value. If no Target ID was set, this value will be `nil`.

#### Example

```objectivec
    [AEPMobileTarget getTntId:^(NSString *tntID, NSError *error){
        // read target's tntId 
    }];
```

## resetExperience

This API resets the user's experience by removing the visitor identifiers and resetting the Target session. Invoking this API also removes previously set Target user ID and custom visitor IDs, Target Edge Host, and the session information from persistent storage.

### Swift 

#### Syntax 

```swift
static func resetExperience()
```

#### Example

```swift
Target.resetExperience()
```

### Objective C

#### Syntax 

```objectivec
+ (void) resetExperience;
```

#### Example

```objectivec
[AEPMobileTarget resetExperience];
```

## clearPrefetchCache

This API clears the in-memory cache that contains the prefetched offers.

### Swift 

#### Syntax 

```swift
static func clearPrefetchCache()
```

#### Example

```swift
Target.clearPrefetchCache()
```

### Objective C

#### Syntax 

```objectivec
+ (void) clearPrefetchCache;
```

#### Example

```objectivec
[AEPMobileTarget clearPrefetchCache];
```

## setPreviewRestartDeepLink

This API sets the Target preview URL to be displayed when the preview mode is enabled and preview selections are confirmed.

### Swift 

#### Syntax 

```swift
static func setPreviewRestartDeepLink(_ deeplink: URL)
```

  - *deeplink* : an `URL` that contains the preview restart deeplink.

#### Example

```swift
    if let url = URL(string: "myapp://HomePage") {
        Target.setPreviewRestartDeepLink(url)
    }
```

### Objective C

#### Syntax 

```objectivec
+ (void) setPreviewRestartDeeplink: (nonnull NSURL*) deeplink;
```

  - *deeplink* : an `NSURL` that contains the preview restart deeplink.

#### Example

```objectivec
[AEPMobileTarget setPreviewRestartDeepLink:@"myapp://HomePage"];
```

## displayedLocations

Use this API to send a location (mbox) display notification to the configured Target server. This API should be invoked for a prefetched mbox after the mbox content is retrieved using the `retrieveLocationContent` API. If no previous prefetch request is made, and the mbox content is retrieved using the `retrieveLocationContent` API, calling this API does not trigger a notification request to the Target server.

### Swift 

#### Syntax 

```swift
static func displayedLocations(_ names: [String], targetParameters: TargetParameters?)
```

  - *names* : is an array of the mbox locations for which the display notification will be sent to Target.
  - *targetParameters* : is the configured `TargetParameters` for the request.

#### Example

```swift
    Target.displayedLocations(
        names: ["mboxName1", "mboxName2"],
        targetParameters: TargetParameters(
            parameters: nil,
            profileParameters: nil,
            order: TargetOrder(id: "ADCKKBC", total: 400.50, purchasedProductIds: ["34", "125"]),
            product: TargetProduct(productId: "24D334", categoryId: "Stationary")
        )
    )
```

### Objective C

#### Syntax 

```objectivec
+ (void) displayedLocations: (nonnull NSArray<NSString*>*) names 
         withTargetParameters: (nullable AEPTargetParameters*) targetParameters;
```

  - *names* : is an NSArray of the mbox locations for which the display notification will be sent to Target.
  - *targetParameters* : is the configured `AEPTargetParameters` for the request. 

#### Example

```objectivec
    AEPTargetOrder *order = [[AEPTargetOrder alloc] initWithId:@"ADCKKBC" total:400.50 purchasedProductIds:@[@"34", @"125"]];
    AEPTargetProduct *product =[[AEPTargetProduct alloc] initWithProductId:@"24D334" categoryId:@"Stationary"];
    AEPTargetParameters * targetParams = [[AEPTargetParameters alloc] initWithParameters:nil profileParameters:nil order:order product:product];
    [AEPMobileTarget displayedLocations:@[@"mboxName1", @"mboxName2"] withTargetParameters:targetParams];
```


## clickedLocation

This API sends a location (mbox) click notification to the configured Target server and can be invoked in the following cases:

- For a prefetched mbox, after the mbox content is retrieved using the `retrieveLocationContent` API.

- For a regular mbox, where no previous prefetch request is made, and the mbox content is retrieved using the `retrieveLocationContent` API.

### Swift 

#### Syntax 

```swift
static func clickedLocation(_ name: String, targetParameters: TargetParameters?)
```

  - *name* : a `String` that contains the mbox location for which the click notification will be sent to Target.
  - *targetParameters* : the configured `TargetParameters` for the request.

#### Example

```swift
    Target.clickedLocation(
        name: "cartLocation",
        targetParameters: TargetParameters(
            parameters: nil,
            profileParameters: nil,
            order: TargetOrder(id: "ADCKKBC", total: 400.50, purchasedProductIds: ["34", "125"]),
            product: TargetProduct(productId: "24D334", categoryId: "Stationary")
        )
    )       
```

### Objective C

#### Syntax 

```objectivec
+ (void) clickedLocation: (nonnull NSArray<NSString*>*) names 
         withTargetParameters: (nullable AEPTargetParameters*) targetParameters;
```

  - *name* : an `NSString` that contains the mbox location for which the click notification will be sent to Target.
  - *targetParameters* : the configured `AEPTargetParameters` for the request.  

#### Example

```objectivec
    EPTargetOrder *order = [[AEPTargetOrder alloc] initWithId:@"ADCKKBC" total:400.50 purchasedProductIds:@[@"34", @"125"]];
    AEPTargetProduct *product =[[AEPTargetProduct alloc] initWithProductId:@"24D334" categoryId:@"Stationary"];
    AEPTargetParameters * targetParams = [[AEPTargetParameters alloc] initWithParameters:nil profileParameters:nil order:order product:product];
    [AEPMobileTarget displayedLocations:@[@"mboxName1", @"mboxName2"] withTargetParameters:targetParams];
```


## Viaual preview

The visual preview mode allows you to easily perform end-to-end QA activities by enrolling and previewing these activities on your device. This mode does not require a specialized testing set up. To get started, set up a URL scheme and generate the preview links.

To enter the preview visual mode, use the `collectLaunchInfo` API to enable the mode and click the red floating button that appears on the app screen.

### Swift 

#### Syntax 

```swift
public static func collectLaunchInfo(_ userInfo: [String: Any])
```

#### Example

```swift
    MobileCore.collectLaunchInfo(["adb_deeplink" : "com.adobe.targetpreview://app.adobetarget.com?at_preview_token=tokenFromTarget"])
```

### Objective C

#### Syntax 

```objectivec
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

#### Example

```objectivec
    [AEPMobileCore collectLaunchInfo: @{@"adb_deeplink":@"com.adobe.targetpreview://app.adobetarget.com?at_preview_token=tokenFromTarget"}];
```