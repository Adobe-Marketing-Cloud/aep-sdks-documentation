# Target API reference

## Get custom visitor IDs

Use this API to get the custom visitor ID for Target.

{% tabs %}
{% tab title="Android" %}
### getThirdPartyId

The callback is invoked to return the `thirdPartyId` value, or if no third-party ID is set, `null` is returned.

#### Syntax

```java
public static void getThirdPartyId(final AdobeCallback<String> callback)
```

#### Example

```java
Target.getThirdPartyId(new AdobeCallback<String>() {                    
    @Override
    public void call(String thirdPartyID) {
                // read Target thirdPartyID
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### getThirdPartyId

The callback will be invoked to return the `thirdPartyId` value, or if no third-party ID is set, `nil` is returned.

#### Syntax

```objectivec
+ (void) getThirdPartyId: (nonnull void (^) (NSString* __nullable thirdPartyId)) callback;
```

#### Examples

Here are the examples in Objective C and Swift:

**Objective C**

```objectivec
[ACPTarget getThirdPartyId:^(NSString *thirdPartyId){
       // read Target thirdPartyId
}];
```

**Swift**

```swift
ACPTarget.getThirdPartyId({thirdPartyID in
       // read Target thirdPartyId
})
```
{% endtab %}
{% endtabs %}

## Set custom visitor IDs

Use this API to set custom visitor IDs for Target.

{% hint style="info" %}
This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when the reset experience API is used.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### setThirdPartyId

#### Syntax

```java
public static void setThirdPartyId(final String thirdPartyId)
```

#### Example

```java
Target.setThirdPartyId("third-party-id");
```
{% endtab %}

{% tab title="iOS" %}
### setThirdPartyId

This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when `resetExperience` API is called.

#### Syntax

```objectivec
+ (void) setThirdPartyId: (nullable NSString*) thirdPartyId;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPTarget setThirdPartyId:@"third-party-id"];
```

**Swift**

```swift
ACPTarget.setThirdPartyId("third-party-id")
```
{% endtab %}
{% endtabs %}

## Get Target user identifier

Use this API to get the Target user identifier.

{% tabs %}
{% tab title="Android" %}
### getTntId

The callback is invoked to return the `tntId` value, or if no Target ID is set, `null` is returned.

Target returns `tntId` with a successful call to `loadRequests` or `prefetchContent`. Once set in the SDK, this ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when `resetExperience` API is called.

#### Syntax

```java
public static void getTntId(final AdobeCallback<String> callback)
```

#### Example

```java
Target.getTntId(new AdobeCallback<String>() {
    @Override
    public void call(String value) {
        // read target's tntid
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### getTntId

The callback will be invoked to return the `tntId` value, or if no Target ID is set, `nil` is returned.

Target returns `tntId` upon a successful call to `loadRequests` or `prefetchContent`. Once set in SDK, this ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when `resetExperience` API is called.

#### Syntax

```objectivec
+ (void) getTntId: (nonnull void (^) (NSString* __nullable tntId)) callback;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPTarget getTntId:^(NSString *tntId){
       // read target's tntId
}];
```

**Swift**

```swift
ACPTarget.getTntId({tntId in
       // read target's tntId
})
```
{% endtab %}
{% endtabs %}

## Reset user experience

Use this API to reset the user's experience by removing the visitor identifiers and resetting Target session. This method also removes previously set Target user ID and custom visitor IDs, Target Edge Host and session information from persistent storage.

{% tabs %}
{% tab title="Android" %}
### resetExperience

#### Syntax

```java
public static void resetExperience()
```

#### Example

```java
Target.resetExperience();
```
{% endtab %}

{% tab title="iOS" %}
### resetExperience

#### Syntax

```objectivec
+ (void) resetExperience;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPTarget resetExperience];
```

**Swift**

```swift
ACPTarget.resetExperience()
```
{% endtab %}
{% endtabs %}

## Set preview restart deeplink

Use this API to set the Target preview URL to be displayed when the preview mode is enabled and preview selections are confirmed.

{% tabs %}
{% tab title="Android" %}
### setPreviewRestartDeeplink

#### Syntax

```text
public static void setPreviewRestartDeepLink(final Uri deepLink)
```

#### Example

```java
Target.setPreviewRestartDeepLink("myapp://HomePage");
```
{% endtab %}

{% tab title="iOS" %}
### setPreviewRestartDeeplink

#### Syntax

```objectivec
+ (void) setPreviewRestartDeeplink: (nonnull NSURL*) deeplink;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```text
[ACPTarget setPreviewRestartDeepLink:@"myapp://HomePage"];
```

**Swift**

```swift
ACPTarget.setPreviewRestartDeepLink("myapp://HomePage")
```
{% endtab %}
{% endtabs %}

## Prefetch offers

The SDK can minimize the number of times it reaches out to Target servers to fetch offers by caching server responses. With a successful prefetch call for mbox locations, offer content is retrieved and cached in the SDK. This content is retrieved from the cache for all future [retrieveLocationContent](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#retrieve-location-content-requests) API calls for the specified mbox names. This prefetch process reduces offer load time, network calls made to Target servers, and allows Target to be notified which mbox was visited by the mobile app user.

{% hint style="warning" %}
Prefetched offer content does not persist across application launches. The prefetch content is cached as long as the application lives in memory or until the API to clear the cache is called. For more information, see [Clear prefetch offer cache](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target#clear-prefetch-offer-cache).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### TargetPrefetch constructor

Using the `TargetPrefetch` constructor, you can create a `TargetPrefetch` instance with the specified data. It accepts the mbox location name and an optional `TargetParameters` object. The returned instance can be used with `prefetchContent` API to prefetch offers for the specified mbox locations.

#### Syntax

```java
public TargetPrefetch(final String mboxName, final TargetParameters targetParameters)
```

#### Example

```java
TargetParameters targetParameters = new TargetParameters.Builder()
.product(new TargetProduct(String, String))
.order(new TargetOrder(String, Double, List<String>))
.parameters(mboxParameters)
.profileParameters(profileParameters).build();

TargetPrefetch prefetchRequest = new TargetPrefetch("mboxName", targetParameters);
```

### prefetchContent

Use this API to send a prefetch request to your configured Target server with the `TargetPrefetch` list and the specified `TargetParameters`. The callback is invoked when the prefetch is complete and, if successful, returns a null value. If the prefetch is not successful, an error message is returned.

#### Syntax

```java
public static void prefetchContent(final List<TargetPrefetch>                                                                         targetPrefetchList,
final TargetParameters targetParameters,
final final AdobeCallback<String> callback);
```

#### Example

```java
// first prefetch request
Map<String, Object> mboxParameters1 = new HashMap<>();
mboxParameters1.put("status", "platinum");

// second prefetch request
Map<String, Object> mboxParameters2 = new HashMap<>();
mboxParameters2.put("userType", "paid");

List<String> purchasedIds = new ArrayList<String>();
purchasedIds.add("34");
purchasedIds.add("125");

TargetOrder targetOrder = new TargetOrder("ADCKKIM", 344.30, purchasedIds);
TargetProduct targetProduct = new TargetProduct("24D3412", "Books");

TargetParameters targetParameters1 = new TargetParameters.Builder()
.parameters(mboxParameters1)
.build();
TargetPrefetch prefetchRequest1 = new TargetPrefetch("mboxName1", targetParameters1);

TargetParameters targetParameters2 = new TargetParameters.Builder()
.parameters(mboxParameters2)
.product(targetProduct)
.order(targetOrder)
.build();
TargetPrefetch prefetchRequest2 = new TargetPrefetch("mboxName2", targetParameters2);


List<TargetPrefetchObject> prefetchMboxesList = new ArrayList<>();
prefetchMboxesList.add(prefetchRequest1);
prefetchMboxesList.add(prefetchRequest2);


// Call the prefetchContent API.
TargetParamters targetParameters = null;
Target.prefetchContent(prefetchMboxesList, targetParameters, prefetchStatusCallback);
```
{% endtab %}

{% tab title="iOS" %}
### prefetchContent

Use this API to send a prefetch request to your configured Target server with the `ACPTargetPrefetchObject` array and the specified `ACPTargetParameters`. The callback is invoked when the prefetch is complete and, if successful, returns a nil value. If the prefetch is not successful, an error message is returned.

#### Syntax

```objectivec
+ (void) prefetchContent: (nonnull NSArray<ACPTargetPrefetchObject*>*) targetPrefetchObjectArray
withParameters: (nullable ACPTargetParameters*) targetParameters
callback: (nullable void (^) (NSError* _Nullable error)) callback;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```objectivec
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
{% endtab %}
{% endtabs %}

## Clear prefetch offer cache

Use this API to clear prefetched offers cached in memory.

{% tabs %}
{% tab title="Android" %}
### clearPrefetchCache

#### Syntax

```java
public static void clearPrefetchCache()
```

#### Example

```java
Target.clearPrefetchCache();
```
{% endtab %}

{% tab title="iOS" %}
### clearPrefetchCache

#### Syntax

```objectivec
+ (void) clearPrefetchCache;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```objectivec
[ACPTarget clearPrefetchCache];
```

**Swift**

```swift
ACPTarget.clearPrefetchCache()
```
{% endtab %}
{% endtabs %}

## Retrieve Location Content requests

Use this API to send a batch request to the configured Target server for multiple mbox locations. The main difference with the deprecated [loadRequests](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference-deprecated#loadrequests) API is in usage with prefetch APIs. For a prefetched mbox, unlike `loadRequests` API, invoking this API does not send a display notification to the configured Target server. If you are not prefetching mbox content, then there is no difference with `loadRequests` API for sending batch request to Target.

{% tabs %}
{% tab title="Android" %}
### retrieveLocationContent

This API will send a batch request to configured Target server only for mbox locations in the `TargetRequest` list that are not already prefetched. The content for the mbox locations which are already prefetched with a prior prefetch request, will be returned from within the SDK itself. Each `TargetRequest` object in the list contains a callback function, which is invoked when content is available for its given mbox location.

#### Syntax

```java
public static void retrieveLocationContent(final List<TargetRequest> targetRequestList,
                                           final TargetParameters parameters)
```

#### Example

```java
// define parameters for first request
Map<String, Object> mboxParameters1 = new HashMap<>();
mboxParameters1.put("status", "platinum");

// define parameters for second request
Map<String, Object> mboxParameters2 = new HashMap<>();
mboxParameters2.put("userType", "paid");

List<String> purchasedIds = new ArrayList<String>();
purchasedIds.add("34");
purchasedIds.add("125");

TargetOrder targetOrder = new TargetOrder("ADCKKIM", 344.30, purchasedIds);
TargetProduct targetProduct = new TargetProduct("24D3412", "Books");

TargetParameters parameters1 = new TargetParameters.Builder().parameters(mboxParameters1).build();
TargetRequest request1 = new TargetRequest("mboxName1", parameters1, "defaultContent1",
                                            new AdobeCallback<String>() {
                                                @Override
                                                public void call(String value) {
                                                    // do something with target content.
                                                }
                                            });

TargetParameters parameters2 = new TargetParameters.Builder()
                               .parameters(mboxParameters1)
                               .product(targetProduct)
                               .order(targetOrder)
                               .build();
TargetRequest request2 = new TargetRequest("mboxName2", parameters2, "defaultContent2",
                                            new AdobeCallback<String>() {
                                                @Override
                                                public void call(String value) {
                                                    // do something with target content.
                                                }
                                            });

// Creating Array of Request Objects
List<TargetRequest> locationRequests = new ArrayList<>();
locationRequests.add(request1);
locationRequests.add(request2);

 // Define the profile parameters map.
Map<String, Object> profileParameters1 = new HashMap<>();
profileParameters1.put("ageGroup", "20-32");

TargetParameters parameters = new TargetParameters.Builder().profileParameters(profileParameters1).build();

// Call the targetRetrieveLocationContent API.
Target.retrieveLocationContent(locationRequests, parameters);
```
{% endtab %}

{% tab title="iOS" %}
### retrieveLocationContent

This API will send a batch request to configured Target server only for mbox locations in the `TargetRequest` list that are not already prefetched. The content for the mbox locations which are already prefetched with a prior prefetch request, will be returned from within the SDK itself. Each `TargetRequest` object in the list contains a callback function, which is invoked when content is available for its given mbox location.

#### Syntax

```objectivec
+ (void) retrieveLocationContent: (nonnull NSArray<ACPTargetRequestObject*>*) requests
                  withParameters: (nullable ACPTargetParameters*) parameters;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```objectivec
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
{% endtab %}
{% endtabs %}

## Send an mbox display notification

Use this API to send a location \(mbox\) display notification to configured Target server. This API should be invoked for a prefetched mbox, after the mbox content is retrieved using [retrieveLocationContent API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#retrieve-location-content-requests). If no previous prefetch request is made and the mbox content is retrieved using `retrieveLocationContent` API, then calling this API does not trigger a notification request to the Target server.

{% hint style="warning" %}
Do not use this API with the deprecated [loadRequests](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference-deprecated#load-target-requests). For a prefetched mbox, on calling the deprecated `loadRequests` API, mbox display notification is internally sent to the Target server by the SDK.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### locationsDisplayed

#### Syntax

```java
public static void locationsDisplayed(final List<String> mboxNames, final TargetParameters targetParameters)
```

#### Example

```java
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("34");
purchasedProductIds.add("125"); 
TargetOrder targetOrder = new TargetOrder("123", 567.89, purchasedProductIds);

TargetProduct targetProduct = new TargetProduct("123", "Books");

TargetParameters targetParameters = new TargetParameters.Builder()
.parameters(new HashMap<String, String>())
.profileParameters(new HashMap<String, String>())
.product(targetProduct)
.order(targetOrder)
.build();

List<String> mboxList = new ArrayList<>();
mboxList.add("mboxName1");

Target.locationsDisplayed(mboxList, targetParameters);
```
{% endtab %}

{% tab title="iOS" %}
### locationsDisplayed

#### Syntax

```objectivec
+ (void) locationsDisplayed: (nonnull NSArray<NSString*>*) mboxNames 
withTargetParameters: (nullable ACPTargetParameters*) targetParameters;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```objectivec
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];

ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];

ACPTargetParameters *targetParameters = [ACPTargetParameters targetParametersWithParameters:nil
profileParameters:nil
product:product
order:order];

[ACPTarget locationsDisplayed:@[@"mboxName1", @"mboxName2"] withTargetParameters:targetParameters];
```

**Swift**

```swift
let product = ACPTargetProduct(id: "24D334", categoryId: "Stationary")

let order = ACPTargetOrder(id: "ADCKKBC", total: NSNumber(value: 400.50), purchasedProductIds: ["34", "125"])

let targetParameters = ACPTargetParameters(parameters: nil, profileParameters: nil, product: product, order: order)

ACPTarget.locationsDisplayed(["mboxName1", "mboxName2"], with: targetParameters)
```
{% endtab %}
{% endtabs %}

## Send an mbox click notification

Use this API to send a location \(mbox\) click notification to configured Target server. This API can be invoked in the following cases:

* For a prefetched mbox, after the mbox content is retrieved using [retrieveLocationContent API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#retrieve-location-content-requests).
* For a regular mbox when no previous prefetch request is made and the mbox content is retrieved using `retrieveLocationContent` API.

{% hint style="warning" %}
For a click notification to be sent to Target, make sure click metric is enabled for the given mbox name in Target.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### locationClicked

#### Syntax

```java
public static void locationClicked(final String mboxName, final TargetParameters parameters)
```

#### Example

```java
// Mbox parameters
Map<String, Object> mboxParameters = new HashMap<>();
mboxParameters.put("membership", "prime");

// Product parameters
Map<String, Object> productParameters = new HashMap<>();
productParameters.put("id", "CEDFJC");
productParameters.put("categoryId","Electronics");

List<String> purchasedIds = new ArrayList<String>();
purchasedIds.add("81");
purchasedIds.add("123");
purchasedIds.add("190");

// Order parameters
Map<String, Object> orderParameters = new HashMap<>();
orderParameters.put("id", "NJJICK");
orderParameters.put("total", "650");
orderParameters.put("purchasedProductIds",  purchasedIds);

// Profile parameters
Map<String, Object> profileParameters = new HashMap<>();
profileParameters.put("ageGroup", "20-32");

// Create Target Parameters
TargetOrder targetOrder = new TargetOrder("NJJICK", "650", purchasedIds);
TargetProduct targetProduct = new TargetProduct("CEDFJC", "Electronics");
TargetParameters targetParameters = new TargetParameters.Builder(mboxParameters)
                                .profileParameters(profileParameters)
                                .order(targetOrder)
                                .product(targetProduct)
                                .build();

Target.locationClicked("cartLocation", targetParameters);
```
{% endtab %}

{% tab title="iOS" %}
### locationClicked

#### Syntax

```objectivec
+ (void) locationClickedWithName: (nonnull NSString*) name targetParameters: (nullable ACPTargetParameters*) parameters;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```objectivec
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
{% endtab %}
{% endtabs %}

## Public classes

{% tabs %}
{% tab title="Android" %}
### TargetRequest

Here is a code sample for this class in Android:

```java
public class TargetRequest extends TargetObject {

    /**
     * Instantiate a TargetRequest object
     * @param mboxName String mbox name for this request
     * @param targetParameters TargetParameters for this request
     * @param defaultContent String default content for this request
     * @param contentCallback AdobeCallback<String> which will get called with Target mbox content
     */
    public TargetRequest(final String mboxName,
                         final TargetParameters targetParameters,
                         final String defaultContent,
                         final AdobeCallback<String> contentCallback);

     /**
     * Sets mbox parameters for the request.
     *
     * @param mboxParameters Map<String, String> mbox parameters
     */
     void setMboxParameters(final Map<String, String> mboxParameters);

     /**
     * Sets profile parameters for the request.
     *
     * @param profileParameters Map<String, String profile parameters
     */
    void setProfileParameters(final Map<String, String> profileParameters);

    /**
     * Sets order parameters for the request.
     *
     * @param orderParameters Map<String, Object> order parameters
     */
    void setOrderParameters(final Map<String, Object> orderParameters);

    /**
     * Sets product parameters for the request.
     *
     * @param productParameters Map<String, String> product parameters
     */
    void setProductParameters(final Map<String, String> productParameters);

    /**
     * Sets targetParameters for the request.
     *
     * @param targetParameters TargetParameters for the request.
     */
    void setTargetParameters(final TargetParameters targetParameters);
}
```

### TargetPrefetch

Here is a code sample for this class in Android:

```java
public class TargetPrefetch extends TargetObject {

    /**
     * Instantiate a TargetPrefetch object
     * @param mboxName String mbox name for this prefetch request
     * @param targetParameters TargetParameters for this prefetch request
     */
     public TargetPrefetch(final String mboxName, final TargetParameters targetParameters)

     /**
     * Sets mbox parameters for the request.
     *
     * @param mboxParameters Map<String, String> mbox parameters
     */
     void setMboxParameters(final Map<String, String> mboxParameters);

     /**
     * Sets profile parameters for the request.
     *
     * @param profileParameters Map<String, String profile parameters
     */
    void setProfileParameters(final Map<String, String> profileParameters);

    /**
     * Sets order parameters for the request.
     *
     * @param orderParameters Map<String, Object> order parameters
     */
    void setOrderParameters(final Map<String, Object> orderParameters);

    /**
     * Sets product parameters for the request.
     *
     * @param productParameters Map<String, String> product parameters
     */
    void setProductParameters(final Map<String, String> productParameters);

    /**
     * Sets targetParameters for the request.
     *
     * @param targetParameters TargetParameters for the request.
     */
    void setTargetParameters(final TargetParameters targetParameters);

}
```

### TargetParameters

Here is a code sample for this class in Android:

```java
public class TargetParameters {

    private TargetParameters() {}

    /**
    * Builder used to construct a TargetParameters object
    */
    public static class Builder {
        private Map<String, String> parameters;
        private Map<String, String> profileParameters;
        private TargetProduct product;
        private TargetOrder order;

        /**
         * Create a TargetParameters object Builder
         */
        public Builder() {}

        /**
         * Create a TargetParameters object Builder
         *
         * @param parameters mbox parameters for the built TargetParameters
         */
        public Builder(final Map<String, String> parameters);

        /**
         * Set mbox parameters on the built TargetParameters
         *
         * @param parameters mbox parameters map
         * @return this builder
         */
        public Builder parameters(final Map<String, String> parameters);

        /**
         * Set profile parameters on the built TargetParameters
         *
         * @param profileParameters profile parameters map
         * @return this builder
         */
        public Builder profileParameters(final Map<String, String> profileParameters);

        /**
         * Set product parameters on the built TargetParameters
         *
         * @param product product parameters
         * @return this builder
         */
        public Builder product(final TargetProduct product);

        /**
         * Set order parameters on the built TargetParameters
         *
         * @param order order parameters
         * @return this builder
         */
        public Builder order(final TargetOrder order);

        /**
         * Build the TargetParameters object
         *
         * @return the built TargetParameters object
         */
        public TargetParameters build();
    }
}
```

### TargetOrder

Here is a code sample for this class in Android:

```java
public class TargetOrder {

    /**
     * Initialize a TargetOrder with an order id, order total and a list of purchasedProductIds
     *
     * @param id String order id
     * @param total double order total amount
     * @param purchasedProductIds a list of purchased product ids
     */
    public TargetOrder(final String id, final double total, final List<String> purchasedProductIds);
    /**
     * Get the order id
     *
     * @return order id
     */
    public String getId();

    /**
     * Get the order total
     *
     * @return order total
     */
    public double getTotal();

    /**
     * Get the order purchasedProductIds
     *
     * @return a list of this order's purchased product ids
     */
    public List<String> getPurchasedProductIds();

    /**
     * Converts an order parameter Map to a TargetOrder
     *
     * @param orderParameters a Map<String, Object> of Target order parameters
     * @return converted TargetOrder
     */
    static TargetOrder fromMap(final Map<String, Object> orderParameters);

    /**
     * Converts TargetOrder to an order parameters Map.
     *
     * @param targetOrder a TargetOrder object
     * @return Map<String, Object> containing Target order parameters
     */
    static Map<String, Object> toMap(final TargetOrder targetOrder);

}
```

### TargetProduct

Here is a code sample for this class in Android:

```java
public class TargetProduct {

    /**
     * Initialize a TargetProduct with a product id and a productCategoryId categoryId
     *
     * @param id String product id
     * @param categoryId String product category id
     */
     public TargetProduct(final String id, final String categoryId);

    /**
     * Get the product id
     *
     * @return product id
     */
    public String getId();

    /**
     * Get the product categoryId
     *
     * @return product category id
     */
    public String getCategoryId();

    /**
     * Converts a product parameter Map to a TargetProduct
     *
     * @param productParameters a Map<String, String> of Target product parameters
     * @return converted TargetProduct
     */
    static TargetProduct fromMap(final Map<String, String> productParameters);

    /**
     * Converts a TargetProduct object to product parameters Map.
     *
     * @param targetProduct a TargetProduct object
     * @return Map<String, String> containing Target product parameters
     */
     static Map<String, String> toMap(final TargetProduct targetProduct);
}
```
{% endtab %}

{% tab title="iOS" %}
### ACPTargetRequestObject

This class extends `ACPTargetPrefetchObject` by adding default content and a callback block that will be invoked to return mbox content from Target.

```objectivec
@interface ACPTargetRequestObject : ACPTargetPrefetchObject

/* The default content that will be returned if Target servers are unreachable */   
@property(nonatomic, strong, nonnull) NSString* defaultContent;

/* Optional. When batch requesting Target locations, callback will be invoked when content is available for this location. */
@property(nonatomic, strong, nullable) void (^callback)(NSString* __nullable content);
@end
```

The following method can be used to create an instance of ACPTargetRequestObject that might be used to make a batch request to the configured Target server to fetch content for mbox locations.

```objectivec
+ (nonnull instancetype) targetRequestObjectWithName: (nonnull NSString*) name
                                    targetParameters: (nullable ACPTargetParameters*) targetParameters
                                      defaultContent: (nonnull NSString*) defaultContent
                                            callback: (nullable void (^) (NSString* __nullable content)) callback;
```

### ACPTargetPrefetchObject

This class contains the name of the Target location/mbox and target parameters to be used in a prefetch request.

```objectivec
@interface ACPTargetPrefetchObject : NSObject

/* The name of the Target location/mbox */
@property(nonatomic, strong, nullable) NSString* name;

/* Target parameters associated with the prefetch object. You can set all other parameters in this object */
@property(nonatomic, strong, nullable) ACPTargetParameters* targetParameters;
@end
```

The following method can be used to create an instance of ACPTargetPrefetchObject that might be used to make a prefetch request to the configured Target server to prefetch content for mbox locations.

```objectivec
+ (nonnull instancetype) targetPrefetchObjectWithName: (nonnull NSString*) name
                                     targetParameters: (nullable ACPTargetParameters*) targetParameters;
```

### ACPTargetParameters

This class contains mbox parameters dictionary, profile parameters dictionary, ACPTargetOrder object as well as ACPTargetProduct object.

```objectivec
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

```objectivec
+ (nonnull instancetype) targetParametersWithParameters: (nullable NSDictionary*) parameters
                                      profileParameters: (nullable NSDictionary*) profileParameters
                                                product: (nullable ACPTargetProduct*) product
                                                  order: (nullable ACPTargetOrder*) order;
```

### ACPTargetOrder

This class contains orderId, total and an array for purchasedProductIds.

```objectivec
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

```objectivec
+ (nonnull instancetype) targetOrderWithId: (nonnull NSString*) orderId
                                     total: (nullable NSNumber*) total
                       purchasedProductIds: (nullable NSArray <NSString*>*) purchasedProductIds;
```

### ACPTargetProduct

This class contains productId and categoryId.

```objectivec
@interface ACPTargetProduct : NSObject

/* Product ID */
@property(nonatomic, strong, nullable) NSString* productId;

/* Category ID */
@property(nonatomic, strong, nullable) NSString* categoryId;
@end
```

The following method can be used to create an instance of ACPTargetProduct.

```objectivec
+ (nonnull instancetype) targetProductWithId: (nonnull NSString*) productId
                                  categoryId: (nullable NSString*) categoryId;
```
{% endtab %}
{% endtabs %}

