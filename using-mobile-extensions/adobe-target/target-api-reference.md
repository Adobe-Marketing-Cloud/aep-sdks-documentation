# Target API reference

## Target API reference

### clearPrefetchCache

This API clears the in-memory cache that contains the prefetched offers.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) clearPrefetchCache;
```

**Example**

**Swift**

```swift
ACPTarget.clearPrefetchCache
```

**Objective-C**

```text
[ACPTarget clearPrefetchCache];
```
{% endtab %}

{% tab title="React Native" %}
**Signature**

```text
clearPrefetchCache();
```

**Example usage**

```text
ACPTarget.clearPrefetchCache();
```
{% endtab %}
{% endtabs %}

### clickedLocation

This API sends a location click notification for an mbox to the configured Target server and can be invoked in the following cases:

* For a prefetched mbox, after the mbox content is retrieved using the `retrieveLocationContent` API.
* For a regular mbox, where no previous prefetch request is made, and the mbox content is retrieved using the `retrieveLocationContent` API.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) locationClickedWithName: (nonnull NSString*) name targetParameters: (nullable ACPTargetParameters*) parameters;
```

* _name_ is an NSString that contains the mbox location for which the click notification will be sent to Target.
* _parameters_ is the configured `ACPTargetParameters` for the request.

**Example**

**Swift**

```swift
// Mbox parameters
let mboxParameters = [
"membership": "prime"
]

// Product parameters
let productParameters = [
"id": "CEDFJC",
"categoryId": "Electronics"
]

// Order parameters
let orderParameters = [
"id": "NJJICK",
"total": "650",
"purchasedProductIds": "81, 123, 190"
]

// Profile parameters
let profileParameters = [
"ageGroup": "20-32"
]

// Create Target parameters
let product = ACPTargetProduct(id: "24D334", categoryId: "Stationary")
let order = ACPTargetOrder(id: "ADCKKBC", total: NSNumber(value: 400.50), purchasedProductIds: ["34", "125"])
let targetParameters = ACPTargetParameters(parameters: nil, profileParameters: nil, product: product, order: order)

ACPTarget.locationClicked(withName: "cartLocation", targetParameters: targetParameters)
```

**Objective-C**

```text
// Mbox parameters
NSDictionary *mboxParameters = @{@"membership":@"prime"};

// Product parameters
NSDictionary *productParameters = @{@"id":@"CEDFJC",
                                    @"categoryId":@"Electronics"};
// Order parameters
NSDictionary *orderParameters = @{@"id":@"NJJICK",
                                    @"total":@"650",
                                    @"purchasedProductIds":@"81, 123, 190"};

// Profile parameters
NSDictionary *profileParameters = @{@"ageGroup":@"20-32"};

// Create Target parameters
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];
ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];
ACPTargetParameters *targetParameters = [ACPTargetParameters targetParametersWithParameters:nil
                                                    profileParameters:nil
                                                              product:product
                                                                order:order];

[ACPTarget locationClickedWithName:@"cartLocation" targetParameters:targetParameters];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
locationClickedWithName(name: string, parameters?: ACPTargetParameters)
```

* _name_ is a string that contains the mbox location for which the click notification will be sent to Target.
* _parameters_ is the configured `ACPTargetParameters` for the request.

**Example**

```javascript
// Mbox parameters
var mboxParameters = {"membership": "prime"};

// Product parameters
var productParameters = new ACPTargetProduct("CEDFJC", "Electronics");

// Order parameters
var orderParameters = new ACPTargetOrder("NJJICK", 650, ["81","123","190"]);

// Profile parameters
var profileParameters = {"ageGroup": "20-32"};

// Create Target parameters
var product = new ACPTargetProduct("24D334", "Stationary");
var order = new ACPTargetOrder("ADCKKBC", 400.50, ["34","125"]);
var targetParameters = new ACPTargetParameters(null, null, product, order);

ACPTarget.locationClickedWithName("cartLocation", targetParameters);
```
{% endtab %}
{% endtabs %}

