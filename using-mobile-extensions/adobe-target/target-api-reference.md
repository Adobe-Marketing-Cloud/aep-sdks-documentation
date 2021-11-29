# Target API reference

## Target API reference

### clearPrefetchCache

This API clears the in-memory cache that contains the prefetched offers.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```text
public static void clearPrefetchCache()
```

**Example**

```text
Target.clearPrefetchCache();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func clearPrefetchCache()
```

**Example**

**Swift**

```swift
Target.clearPrefetchCache()
```

**Objective-C**

```text
[AEPMobileTarget clearPrefetchCache];
```
{% endtab %}
{% endtabs %}

### clickedLocation

This API sends a location click notification for an mbox to the configured Target server and can be invoked in the following cases:

* For a prefetched mbox, after the mbox content is retrieved using the `retrieveLocationContent` API.
* For a regular mbox, where no previous prefetch request is made, and the mbox content is retrieved using the `retrieveLocationContent` API.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void locationClicked(final String mboxName, final TargetParameters parameters)
```

* _mboxName_ is a String that contains the mbox location for which the click notification will be sent to Target.
* _parameters_ is the configured `TargetParameters` for the request.

**Example**

```java
// Mbox parameters
Map<String, String> mboxParameters = new HashMap<>();
mboxParameters.put("membership", "prime");

// Product parameters
TargetProduct targetProduct = new TargetProduct("CEDFJC", "Electronics");


// Order parameters
List<String> purchasedIds = new ArrayList<String>();
purchasedIds.add("81");
purchasedIds.add("123");
purchasedIds.add("190");
TargetOrder targetOrder = new TargetOrder("NJJICK", "650", purchasedIds);

// Profile parameters
Map<String, String> profileParameters = new HashMap<>();
profileParameters.put("ageGroup", "20-32");

// Create Target Parameters
TargetParameters targetParameters = new TargetParameters.Builder(mboxParameters)
                                .profileParameters(profileParameters)
                                .order(targetOrder)
                                .product(targetProduct)
                                .build();