### displayedLocations

This API sends a location display notification for an mbox to the configured Target server. The API should be invoked for a prefetched mbox after the mbox content is retrieved using the `retrieveLocationContent` API. If no previous prefetch request is made, and the mbox content is retrieved using the `retrieveLocationContent` API, calling this API does not trigger a notification request to the Target server.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) locationsDisplayed: (nonnull NSArray<NSString*>*) mboxNames 
withTargetParameters: (nullable ACPTargetParameters*) targetParameters;
```

* _mboxNames_ is an NSArray of the mbox locations for which the display notification will be sent to Target.
* _targetParameters_ is the configured `ACPTargetParameters` for the request.

**Example**

**Swift**

```swift
let product = ACPTargetProduct(id: "24D334", categoryId: "Stationary")

let order = ACPTargetOrder(id: "ADCKKBC", total: NSNumber(value: 400.50), purchasedProductIds: ["34", "125"])

let targetParameters = ACPTargetParameters(parameters: nil, profileParameters: nil, product: product, order: order)

ACPTarget.locationsDisplayed(["mboxName1", "mboxName2"], with: targetParameters)
```

**Objective-C**

```text
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];

ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];

ACPTargetParameters *targetParameters = [ACPTargetParameters targetParametersWithParameters:nil
profileParameters:nil
product:product
order:order];

[ACPTarget locationsDisplayed:@[@"mboxName1", @"mboxName2"] withTargetParameters:targetParameters];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
locationsDisplayed(mboxNames: Array<string>, parameters?: ACPTargetParameters)
```

* _mboxNames_ is an Array of the mbox locations for which the display notification will be sent to Target.
* _targetParameters_ is the configured `ACPTargetParameters` for the request.

**Example**

```javascript
var product = new ACPTargetProduct("24D334", "Stationary");
var order = new ACPTargetOrder("ADCKKBC", 400.50, ["34", "125"]);
var targetParameters = new ACPTargetParameters(null, null, product, order);

ACPTarget.locationsDisplayed(["mboxName1", "mboxName2"], targetParameters);
```
{% endtab %}
{% endtabs %}

### extensionVersion

Returns the running version of the Target extension.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (nonnull NSString*) extensionVersion;
```

**Example**

**Swift**

```swift
let targetVersion = ACPTarget.extensionVersion()
```

**Objective-C**

```text
NSString *targetVersion = [ACPTarget extensionVersion];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
extensionVersion(): Promise<string>
```

**Example**

```javascript
ACPTarget.extensionVersion().then(version => {
            // read Target extension version 
});
```
{% endtab %}
{% endtabs %}

### getThirdPartyId

This API gets the custom visitor ID for Target. If no `third-party` ID was previously set, or if the ID was reset by calling resetExperience API, it will have a `nil` value.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) getThirdPartyId: (nonnull void (^) (NSString* __nullable thirdPartyId)) callback;
```

* _callback_ is invoked with the `thirdPartyId` value. If no third-party ID was set, this value will be `nil`.

**Example**

**Swift**

```swift
ACPTarget.getThirdPartyId({thirdPartyID in
       // read Target thirdPartyId
})
```

**Objective-C**

```text
[ACPTarget getThirdPartyId:^(NSString *thirdPartyId){
       // read Target thirdPartyId
}];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
getThirdPartyId(): Promise<string>
```

* A _Promise_ object is returned and is resolved with the `thirdPartyId` value.

**Example**

```javascript
ACPTarget.getThirdPartyId().then(thirdPartyId => {
            // read Target thirdPartyId 
});
```
{% endtab %}
{% endtabs %}

### getTntId

This API gets the Target user ID \(also known as the `tntId`\) from the Target service. The `tntId` is returned in the network response after a successful call to `prefetchContent` or `retrieveLocationContent`, which is then persisted in the SDK. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when the `resetExperience` API is used.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) getTntId: (nonnull void (^) (NSString* __nullable tntId)) callback;
```

* _callback_ is invoked with the `tntId` value. If no Target ID was set, this value will be `nil`.

**Example**

**Swift**

```swift
ACPTarget.getTntId({tntId in
       // read target's tntId
})
```

**Objective-C**

```text
[ACPTarget getTntId:^(NSString *tntId){
       // read target's tntId
}];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
getTntId(): Promise<string>
```

* A _Promise_ object is returned and is resolved with the `thirdPartyId` value.

**Example**

```javascript
ACPTarget.getTntId().then(tntId => {
            // read target's tntId                         
});
```
{% endtab %}
{% endtabs %}

### prefetchContent

This API sends a prefetch request to your configured Target server. The prefetch request is sent with the prefetch objects array and the specified Target parameters.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) prefetchContent: (nonnull NSArray<ACPTargetPrefetchObject*>*) prefetchObjectArray
          withParameters: (nullable ACPTargetParameters*) parameters
                callback: (nullable void (^) (NSError* _Nullable error)) callback;
```

**Example**

**Swift**

```swift
let mboxParameters1 = [
"status": "platinum"
]
let profileParameters1 = [
"age": "20"
]
let product1 = ACPTargetProduct(id: "24D3412", categoryId: "Books")
let order1 = ACPTargetOrder(id: "ADCKKIM", total: NSNumber(value: 344.30), purchasedProductIds: ["34", "125"])

let targetParameters1 = ACPTargetParameters(parameters: mboxParameters1, profileParameters: profileParameters1, product: product1, order: order1)

let mboxParameters2 = [
"userType": "Paid"
]
let product2 = ACPTargetProduct(id: "764334", categoryId: "Online")
let order2 = ACPTargetOrder(id: "ADCKKIM", total: NSNumber(value: 344.30), purchasedProductIds: ["id1", "id2"])

let targetParameters2 = ACPTargetParameters(parameters: mboxParameters2, profileParameters: nil, product: product2, order: order2)

// Creating Prefetch Objects
let prefetch1 = ACPTargetPrefetchObject(name: "logo", targetParameters: targetParameters1)

let prefetch2 = ACPTargetPrefetchObject(name: "buttonColor", targetParameters: targetParameters2)

// Creating prefetch Array
let prefetchArray = [prefetch1, prefetch2]

// Creating Target parameters
let mboxParameters = [
"status": "progressive"
]
let profileParameters = [
"age": "20-32"
]
let product = ACPTargetProduct(id: "24D334", categoryId: "Stationary")
let order = ACPTargetOrder(id: "ADCKKBC", total: NSNumber(value: 400.50), purchasedProductIds: ["34", "125"])

let targetParameters = ACPTargetParameters(parameters: mboxParameters, profileParameters: profileParameters, product: product, order: order)

// Target API Call
ACPTarget.prefetchContent(prefetchArray, with: targetParameters, callback: { error in
// do something with the callback response
})
```

**Objective-C**

```text
NSDictionary *mboxParameters1 = @{@"status":@"platinum"};
NSDictionary *profileParameters1 = @{@"age":@"20"};
ACPTargetProduct *product1 = [ACPTargetProduct targetProductWithId:@"24D3412" categoryId:@"Books"];
ACPTargetOrder *order1 = [ACPTargetOrder targetOrderWithId:@"ADCKKIM" total:@(344.30) purchasedProductIds:@[@"34", @"125"]];

ACPTargetParameters *targetParameters1 = [ACPTargetParameters targetParametersWithParameters:mboxParameters1
profileParameters:profileParameters1
product:product1
order:order1];

NSDictionary *mboxParameters2 = @{@"userType":@"Paid"};
ACPTargetProduct *product2 = [ACPTargetProduct targetProductWithId:@"764334" categoryId:@"Online"];
ACPTargetOrder *order2 = [ACPTargetOrder targetOrderWithId:@"ADCKKIM" total:@(344.30) purchasedProductIds:@[@"id1",@"id2"]];

ACPTargetParameters *targetParameters2 = [ACPTargetParameters targetParametersWithParameters:mboxParameters2
profileParameters:nil
product:product2
order:order2];