Target.locationClicked("cartLocation", targetParameters);
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func clickedLocation(_ name: String, targetParameters: TargetParameters?)
```

* _name_ : a `String` that contains the mbox location for which the click notification will be sent to Target.
* _targetParameters_ : the configured `TargetParameters` for the request.

**Example**

**Swift**

```swift
Target.clickedLocation("aep-loc-1", targetParameters: TargetParameters(parameters: ["mbox_parameter_key": "mbox_parameter_value"], profileParameters: ["name": "Smith"], order: TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"]), product: TargetProduct(productId: "pId1", categoryId: "cId1")))
```

**Objective-C**

```text
AEPTargetOrder *order = [[AEPTargetOrder alloc] initWithId:@"id1" total:1.0 purchasedProductIds:@[@"ppId1"]];
AEPTargetProduct *product =[[AEPTargetProduct alloc] initWithProductId:@"pId1" categoryId:@"cId1"];
AEPTargetParameters * targetParams = [[AEPTargetParameters alloc] initWithParameters:@{@"mbox_parameter_key":@"mbox_parameter_value"} profileParameters:@{@"name":@"Smith"} order:order product:product];
[AEPMobileTarget clickedLocation:@"aep-loc-1" withTargetParameters:targetParams];
```
{% endtab %}
{% endtabs %}

### displayedLocations

This API sends a location display notification for an mbox to the configured Target server. The API should be invoked for a prefetched mbox after the mbox content is retrieved using the `retrieveLocationContent` API. If no previous prefetch request is made, and the mbox content is retrieved using the `retrieveLocationContent` API, calling this API does not trigger a notification request to the Target server.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void locationsDisplayed(final List<String> mboxNames, final TargetParameters targetParameters)
```

* _mboxNames_ is a list of the mbox locations for which the display notification will be sent to Target.
* _targetParameters_ is the configured `TargetParameters` for the request.

**Example**

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

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func displayedLocations(_ names: [String], targetParameters: TargetParameters?)
```

* _names_ : is an `array` of the mbox locations for which the display notification will be sent to Target.
* _targetParameters_ : is the configured `TargetParameters` for the request.

**Example**

**Swift**

```swift
Target.displayedLocations(
              ["mboxName1", "mboxName2"], 
        targetParameters: TargetParameters(
        parameters: nil,
        profileParameters: nil,
        order: TargetOrder(id: "ADCKKBC", total: 400.50, purchasedProductIds: ["34", "125"]),
        product: TargetProduct(productId: "24D334", categoryId: "Stationary")
        )
)
```

**Objective-C**

```text
AEPTargetOrder *order = [[AEPTargetOrder alloc] initWithId:@"ADCKKBC" total:400.50 purchasedProductIds:@[@"34", @"125"]];
AEPTargetProduct *product =[[AEPTargetProduct alloc] initWithProductId:@"24D334" categoryId:@"Stationary"];
AEPTargetParameters * targetParams = [[AEPTargetParameters alloc] initWithParameters:nil profileParameters:nil order:order product:product];
[AEPMobileTarget displayedLocations:@[@"mboxName1", @"mboxName2"] withTargetParameters:targetParams];
```
{% endtab %}
{% endtabs %}

### extensionVersion

Returns the running version of the Target extension.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public String extensionVersion()
```

**Example**

```java
Target.extensionVersion();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static var extensionVersion: String
```

**Example**

**Swift**

```swift
let targetVersion = Target.extensionVersion
```

**Objective-C**

```text
NSString *targetVersion = [AEPMobileTarget extensionVersion];
```
{% endtab %}
{% endtabs %}

### getThirdPartyId

This API gets the custom visitor ID for Target. If no `third-party` ID was previously set, or if the ID was reset by calling resetExperience API, it will have a `nil` value.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void getThirdPartyId(final AdobeCallback<String> callback)
```

* _callback_ is invoked with the `thirdPartyId` value. If no third-party ID was set, this value will be `null`.

**Example**

```java
Target.getThirdPartyId(new AdobeCallback<String>() {                    
    @Override
    public void call(String thirdPartyId) {
                // read Target thirdPartyId
    }
});
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func getThirdPartyId(_ completion: @escaping (String?, Error?) -> Void)
```

* _completion_ : invoked with the `thirdPartyId` value. If no `third-party` ID was set, this value will be `nil`.

**Example**

**Swift**

```swift
Target.getThirdPartyId { (id, err) in
    // read Target thirdPartyId
}
```

**Objective-C**

```text
[AEPMobileTarget getThirdPartyId:^(NSString *thirdPartyID, NSError *error){
    // read Target thirdPartyId
}];
```
{% endtab %}
{% endtabs %}

### getTntId

This API gets the Target user ID \(also known as the `tntId`\) from the Target service. The `tntId` is returned in the network response after a successful call to `prefetchContent` or `retrieveLocationContent`, which is then persisted in the SDK. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when the `resetExperience` API is used.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void getTntId(final AdobeCallback<String> callback)
```

* _callback_ is invoked with the `tntId` value. If no Target ID was set, this value will be `null`. 

**Example**

```java
Target.getTntId(new AdobeCallback<String>() {
    @Override
    public void call(String tntId) {
        // read target's tntid
    }
});
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func getTntId(_ completion: @escaping (String?, Error?) -> Void)
```

* _completion_ : invoked with the `tntId` value. If no Target ID was set, this value will be `nil`.

**Example**

**Swift**

```swift
Target.getTntId({ (id, err) in
    // read target's tntId        
})
```

**Objective-C**

```text
[AEPMobileTarget getTntId:^(NSString *tntID, NSError *error){
    // read target's tntId 
}];
```
{% endtab %}
{% endtabs %}

### prefetchContent

This API sends a prefetch request to your configured Target server. The prefetch request is sent with the prefetch objects array and the specified Target parameters.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void prefetchContent(final List<TargetPrefetch> mboxPrefetchList, final TargetParameters parameters, final AdobeCallback<String> callback)
```

* _mboxPrefetchList_ is a list of `TargetPrefetch` objects for various mbox locations.
* _parameters_ is the configured `TargetParameters` for the prefetch request.
* If the prefetch is successful, _callback_ is invoked with a `null` value. If the prefetch is not successful, an error message is returned.

**Example**

```java
// first prefetch request
Map<String, String> mboxParameters1 = new HashMap<>();
mboxParameters1.put("status", "platinum");

TargetParameters targetParameters1 = new TargetParameters.Builder()
.parameters(mboxParameters1)
.build();

TargetPrefetch prefetchRequest1 = new TargetPrefetch("mboxName1", targetParameters1);

// second prefetch request
Map<String, String> mboxParameters2 = new HashMap<>();
mboxParameters2.put("userType", "paid");

List<String> purchasedIds = new ArrayList<String>();
purchasedIds.add("34");
purchasedIds.add("125");
TargetOrder targetOrder = new TargetOrder("ADCKKIM", 344.30, purchasedIds);

TargetProduct targetProduct = new TargetProduct("24D3412", "Books");

TargetParameters targetParameters2 = new TargetParameters.Builder()
.parameters(mboxParameters2)
.product(targetProduct)
.order(targetOrder)
.build();

TargetPrefetch prefetchRequest2 = new TargetPrefetch("mboxName2", targetParameters2);

List<TargetPrefetch> prefetchMboxesList = new ArrayList<>();
prefetchMboxesList.add(prefetchRequest1);
prefetchMboxesList.add(prefetchRequest2);

// Call the prefetchContent API.
TargetParamters targetParameters = null;
Target.prefetchContent(prefetchMboxesList, targetParameters, prefetchStatusCallback);
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func prefetchContent(_ prefetchArray: [TargetPrefetch], with targetParameters: TargetParameters? = nil, _ completion: ((Error?) -> Void)?)
```

* _prefetchArray_ - is an array of `TargetPrefetch` objects for various mbox locations.
* _targetParameters_ - is the configured `TargetParameters` for the prefetch request.
* If the prefetch is successful, `completion` is invoked with a nil value. If the prefetch is not successful, an error message is returned.

**Example**

**Swift**

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

Target.prefetchContent([
    TargetPrefetch(name: "mboxName1", targetParameters: TargetParameters1),
    TargetPrefetch(name: "mboxName2", targetParameters: TargetParameters2),
    ],
    with: globalTargetParameters
    ){ error in
        // do something with the callback response
}
```

**Objective-C**

```text
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

{% tab title="iOS \(AEP 3.x\)" %}
This API no longer exists in `Target`. Instead, the extension should be registered by calling the `registerExtensions` API in the MobileCore. Please see the updated SDK initialization steps at the [migrate to Swift tutorial.](../../resources/migrate-to-swift.md#update-sdk-initialization)
{% endtab %}
{% endtabs %}

### resetExperience

This API resets the user's experience by removing the visitor identifiers and resetting the Target session. Invoking this API also removes previously set Target user ID and custom visitor IDs, Target Edge Host, and the session information from persistent storage.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void resetExperience()
```

**Example**

```java
Target.resetExperience();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func resetExperience()
```

**Example**

**Swift**

```swift
Target.resetExperience()
```

**Objective-C**

```text
[AEPMobileTarget resetExperience];
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
{% tab title="Android" %}
**Syntax**

```java
public static void retrieveLocationContent(final List<TargetRequest> targetRequestList, final TargetParameters parameters)
```

* _targetRequestList_ is a list of `TargetRequest` objects for various mbox locations.
* _parameters_ is the configured `TargetParameters` for the retrieve location request.

**Example**

```java
// define parameters for first request
Map<String, String> mboxParameters1 = new HashMap<>();
mboxParameters1.put("status", "platinum");

TargetParameters parameters1 = new TargetParameters.Builder().parameters(mboxParameters1).build();

TargetRequest request1 = new TargetRequest("mboxName1", parameters1, "defaultContent1",
                                            new AdobeCallback<String>() {
                                                @Override
                                                public void call(String value) {
                                                    // do something with target content.
                                                }
                                            });

// define parameters for second request
Map<String, String> mboxParameters2 = new HashMap<>();
mboxParameters2.put("userType", "paid");

List<String> purchasedIds = new ArrayList<String>();
purchasedIds.add("34");
purchasedIds.add("125");
TargetOrder targetOrder = new TargetOrder("ADCKKIM", 344.30, purchasedIds);

TargetProduct targetProduct = new TargetProduct("24D3412", "Books");

TargetParameters parameters2 = new TargetParameters.Builder()
                               .parameters(mboxParameters2)
                               .product(targetProduct)
                               .order(targetOrder)
                               .build();

TargetRequest request2 = new TargetRequest("mboxName2", parameters2, "defaultContent2",
                                            new AdobeTargetDetailedCallback() {
                                                @Override
                                                public void call(final String content, final Map<String, Object> data) {
                                                    if (content != null && !content.isEmpty()) {
                                                        // do something with the target content.
                                                    }

                                                    // Read the data Map containing one or more of response tokens, analytics payload 
                                                    // and click metric analytics payload, if available
                                                    if (data != null && !data.isEmpty()) {

                                                        Map<String, String> responseTokens = data.containsKey("responseTokens") ? 
                                                                                            (Map<String, String>) data.get("responseTokens") : 
                                                                                            null;

                                                        Map<String, String> analyticsPayload = data.containsKey("analytics.payload") ? 
                                                                                              (Map<String, String>) data.get("analytics.payload") : 
                                                                                              null;

                                                        Map<String, String> clickMetricAnalyticsPayload = data.containsKey("clickmetric.analytics.payload") ? 
                                                                                                          (Map<String, String>) data.get("clickmetric.analytics.payload") : 
                                                                                                          null;

                                                        ...
                                                    }
                                                }

                                                @Overrides
                                                void fail(final AdobeError error) {
                                                    // take appropriate action upon error.
                                                }
                                            });

// Creating Array of Request Objects
List<TargetRequest> locationRequests = new ArrayList<>();
locationRequests.add(request1);
locationRequests.add(request2);

 // Define the profile parameters map.
Map<String, String> profileParameters1 = new HashMap<>();
profileParameters1.put("ageGroup", "20-32");

TargetParameters parameters = new TargetParameters.Builder().profileParameters(profileParameters1).build();

// Call the targetRetrieveLocationContent API.
Target.retrieveLocationContent(locationRequests, parameters);
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func retrieveLocationContent(_ requestArray: [TargetRequest], with targetParameters: TargetParameters? = nil)
```

* _requestArray_ - an array of `TargetRequest` objects to retrieve content
* _targetParameters_ - a `TargetParameters` object containing parameters for all locations in the requests array

**Example**

**Swift**

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

let request1 = TargetRequest(mboxName: "logo", defaultContent: "BlueWhale", targetParameters: TargetParameters1) { content in
    if let content = content {
        // do something with the target content.
    }
}
let request2 = TargetRequest(mboxName: "logo", defaultContent: "red", targetParameters: TargetParameters2) { content, data in
        if let content = content {
        // do something with the target content.
    }

    // Read the data dictionary containing one or more of response tokens, analytics payload and click-tracking analytics payload, if available.
    if let data = data {
        let responseTokens = data["responseTokens"] as? [String: String] ?? [:]

        let analyticsPayload = data["analytics.payload"] as? [String: String] ?? [:]

        let clickMetricAnalyticsPayload = data["clickmetric.analytics.payload"] as? [String: String] ?? [:]
        ...
    }
}
Target.retrieveLocationContent([request1, request2], with: globalTargetParameters)
```

**Objective-C**

```text
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
    NSString *targetContent = content ?: @"";
}];
AEPTargetRequestObject *request2 = [[AEPTargetRequestObject alloc] initWithMboxName: @"logo" defaultContent: @"red" targetParameters: targetParameters2 contentWithDataCallback:^(NSString * _Nullable content, NSDictionary<NSString *,id> * _Nullable data) {
    // do something with the target content.
    NSString *targetContent = content ?: @"";

    // Read the data dictionary containing one or more of response tokens, analytics payload and click-tracking analytics payload, if available.      
    if ([data count] > 0) {
        if ([data objectForKey:@"responseTokens"]) {
            // read response tokens
        }

        if ([data objectForKey:@"analytics.payload"]) {
          // read analytics payload
        }

        if ([data objectForKey:@"clickmetric.analytics.payload"]) {
          // read click-tracking analytics payload
        }
    }   
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
{% endtab %}
{% endtabs %}

### setPreviewRestartDeepLink

This API sets a specific location in the app to be displayed when preview mode selections have been confirmed.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void setPreviewRestartDeepLink(final Uri deepLink)
```

* _deeplink_ is a Uri that contains the preview restart deeplink.

**Example**

```java
Target.setPreviewRestartDeepLink("myapp://HomePage");
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func setPreviewRestartDeepLink(_ deeplink: URL)
```

* _deeplink_ : a `URL` that contains the preview restart deeplink.

**Example**

**Swift**

```swift
if let url = URL(string: "myapp://HomePage") {
    Target.setPreviewRestartDeepLink(url)
}
```

**Objective-C**

```text
[AEPMobileTarget setPreviewRestartDeepLink:@"myapp://HomePage"];
```
{% endtab %}
{% endtabs %}

### setThirdPartyId

This API sets the custom visitor ID for Target. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when the resetExperience API is used.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void setThirdPartyId(final String thirdPartyId)
```

* _thirdPartyId_ is a String that contains the custom visitor ID to be set in Target.

**Example**

```java
Target.setThirdPartyId("third-party-id");
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Syntax**

```swift
static func setThirdPartyId(_ id: String)
```

* _id_ : a `String` that contains the custom visitor ID to be set in Target.

**Example**

**Swift**

```swift
Target.setThirdPartyId("third-party-id")
```

**Objective-C**

```text
[AEPMobileTarget setThirdPartyId:@"third-party-id"]
```
{% endtab %}
{% endtabs %}

### Visual preview

Target visual preview mode allows you to easily perform end-to-end QA activities by enrolling and previewing these activities on your device. This mode does not require a specialized testing set up. To get started, set up a URL scheme and generate the preview links.

{% tabs %}
{% tab title="Android" %}
On Android, when the application is launched as a result of a deep link, the `collectLaunchInfo` API is internally invoked, and the Target activity and deep link information is extracted from the Intent extras.

{% hint style="info" %}
The SDK can only collect information from the launching Activity if [`setApplication`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#application-reference-android-only) has been called. Setting the Application is only necessary on an Activity that is also an entry point for your application. However, setting the Application on each Activity has no negative impact and ensures that the SDK always has the necessary reference to your Application. We recommend that you call `setApplication` in each of your Activities.
{% endhint %}
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
To enter the preview visual mode, use the `collectLaunchInfo` API to enable the mode and click the red floating button that appears on the app screen.

**Syntax**

```swift
public static func collectLaunchInfo(_ userInfo: [String: Any])
```

* _userInfo_ : Dictionary of data relevant to the expected use case.

**Example**

**Swift**

```swift
MobileCore.collectLaunchInfo(["adb_deeplink" : "com.adobe.targetpreview://app.adobetarget.com?at_preview_token=tokenFromTarget"])
```

**Objective-C**

```text
[AEPMobileCore collectLaunchInfo: @{@"adb_deeplink":@"com.adobe.targetpreview://app.adobetarget.com?at_preview_token=tokenFromTarget"}];
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
    * Instantiate a TargetRequest object.
    *
    * @param mboxName String mbox name for this request.
    * @param targetParameters TargetParameters for this request.
    * @param defaultContent String default content for this request.
    * @param contentWithDataCallback AdobeTargetDetailedCallback which will get called with Target mbox content and other optional data such as Target response tokens, analytics payload, click metric analytics payload if available.
    */
    public TargetRequest(final String mboxName, 
                         final TargetParameters targetParameters, 
                         final String defaultContent,
                         final AdobeTargetDetailedCallback contentWithDataCallback);
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
}
```

### AdobeTargetDetailedCallback

A sample of this interface on Android can be seen below:

```java
public interface AdobeTargetDetailedCallback {

    /**
     * Callback function to pass the mbox content and other mbox payload values.
     *
     * @param content {@code String} mox content
     * @param data A {@code Map<String, Object>} of mbox payload values. It will be null if neither response tokens nor analytics payload is available.
     */
    void call(final String content, final Map<String, Object> data);

    /**
     * Callback function for notifying about the internal error in getting mbox details.
     *
     * @param error {@link AdobeError} represents the internal error occurred.
     */
    void fail(final AdobeError error);
}
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
### TargetRequest

```swift
@objc(AEPTargetRequestObject)
public class TargetRequest: NSObject, Codable {
    @objc public let name: String
    @objc public let defaultContent: String
    @objc public let targetParameters: TargetParameters?
    @objc let responsePairId: String
    @objc var contentCallback: ((String?) -> Void)?

    /// Instantiate a `TargetRequest` object
    /// - Parameters:
    ///   - name: `String` mbox name for this request
    ///   - defaultContent: `String` default content for this request
    ///   - targetParameters: `TargetParameters` for this request
    ///   - contentCallback: which will get called with target mbox content
    @objc public init(mboxName: String, defaultContent: String, targetParameters: TargetParameters? = nil, contentCallback: ((String?) -> Void)? = nil) {
        name = mboxName
        self.defaultContent = defaultContent
        self.targetParameters = targetParameters
        self.contentCallback = contentCallback
        contentWithDataCallback = nil
        responsePairId = UUID().uuidString
    }

    /// Instantiate a `TargetRequest` object
    /// - Parameters:
    ///   - name: `String` mbox name for this request
    ///   - defaultContent: `String` default content for this request
    ///   - targetParameters: `TargetParameters` for this request
    ///   - contentWithDataCallback: which will get called with target mbox content, and an optional dictionary containing one or more of response tokens, analytics payload, and click metric analytics payload, if available.
    @objc public init(mboxName: String, defaultContent: String, targetParameters: TargetParameters? = nil, contentWithDataCallback: ((String?, [String: Any]?) -> Void)? = nil) {
        name = mboxName
        self.defaultContent = defaultContent
        self.targetParameters = targetParameters
        self.contentWithDataCallback = contentWithDataCallback
        contentCallback = nil
        responsePairId = UUID().uuidString
    }
}
```

The following example shows how to create an instance of a TargetRequest object that might be used to make a batch request to the configured Target server to fetch content for mbox locations.

**Swift**

```swift
let request1 = TargetRequest(mboxName: "mboxName", defaultContent: "default content", targetParameters: nil, contentCallback: { content in
    print(content ?? "")
})

let request2 = TargetRequest(mboxName: "mboxName", defaultContent: "default content", targetParameters: nil, contentwithDataCallback: { content, data in
    print(content ?? "")

  if let data = data {
      // read response tokens
      let responseTokens = data["responseTokens"] as? [String: String] ?? [:]

      // read analytics payload
      let analyticsPayload = data["analytics.payload"] as? [String: String] ?? [:]

      // read click-tracking analytics payload
      let clickMetricAnalyticsPayload = data["clickmetric.analytics.payload"] as? [String: String] ?? [:]
  }
})
```

**Objective-C**

```text
AEPTargetRequestObject *request1 = [[AEPTargetRequestObject alloc] initWithMboxName:@"mboxName" defaultContent:@"defaultContent" targetParameters:nil contentCallback:^(NSString * _Nullable content) {
      NSLog(@"%@", content ?: @"");
}];

AEPTargetRequestObject *request2 = [[AEPTargetRequestObject alloc] initWithMboxName: @"logo" defaultContent: @"red" targetParameters: targetParameters2 contentWithDataCallback:^(NSString * _Nullable content, NSDictionary<NSString *,id> * _Nullable data) {
    NSLog(@"%@", content ?: @"");

    if ([data count] > 0) {
        if ([data objectForKey:@"responseTokens"]) {
            // read response tokens
        }

        if ([data objectForKey:@"analytics.payload"]) {
          // read analytics payload
        }

        if ([data objectForKey:@"clickmetric.analytics.payload"]) {
          // read click-tracking analytics payload
        }
    }   
}];
```

### TargetPrefetch

This class contains the name of the Target location/mbox and target parameters to be used in a prefetch request.

```swift
/// `TargetPrefetch` class, used for specifying a mbox location.
@objc(AEPTargetPrefetchObject)
public class TargetPrefetch: NSObject, Codable {
    @objc public let name: String
    @objc public let targetParameters: TargetParameters?

    /// Instantiate a `TargetPrefetch` object
    /// - Parameters:
    ///   - name: `String` mbox name for this prefetch
    ///   - targetParameters: `TargetParameters` for this prefetch
    @objc public init(name: String, targetParameters: TargetParameters? = nil) {
        self.name = name
        self.targetParameters = targetParameters
    }
}
```

The following example can be used to create an instance of a TargetPrefetch object that might be used to make a prefetch request to the configured Target server to prefetch content for mbox locations.

**Swift**

```swift
let prefetch = TargetPrefetch(name: "mboxName", targetParameters: nil)
```

**Objective-C**

```text
AEPTargetPrefetchObject *prefetch = [[AEPTargetPrefetchObject alloc] initWithName:@"mboxName" targetParameters:nil];
```

### TargetParameters

This class may optionally contain the mbox parameters dictionary, the profile parameters dictionary, the TargetOrder object, as well as the TargetProduct object.

```swift
/// Target parameter class, used for specifying custom parameters to be sent in Target requests,
/// such as location (former mbox) parameters, profile parameters, order/product parameters.
@objc(AEPTargetParameters)
public class TargetParameters: NSObject, Codable {
    @objc public let parameters: [String: String]?
    @objc public let profileParameters: [String: String]?
    @objc public let order: TargetOrder?
    @objc public let product: TargetProduct?

    /// Initialize a `TargetParameters` with the mbox parameters, the profile parameters, the order parameters and the product parameters.
    /// - Parameters:
    ///   - parameters: the mbox parameters
    ///   - profileParameters: the profile parameters
    ///   - order: the order parameters
    ///   - product: the product parameters
    @objc public init(parameters: [String: String]? = nil, profileParameters: [String: String]? = nil, order: TargetOrder? = nil, product: TargetProduct? = nil) {
        self.parameters = parameters
        self.profileParameters = profileParameters
        self.order = order
        self.product = product
    }
}
```

The following example can be used to create an instance of a TargetParameters object.

**Swift**

```swift
let targetParameters = TargetParameters(parameters: ["mbox_parameter_key": "mbox_parameter_value"], profileParameters: ["name": "Smith"], order: TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"]), product: TargetProduct(productId: "pId1", categoryId: "cId1"))
```

**Objective-C**

```text
AEPTargetOrder *order = [[AEPTargetOrder alloc] initWithId:@"id1" total:1.0 purchasedProductIds:@[@"ppId1"]];
AEPTargetProduct *product =[[AEPTargetProduct alloc] initWithProductId:@"pId1" categoryId:@"cId1"];
AEPTargetParameters * targetParams = [[AEPTargetParameters alloc] initWithParameters:@{@"mbox_parameter_key":@"mbox_parameter_value"} profileParameters:@{@"name":@"Smith"} order:order product:product];
```

### TargetOrder

This class contains orderId, total and an array for purchasedProductIds.

```swift
/// Class for specifying Target order parameters
@objc(AEPTargetOrder)
public class TargetOrder: NSObject, Codable {
    @objc public let orderId: String
    @objc public let total: Double
    @objc public let purchasedProductIds: [String]?

    /// Initialize a `TargetOrder` with an order `id`, order `total`  and a list of `purchasedProductIds`
    /// - Parameters:
    ///   - id: `String` order id
    ///   - total: `Double` order total amount
    ///   - purchasedProductIds: a list of purchased product ids
    @objc public init(id: String, total: Double = 0, purchasedProductIds: [String]? = nil) {
        orderId = id
        self.total = total
        self.purchasedProductIds = purchasedProductIds
    }
}
```

The following example can be used to create an instance of a TargetOrder object.

**Swift**

```swift
let targetOrder = TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"])
```

**Objective-C**

```text
AEPTargetOrder *order = [[AEPTargetOrder alloc] initWithId:@"id1" total:1.0 purchasedProductIds:@[@"ppId1"]];
```

### TargetProduct

This class contains productId and categoryId.

```swift
/// Class for specifying Target product parameters
@objc(AEPTargetProduct)
public class TargetProduct: NSObject, Codable {
    @objc public let productId: String
    @objc public let categoryId: String?

    /// Initialize a `TargetProduct` with a product  id and a productCategoryId.
    /// - Parameters:
    ///   - productId: product id
    ///   - categoryId: product category id
    @objc public init(productId: String, categoryId: String? = nil) {
        self.productId = productId
        self.categoryId = categoryId
    }
}
```

The following example can be used to create an instance of a TargetProduct object.

**Swift**

```swift
let targetProduct = TargetProduct(productId: "pId1", categoryId: "cId1")
```

**Objective-C**

```text
AEPTargetProduct *product =[[AEPTargetProduct alloc] initWithProductId:@"pId1" categoryId:@"cId1"];
```
{% endtab %}
{% endtabs %}