// Creating Prefetch Objects
ACPTargetPrefetchObject *prefetch1 = [ACPTargetPrefetchObject targetPrefetchObjectWithName:@"logo"
targetParameters:targetParameters1];

ACPTargetPrefetchObject *prefetch2 = [ACPTargetPrefetchObject targetPrefetchObjectWithName:@"buttonColor"
targetParameters:targetParameters2];

// Creating prefetch Array
NSArray *prefetchArray = @[prefetch1,prefetch2];

// Creating Target parameters
NSDictionary *mboxParameters = @{@"status":@"progressive"};
NSDictionary *profileParameters = @{@"age":@"20-32"};
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];
ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];

ACPTargetParameters *targetParameters = [ACPTargetParameters targetParametersWithParameters:mboxParameters
profileParameters:profileParameters
product:product
order:order];

// Target API Call
[ACPTarget prefetchContent:prefetchArray withParameters:targetParameters callback:^(NSError * _Nullable error){
// do something with the callback response
}];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
prefetchContent(prefetchObjectArray: Array<ACPTargetPrefetchObject>, parameters?: ACPTargetParameters): Promise<any>
```

* _prefetchObjectArray_ is an Array of `ACPTargetPrefetchObject` objects for various mbox locations.
* _parameters_ is the configured `ACPTargetParameters` for the prefetch request.
* A Promise object is returned and is resolved with true value or is rejected with the reason for the error.

**Example**

```javascript
var mboxParameters1 = {"status": "platinum"};
var profileParameters1 = {"age": "20"};
var product1 = new ACPTargetProduct("24D3412", "Books");
var order1 = new ACPTargetOrder("ADCKKIM", 344.30, ["34","125"]);
var targetParameters1 = new ACPTargetParameters(mboxParameters1, profileParameters1, product1, order1);

var mboxParameters2 = {"userType": "Paid"};
var product2 = new ACPTargetProduct("764334", "Online");
var order2 = new ACPTargetOrder("ADCKKIM", 344.30, ["id1","id2"]);
var targetParameters2 = new ACPTargetParameters(mboxParameters2, null, product2, order2);

// Creating Prefetch Objects
var prefetch1 = new ACPTargetPrefetchObject("logo", targetParameters1);
var prefetch2 = new ACPTargetPrefetchObject("buttonColor", targetParameters2);

// Creating prefetch Array
var prefetchList = [prefetch1, prefetch2];

// Creating Target parameters
var mboxParameters = {"status": "progressive"};
var profileParameters = {"age": "20-32"};
var product = new ACPTargetProduct("24D334", "Stationary");
var order = new ACPTargetOrder("ADCKKBC", 400.50, ["34","125"]);
var targetParameters = new ACPTargetParameters(mboxParameters, profileParameters, product, order);

// Target API Call
ACPTarget.prefetchContent(prefetchList, targetParameters).then(success => console.log(success)).catch(err => console.log(err));
```
{% endtab %}
{% endtabs %}

### registerExtension

Registers the Target extension with the Mobile Core.

{% tabs %}
{% tab title="Android" %}
**Syntax**
 
```java
public static void registerExtension()
```

**Example**

```java
Target.registerExtension();
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) registerExtension;
```

**Example**

**Swift**

```swift
ACPTarget.registerExtension()
```

**Objective-C**

```text
[ACPTarget registerExtension];
```
{% endtab %}

{% tab title="React Native" %}
When using React Native, register the Target extension with Mobile Core in native code as shown on the Android and iOS tabs.
{% endtab %}
{% endtabs %}

### resetExperience

This API resets the user's experience by removing the visitor identifiers and resetting the Target session. Invoking this API also removes previously set Target user ID and custom visitor IDs, Target Edge Host, and the session information from persistent storage.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) resetExperience;
```

**Example**

**Swift**

```swift
ACPTarget.resetExperience()
```

**Objective-C**

```text
[ACPTarget resetExperience];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
resetExperience()
```

**Example**

```javascript
ACPTarget.resetExperience();
```
{% endtab %}
{% endtabs %}

### retrieveLocationContent

This API sends a batch request to the configured Target server for multiple mbox locations.

A request will be sent to the configured Target server for mbox locations in the requests array for Target requests that have not been previously prefetched. The content for the mbox locations that have been prefetched in a previous request are returned from the SDK, and no additional network request is made. Each Target request object in the list contains a callback function, which is invoked when content is available for its given mbox location.

When using `contentWithData` callback to instantiate TargetRequest object, the following keys can be used to read response tokens and Analytics for Target \(A4T\) info from the data payload, if available in the Target response.

* responseTokens \(Response tokens\)
* analytics.payload \(A4T payload\)
* clickmetric.analytics.payload \(Click tracking A4T payload\)

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) retrieveLocationContent: (nonnull NSArray<ACPTargetRequestObject*>*) requests
                  withParameters: (nullable ACPTargetParameters*) parameters;
```

* _requests_ is an NSArray of `ACPTargetRequestObject` objects for various mbox locations.
* _parameters_ is the configured `ACPTargetParameters` for the load request.

**Example**

**Swift**

```swift
let mboxParameters1 = [
"status": "platinum"
]
let product1 = ACPTargetProduct(id: "24D3412", categoryId: "Books")
let order1 = ACPTargetOrder(id: "ADCKKIM", total: NSNumber(value: 344.30), purchasedProductIds: ["a", "b"])

let mboxParameters2 = [
"userType": "Paid"
]
let product2 = ACPTargetProduct(id: "764334", categoryId: "Online")
let order2 = ACPTargetOrder(id: "4t4uxksa", total: NSNumber(value: 54.90), purchasedProductIds: ["id1", "id2"])

let params1 = ACPTargetParameters(parameters: mboxParameters1, profileParameters: nil, product: product1, order: order1)
let request1 = ACPTargetRequestObject(name: "logo", targetParameters: params1, defaultContent: "BlueWhale", callback: { content in
// do something with the received content
})

let params2 = ACPTargetParameters(parameters: mboxParameters2, profileParameters: nil, product: product2, order: order2)
let request2 = ACPTargetRequestObject(name: "logo", targetParameters: params2, defaultContent: "red", callback: { content in
// do something with the received content
})

// Create request object array
let requestArray = [request1, request2]

// Creating Target parameters
let mboxParameters = [
"status": "progressive"
]
let profileParameters = [
"age": "20-32"
]
let product = ACPTargetProduct(id: "24D334", categoryId: "Stationary")
let order = ACPTargetOrder(id: "ADCKKBC", total: NSNumber(value: 400.50), purchasedProductIds: ["34", "125"])

let targetParameters = ACPTargetParameters(parameters: mboxParameters, profileParameters: profileParameters, product: product, order: order)

// Call the API
ACPTarget.retrieveLocationContent(requestArray, with: targetParameters)
```

**Objective-C**

```text
NSDictionary *mboxParameters1 = @{@"status":@"platinum"};
ACPTargetProduct *product1 = [ACPTargetProduct targetProductWithId:@"24D3412" categoryId:@"Books"];
ACPTargetOrder *order1 = [ACPTargetOrder targetOrderWithId:@"ADCKKIM" total:@(344.30) purchasedProductIds:@[@"a", @"b"]];

NSDictionary *mboxParameters2 = @{@"userType":@"Paid"};
ACPTargetProduct *product2 = [ACPTargetProduct targetProductWithId:@"764334" categoryId:@"Online"];
ACPTargetOrder *order2 = [ACPTargetOrder targetOrderWithId:@"4t4uxksa" total:@(54.90) purchasedProductIds:@[@"id1",@"id2"]];

ACPTargetParameters *params1 = [ACPTargetParameters targetParametersWithParameters:mboxParameters1
                                                    profileParameters:nil
                                                              product:product1
                                                                order:order1];
ACPTargetRequestObject *request1 = [ACPTargetRequestObject targetRequestObjectWithName:@"logo" targetParameters:params1
defaultContent:@"BlueWhale" callback:^(NSString * _Nullable content) {
    // do something with the received content
  }];

ACPTargetParameters *params2 = [ACPTargetParameters targetParametersWithParameters:mboxParameters2
                                                    profileParameters:nil
                                                              product:product2
                                                                order:order2];
ACPTargetRequestObject *request2 = [ACPTargetRequestObject targetRequestObjectWithName:@"logo" targetParameters:params2
defaultContent:@"red" callback:^(NSString * _Nullable content) {
    // do something with the received content
  }];

// Create request object array
NSArray *requestArray = @[request1,request2];

// Creating Target parameters
NSDictionary *mboxParameters = @{@"status":@"progressive"};
NSDictionary *profileParameters = @{@"age":@"20-32"};
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];
ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];

ACPTargetParameters *targetParameters = [ACPTargetParameters targetParametersWithParameters:mboxParameters
                                                    profileParameters:profileParameters
                                                              product:product
                                                                order:order];
// Call the API
[ACPTarget retrieveLocationContent:requestArray withParameters:targetParameters];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
retrieveLocationContent(requests: Array<ACPTargetRequestObject>, parameters?: ACPTargetParameters)
```

* _requests_ is an Array of `ACPTargetRequestObject` objects for various mbox locations.
* _parameters_ is the configured `ACPTargetParameters` for the load request.

**Example**

```javascript
var mboxParameters1 = {"status": "platinum"};
var product1 = new ACPTargetProduct("24D3412", "Books");
var order1 = new ACPTargetOrder("ADCKKIM", 344.30, ["a","b"]);

var mboxParameters2 = {"userType": "Paid"};
var product2 = new ACPTargetProduct("764334", "Online");
var order2 = new ACPTargetOrder("4t4uxksa", 54.90, ["id1","id2"]);

var params1 = new ACPTargetParameters(mboxParameters1, null, product1, order1);
var request1 = new ACPTargetRequestObject("logo", params1, "BlueWhale", (error, content) => {
      if (error) {
        console.error(error);
      } else {
        console.log("Target content:" + content);
      }
});

var params2 = new ACPTargetParameters(mboxParameters2, null, product2, order2);
var request2 = new ACPTargetRequestObject("logo", params1, "red", (error, content) => {
      if (error) {
        console.error(error);
      } else {
        console.log("Target content:" + content);
      }
});

// Create request object array
let requestArray = [request1, request2]

// Creating Target parameters
var mboxParameters = {"status": "progressive"};
var profileParameters = {"age": "20-32"};
var product = new ACPTargetProduct("24D334", "Stationary");
var order = new ACPTargetOrder("ADCKKBC", 400.50, ["34","125"]);
var targetParameters = new ACPTargetParameters(mboxParameters, profileParameters, product, order);

// Target API Call
ACPTarget.retrieveLocationContent(requestArray, targetParameters);
```
{% endtab %}
{% endtabs %}

### setPreviewRestartDeepLink

This API sets a specific location in the app to be displayed when preview mode selections have been confirmed.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) setPreviewRestartDeeplink: (nonnull NSURL*) deeplink;
```

* _deeplink_ is an NSURL that contains the preview restart deeplink.

**Example**

**Swift**

```swift
ACPTarget.setPreviewRestartDeepLink("myapp://HomePage")
```

**Objective-C**

```text
[ACPTarget setPreviewRestartDeepLink:@"myapp://HomePage"];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
setPreviewRestartDeeplink(deepLink: string)
```

* _deepLink_ is a string that contains the preview restart deeplink.

**Example**

```javascript
ACPTarget.setPreviewRestartDeeplink("myapp://HomePage");
```
{% endtab %}
{% endtabs %}

### setThirdPartyId

This API sets the custom visitor ID for Target. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when the resetExperience API is used.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) setThirdPartyId: (nullable NSString*) thirdPartyId;
```

* _thirdPartyId_ is a NSString that contains the custom visitor ID to be set in Target.

**Example**

**Swift**

```swift
ACPTarget.setThirdPartyId("third-party-id")
```

**Objective-C**

```text
[ACPTarget setThirdPartyId:@"third-party-id"];
```
{% endtab %}

{% tab title="React Native" %}
**Syntax**

```javascript
setThirdPartyId(thirdPartyId: string)
```

* _thirdPartyId_ is a string that contains the custom visitor ID to be set in Target.

**Example**

```javascript
ACPTarget.setThirdPartyId("third-party-id");
```
{% endtab %}
{% endtabs %}

### Visual preview

Target visual preview mode allows you to easily perform end-to-end QA activities by enrolling and previewing these activities on your device. This mode does not require a specialized testing set up. To get started, set up a URL scheme and generate the preview links.

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
To enter the preview visual mode, use the `collectLaunchInfo` API to enable the mode and click the red floating button that appears on the app screen.

**Syntax**

```text
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

* _userInfo_ : NSDictionary of data relevant to the expected use case.

**Example**

**Swift**

```swift
ACPCore.collectLaunchInfo(["adb_deeplink" : "com.adobe.targetpreview://app.adobetarget.com?at_preview_token=tokenFromTarget"])
```

**Objective-C**

```text
[ACPCore collectLaunchInfo: @{@"adb_deeplink":@"com.adobe.targetpreview://app.adobetarget.com?at_preview_token=tokenFromTarget"}];`
```
{% endtab %}
{% endtabs %}

## Public classes

{% tabs %}
{% tab title="iOS \(ACP 2.x\)" %}
### ACPTargetRequestObject

This class extends `ACPTargetPrefetchObject` by adding default content and a callback block that will be invoked to return mbox content from Target.

```text
@interface ACPTargetRequestObject : ACPTargetPrefetchObject

/* The default content that will be returned if Target servers are unreachable */   
@property(nonatomic, strong, nonnull) NSString* defaultContent;

/* Optional. When batch requesting Target locations, callback will be invoked when content is available for this location. */
@property(nonatomic, strong, nullable) void (^callback)(NSString* __nullable content);
@end
```

The following method can be used to create an instance of ACPTargetRequestObject that might be used to make a batch request to the configured Target server to fetch content for mbox locations.

```text
+ (nonnull instancetype) targetRequestObjectWithName: (nonnull NSString*) name
                                    targetParameters: (nullable ACPTargetParameters*) targetParameters
                                      defaultContent: (nonnull NSString*) defaultContent
                                            callback: (nullable void (^) (NSString* __nullable content)) callback;
```

### ACPTargetPrefetchObject

This class contains the name of the Target location/mbox and target parameters to be used in a prefetch request.

```text
@interface ACPTargetPrefetchObject : NSObject

/* The name of the Target location/mbox */
@property(nonatomic, strong, nullable) NSString* name;

/* Target parameters associated with the prefetch object. You can set all other parameters in this object */
@property(nonatomic, strong, nullable) ACPTargetParameters* targetParameters;
@end
```

The following method can be used to create an instance of ACPTargetPrefetchObject that might be used to make a prefetch request to the configured Target server to prefetch content for mbox locations.

```text
+ (nonnull instancetype) targetPrefetchObjectWithName: (nonnull NSString*) name
                                     targetParameters: (nullable ACPTargetParameters*) targetParameters;
```

### ACPTargetParameters

This class contains mbox parameters dictionary, profile parameters dictionary, ACPTargetOrder object as well as ACPTargetProduct object.

```text
@interface ACPTargetParameters : NSObject

/* Dictionary containing key-value pairs of parameters */
@property(nonatomic, strong, nullable) NSDictionary<NSString*, NSString*>* parameters;

/* Dictionary containing key-value pairs of profile parameters */
@property(nonatomic, strong, nullable) NSDictionary<NSString*, NSString*>* profileParameters;

/* ACPTargetOrder object */
@property(nonatomic, strong, nullable) ACPTargetOrder* order;

/* ACPTargetProduct object */
@property(nonatomic, strong, nullable) ACPTargetProduct* product;
@end
```

The following method can be used to create an instance of ACPTargetParameters.

```text
+ (nonnull instancetype) targetParametersWithParameters: (nullable NSDictionary*) parameters
                                      profileParameters: (nullable NSDictionary*) profileParameters
                                                product: (nullable ACPTargetProduct*) product
                                                  order: (nullable ACPTargetOrder*) order;
```

### ACPTargetOrder

This class contains orderId, total and an array for purchasedProductIds.

```text
@interface ACPTargetOrder : NSObject

/* Order ID */
@property(nonatomic, strong, nonnull) NSString* orderId;

/* Order total */
@property(nonatomic, strong, nullable) NSNumber* total;

/* Array of Purchased Product Ids */
@property(nonatomic, strong, nullable) NSArray<NSString*>* purchasedProductIds;
@end
```

The following method can be used to create an instance of ACPTargetOrder.

```text
+ (nonnull instancetype) targetOrderWithId: (nonnull NSString*) orderId
                                     total: (nullable NSNumber*) total
                       purchasedProductIds: (nullable NSArray <NSString*>*) purchasedProductIds;
```

### ACPTargetProduct

This class contains productId and categoryId.

```text
@interface ACPTargetProduct : NSObject

/* Product ID */
@property(nonatomic, strong, nullable) NSString* productId;

/* Category ID */
@property(nonatomic, strong, nullable) NSString* categoryId;
@end
```

The following method can be used to create an instance of ACPTargetProduct.

```text
+ (nonnull instancetype) targetProductWithId: (nonnull NSString*) productId
                                  categoryId: (nullable NSString*) categoryId;
```
{% endtab %}

{% tab title="React Native" %}
### ACPTargetRequestObject

This class extends `ACPTargetPrefetchObject` by adding default content and a callback block that is invoked to return mbox content from Target.

```javascript
class ACPTargetRequestObject extends ACPTargetPrefetchObject {
  defaultContent:   string;

  constructor(name: string, targetParameters: ACPTargetParameters, defaultContent: string) {
    super(name, targetParameters);
    this.defaultContent = defaultContent;
  }
}
```

### ACPTargetPrefetchObject

This class contains the name of the Target location/mbox and Target parameters to be used in a prefetch request.

```javascript
class ACPTargetPrefetchObject {
  name:   string;
  targetParameters: ACPTargetParameters;

  constructor(name?: string, targetParameters?: ACPTargetParameters) {
      this.name = name;
    this.targetParameters = targetParameters;
  }

}
```

### ACPTargetParameters

This class contains an mbox parameters dictionary, a profile parameters dictionary, an `ACPTargetOrder` object, and an `ACPTargetProduct` object.

```javascript
class ACPTargetParameters {
  parameters: {string: string};
  profileParameters: {string: string};
  order: ACPTargetOrder;
  product: ACPTargetProduct;

  constructor(parameters?: {string: string}, profileParameters?: {string: string}, product?: ACPTargetProduct, order?: ACPTargetOrder) {
      this.parameters = parameters;
    this.profileParameters = profileParameters;
    this.product = product;
    this.order = order;
  }
}
```

### ACPTargetOrder

This class contains an `orderId`, the total, and an array, for `purchasedProductIds`.

```javascript
class ACPTargetOrder {
  orderId:   string;
  total:     number;
  purchasedProductIds: Array<string>;

  constructor(orderId: string, total?: number, purchasedProductIds: Array<string>) {
      this.orderId = orderId;
    this.total = total;
    this.purchasedProductIds = purchasedProductIds;
  }
}
```

### ACPTargetProduct

This class contains a productId and a categoryId.

```javascript
class ACPTargetProduct {
  productId: string;
  categoryId: string;

  constructor(productId: string, categoryId: string) {
      this.productId = productId;
    this.categoryId = categoryId;
  }
}
```
{% endtab %}
{% endtabs %}

