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
                // read target's thirdPartyID
    }
});
```
{% endtab %}

{% tab title="iOS" %}
### getThirdPartyId

Gets the custom visitor ID for Target. The callback will be invoked to return the `thirdPartyId` value, or if no third-party ID is set, `nil` is returned.

### Syntax  <a id="syntax"></a>

```objectivec
+ (void) getThirdPartyId: (nonnull void (^) (NSString* __nullable thirdPartyId)) callback;
```

### Examples  <a id="examples"></a>

Here are the examples in Objective C and Swift:

#### **Objective C**  <a id="objective-c"></a>

```objectivec
[ACPTarget getThirdPartyId:^(NSString *thirdPartyId){
       // read thirdPartyId
}];
```

#### **Swift**  <a id="swift"></a>

```swift
ACPTarget.getThirdPartyId({thirdPartyID in
       // read thirdPartyId
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

Sets the custom visitor ID for Target. This ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when `resetExperience` API is called.

### Syntax  <a id="syntax-1"></a>

```objectivec
+ (void) setThirdPartyId: (nullable NSString*) thirdPartyId;
```

### Examples  <a id="examples-1"></a>

Here are some examples in Objective-C and Swift:

#### **Objective-C**  <a id="objective-c-1"></a>

```objectivec
[ACPTarget setThirdPartyId:@"third-party-id"];
```

**Swift**

```swift
ACPTarget.setThirdPartyId("third-party-id")
```
{% endtab %}
{% endtabs %}

## Reset user experience

Use this API to reset the user's experience by removing the visitor identifiers. This method also removes previously set third-party and Target IDs from persistent storage.

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

### Syntax  <a id="syntax-2"></a>

```objectivec
+ (void) resetExperience;
```

### Examples  <a id="examples-2"></a>

Here are some examples in Objective-C and Swift:

#### **Objective-C**  <a id="objective-c-2"></a>

```objectivec
[ACPTarget resetExperience];
```

#### **Swift**  <a id="swift-1"></a>

```swift
ACPTarget.resetExperience()
```
{% endtab %}
{% endtabs %}

## Get Target user identifier

Gets the Target user identifier.

{% tabs %}
{% tab title="Android" %}
### getTntId

The callback is invoked to return the `tntId` value 0 if no Target ID is set, and `null` is returned.

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

Gets the Target user identifier. The callback will be invoked to return the `tntId` value, or if no Target ID is set, `nil` is returned.

Target returns `tntId` upon a successful call to `loadRequests` or `prefetchContent`. Once set in SDK, this ID is preserved between app upgrades, is saved and restored during the standard application backup process, and is removed at uninstall or when `rResetExperience` API is called.

#### Syntax

```objectivec
+ (void) getTntId: (nonnull void (^) (NSString* __nullable tntId)) callback;
```

#### **Examples**

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

## Load Target requests

Sends a batch request to your configured Target server for multiple mbox locations that are specified.

{% hint style="warning" %}
`loadRequests` API is deprecated, and replaced with `retrieveLocationContent` for batch scenarios instead.

Note: When working with prefetch API's, and switching to new `retrieveLocationContent` API, please also use `locationsDisplayed`, otherwise reporting will not work.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### TargetRequest Constructor

`TargetRequest` Constructor helps create a `TargetRequest` instance. It replaces the deprecated builder pattern. The returned instance can be used with `loadRequests`, which accepts a `TargetRequest` object list to retrieve offers for the specified mbox locations.

#### Syntax

```java
TargetParameters parameters = new TargetParameters.Builder()
                                    .parameters(new HashMap<String, String>())
                                    .profileParameters(new HashMap<String, String>())
                                    .order(new TargetOrder())
                                    .product(new TargetProduct())
                                    .build();
TargetRequest targetRequest = new TargetRequest("mboxName", parameters, "defaultContent", 
                                                new AdobeCallback<String>() {
                                                    @Override
                                                    public void call(String value) {
                                                        // do something with target content.
                                                    }
                                                });
```

### TargetRequest Builder (Marked as deprecated)

`TargetRequest` builder helps create a `TargetRequest` instance. The returned instance can be used with `loadRequests`, which accepts a `TargetRequest` object list to retrieve offers for the specified mbox locations.

#### Syntax

```java
TargetRequest request = new TargetRequest.Builder("mboxName","defaultContent")
                .setMboxParameters(new HashMap<String, String>())
                .setOrderParameters(new HashMap<String, Object>())
                .setProductParameters(new HashMap<String, String>())
                .setContentCallback(new AdobeCallback<String>() {
                    @Override
                    public void call(String value) {
                        // do something with target content.
                    }
                }).build();
```

### loadRequests (Marked as deprecated)

Sends a batch request to your configured Target server for multiple mbox locations that are specified in the `TargetRequest` list. Each object in the array contains a callback function, which is invoked when content is available for its given mbox location.

#### Syntax

```java
public static void loadRequests(final List<TargetRequest> requestArray,
                                    final Map<String, Object> profileParameters);
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

Map<String, Object> orderParameters2 = new HashMap<>();
orderParameters2.put("id", "ADCKKIM");
orderParameters2.put("total", "344.30");
orderParameters2.put("purchasedProductIds",  purchasedIds);

Map<String, Object> productParameters2 = new HashMap<>();
productParameters2.put("id", "24D3412");
productParameters2.put("categoryId","Books");

TargetRequest request1 = new TargetRequest.Builder("mboxName1", "defaultContent1")
                .setMboxParameters(mboxParameters1)
                .setContentCallback(new AdobeCallback<String>() {
                    @Override
                    public void call(String value) {
                        // do something with target content.
                    }
                }).build();

TargetRequest request2 = new TargetRequest.Builder("mboxName2", "defaultContent2")
                .setMboxParameters(mboxParameters2)
                .setOrderParameters(orderParameters2)
                .setProductParameters(productParameters2)
                .setContentCallback(new AdobeCallback<String>() {
                    @Override
                    public void call(String value) {
                        // do something with target content.
                    }
                }).build();

// Creating Array of Request Objects
List<TargetRequest> locationRequests = new ArrayList<>();
locationRequests.add(request1);
locationRequests.add(request2);

 // Define the profile parameters map.
Map<String, Object> profileParameters = new HashMap<>();
profileParameters.put("ageGroup", "20-32");

// Call the targetLoadRequests API.
Target.loadRequests(locationRequests, profileParameters);
```
{% endtab %}

{% tab title="iOS" %}
### loadRequests(Marked as deprecated)

Sends a batch request to your configured Target server for multiple mbox locations that are specified in the`ACPTargetRequestObject` array. Each object in the array contains a callback function, which will be invoked when content is available for its given mbox location.

#### Syntax

```objectivec
+ (void) loadRequests: (nonnull NSArray<ACPTargetRequestObject*>*) requests
      withProfileParameters: (nullable NSDictionary<NSString*, NSString*>*) profileParameters;
```

#### Example

```objectivec
NSDictionary *mboxParameters1 = @{@"status":@"platinum"};
NSDictionary *productParameters1 = @{@"id":@"24D3412",
                                        @"categoryId":@"Books"};
NSDictionary *orderParameters1 = @{@"id":@"ADCKKIM",
                                      @"total":@"344.30",
                                      @"purchasedProductIds":@"34, 125, 99"};
​
NSDictionary *mboxParameters2 = @{@"userType":@"Paid"};
NSDictionary *productParameters2 = @{@"id":@"764334",
                                         @"categoryId":@"Online"};
NSArray *purchaseIDs = @[@"id1",@"id2"];
NSDictionary *orderParameters2 = @{@"id":@"4t4uxksa",
                                       @"total":@"54.90",
                                       @"purchasedProductIds":purchaseIDs};
​
ACPTargetRequestObject *request1 = [ACPTargetRequestObject requestObjectWithName:@"logo" defaultContent:@"BlueWhale" mboxParameters:mboxParameters1 callback:^(NSString *content){
        // do something with the received content
  }];
request1.productParameters = productParameters1;
request1.orderParameters = orderParameters1;
​
​
ACPTargetRequestObject *request2 = [ACPTargetRequestObject requestObjectWithName:@"buttonColor" defaultContent:@"red" mboxParameters:mboxParameters2 callback:^(NSString *content){
        // do something with the received content
}];
request2.productParameters = productParameters1;
request2.orderParameters = orderParameters1;
​
// create request object array
NSArray *requestArray = @[request1,request2];
​
// Creating Profile parameters
NSDictionary *profileParameters = @{@"age":@"20-32"};
​
// Call the API
[ACPTarget loadRequests:requestArray withProfileParameters:profileParameters];
```
{% endtab %}
{% endtabs %}

## Retrieve Location Content requests

Executes a batch request to the configured Target server for multiple mbox locations. 
The main difference with `loadRequest` API is in usage along with prefetch APIs.
This API only returns the content and does not increase the reporting count. 
If you are using normal batch requests, then there is no difference with `loadRequest` API.

{% tabs %}
{% tab title="Android" %}
### retrieveLocationContent

Sends a batch request to your configured Target server for multiple mbox locations that are specified in the `TargetRequest` list. Any prefetched content which matches a given mbox location is returned and not included in the batch request to the Target server. Each object in the list contains a callback function, which will be invoked when content is available for its given mbox location.

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
TargetRequest request1 = new TargetRequest("mboxName1", parameters2, "defaultContent1",
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

Sends a batch request to your configured Target server for multiple mbox locations that are specified in the`ACPTargetRequestObject` array. Each object in the array contains a callback function, which will be invoked when content is available for its given mbox location.

#### Syntax

```objectivec
+ (void) retrieveLocationContent: (nonnull NSArray<ACPTargetRequestObject*>*) requests
                  withParameters: (nullable ACPTargetParameters*) parameters;
```

#### Example

```objectivec
NSDictionary *mboxParameters1 = @{@"status":@"platinum"};
ACPTargetProduct *product1 = [ACPTargetProduct targetProductWithId:@"24D3412" categoryId:@"Books"];
ACPTargetOrder *order1 = [ACPTargetOrder targetOrderWithId:@"ADCKKIM" total:@(344.30) purchasedProductIds:@[@"a", @"b"]];

NSDictionary *mboxParameters2 = @{@"userType":@"Paid"};
ACPTargetProduct *product2 = [ACPTargetProduct targetProductWithId:@"764334" categoryId:@"Online"];
NSArray *purchaseIDs = @[@"id1",@"id2"];
ACPTargetOrder *order2 = [ACPTargetOrder targetOrderWithId:@"4t4uxksa" total:@(54.90) purchasedProductIds:purchaseIDs];

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
// create request object array
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
[ACPTarget retrieveLocationContent:requestArray withParameters:targetParameters]
```
{% endtab %}
{% endtabs %}

## Set preview restart deep link

This API sets the Target preview URL to be displayed when the preview mode is restarted.

{% tabs %}
{% tab title="Android" %}
### setPreviewRestartDeeplink

#### Syntax

```text
public static void setPreviewRestartDeepLink(final Uri deepLink)
```
{% endtab %}

{% tab title="iOS" %}
### setPreviewRestartDeeplink

#### Syntax

```objectivec
+ (void) setPreviewRestartDeeplink: (nonnull NSURL*) deeplink;
```
{% endtab %}
{% endtabs %}

## Send an mbox click notification

Sends a click notification to the configured Target server for a prefetched or regular mbox location. The click metric should be enabled for the provided location name in Target.

{% tabs %}
{% tab title="Android" %}
### locationClicked

If a notification is sent for a prefetched mbox, its contents should already have been requested with `loadRequests`, which indicates that the mbox was viewed.

#### Syntax

```java
public static void locationClicked(final String mboxName, final TargetParameters parameters)

@Deprecated
public static void locationClicked(final String mboxName,
                                    final Map<String, String> mboxParameters
                                    final Map<String, String> productParameters
                                    final Map<String, Object> orderParameters
                                    final Map<String, String> profileParameters);
```

#### Example

```java
// Define Mbox parameters
Map<String, Object> mboxParameters = new HashMap<>();
mboxParameters.put("membership", "prime");

// Define Product parameters
Map<String, Object> productParameters = new HashMap<>();
productParameters.put("id", "CEDFJC");
productParameters.put("categoryId","Electronics");

List<String> purchasedIds = new ArrayList<String>();
purchasedIds.add("81");
purchasedIds.add("123"); 
purchasedIds.add("190");

// Define Order parameters
Map<String, Object> orderParameters = new HashMap<>();
orderParameters.put("id", "NJJICK");
orderParameters.put("total", "650");
orderParameters.put("purchasedProductIds",  purchasedIds);

// Creating Profile parameters
Map<String, Object> profileParameters = new HashMap<>();
profileParameters.put("ageGroup", "20-32");

//Deprecated API call
Target.locationClicked("cartLocation", mboxParameters, productParameters, orderParameters, profileParameters);

//Target Parameters
TargetOrder targetOrder = new TargetOrder("NJJICK", "650", purchasedIds);
TargetProduct targetProduct = new TargetProduct("CEDFJC", "Electronics");
TargetParameters targetParameters = new TargetParameters.Builder(mboxParameters)
								.profileParameters(profileParameters)
								.order(targetOrder)
								.product(targetProduct)
								.build();
//New API call
Target.locationClicked("cartLocation", targetParameters);

```
{% endtab %}

{% tab title="iOS" %}
### locationClicked

If a notification is sent for a prefetched mbox, its contents should already have been requested with `loadRequests`, which indicates that the mbox was viewed.

#### Syntax

```objectivec
+ (void) locationClickedWithName: (nonnull NSString*) name targetParameters: (nullable ACPTargetParameters*) parameters;

@Deprecated
+ (void) locationClickedWithName: (nonnull NSString*) name mboxParameters: (nullable NSDictionary<NSString*, NSString*>*) mboxParameters productParameters: (nullable NSDictionary<NSString*, NSString*>*) productParameters orderParameters: (nullable NSDictionary*) orderParameters profileParameters: (nullable NSDictionary<NSString*, NSString*>*) profileParameters;
```

#### Example

```objectivec
// Define Mbox parameters
NSDictionary *mboxParameters = @{@"membership":@"prime"};

// Define Product parameters
NSDictionary *productParameters = @{@"id":@"CEDFJC",
                                    @"categoryId":@"Electronics"};
// Define Order parameters
NSDictionary *orderParameters = @{@"id":@"NJJICK",
                                    @"total":@"650",
                                    @"purchasedProductIds":@"81, 123, 190"};

// Define Profile parameters
NSDictionary *profileParameters = @{@"ageGroup":@"20-32"};

 
// Deprecated API Call
[ACPTarget locationClickedWithName:@"cartLocation" mboxParameters:mboxParameters productParameters:productParameters orderParameters:orderParameters profileParameters:profileParameters];

// Create Target parameters
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];
ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];
ACPTargetParameters *targetParameters = [ACPTargetParameters targetParametersWithParameters:nil
                                                    profileParameters:nil
                                                              product:product
                                                                order:order];

//New API call
[ACPTarget locationClickedWithName:@"cartLocation" targetParameters:targetParameters]

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

    private TargetRequest() {}

    /**
    * Builder used to construct a TargetRequest object.
    */
    public static class Builder {
        private TargetRequest targetRequest;

        /**
         * Create a TargetRequest Builder.
         *
         * @param mboxName String mbox name for this request
         * @param defaultContent String default content for this request
         */
        public Builder(final String mboxName, final String defaultContent);

        /**
         * Set mbox parameters for this request.
         *
         * @param mboxParameters Map<String, String> mbox parameters
         * @return this builder
         */
        public Builder setMboxParameters(final Map<String, String> mboxParameters);

        /**
        * Set order parameters for this request.
        *
        * @param orderParameters Map<String, Object> order parameters
        * @return this builder
        */
        public Builder setOrderParameters(final Map<String, Object> orderParameters);

        /**
         * Set profile parameters for this request.
         *
         * @param productParameters Map<String, String> product parameters
         * @return this builder
         */
        public Builder setProductParameters(final Map<String, String> productParameters);

        /**
        * Set the callback function for this request.
        *
        * @param contentCallback AdobeCallback<String> which will get called with the returning content
        * @return this builder
        */
        public Builder setContentCallback(final AdobeCallback<String> contentCallback);

        /**
         * Build the TargetRequest.
         *
         * @return TargetRequest the target request object
         */
        public TargetRequest build();
    }
}
```

### TargetPrefetch

Here is a code sample for this class in Android:

```java
public class TargetPrefetch extends TargetObject {
    private TargetPrefetch() {}

    /**
     * Builder used to construct a TargetPrefetch object
     */
    public static class Builder {
        private TargetPrefetch targetPrefetch;

        /**
         * Create a TargetPrefetch Builder.
         *
         * @param mboxName String mbox name for this request
         */
         public Builder(final String mboxName);

        /**
         * Set mbox parameters for this request.
         *
         * @param mboxParameters Map<String, String> mbox parameters
         * @return this builder
         */
         public Builder setMboxParameters(final Map<String, String> mboxParameters);

        /**
         * Set order parameters for this request.
         *
         * @param orderParameters Map<String, String> order parameters
         * @return this builder
         */
         public Builder setOrderParameters(final Map<String, Object> orderParameters);

        /**
         * Set product parameters for this request.
         *
         * @param productParameters Map<String, String> product parameters
         * @return this builder
         */
         public Builder setProductParameters(final Map<String, String> productParameters);

        /**
         * Build and return TargetPrefetch
         *
         * @return TargetPrefetch the target prefetch object
         */
         public TargetPrefetch build();
    }

}
```
{% endtab %}

{% tab title="iOS" %}
### ACPTargetRequestObject

This class extends `ACPTargetPrefetchObject` by adding default content and a function pointer property that will be used as a callback when requesting content from Target:

```objectivec
@interface ACPTargetRequestObject : ACPTargetPrefetchObject​

///< The default content that will be returned if Target servers are unreachable    
@property(nonatomic, strong, nonnull) NSString* defaultContent;​

///< Optional. When batch requesting Target locations, callback will be invoked when content is available for this location.
@property(nonatomic, strong, nullable) void (^callback)(NSString* __nullable content);
@end
```

The following method can be used to create an instance of a Target prefetch object that might be used to make a batch request to the configured Target server to prefetch content for mbox locations:

```objectivec
+ (nonnull instancetype) requestObjectWithName: (nonnull NSString*) name
                                defaultContent: (nonnull NSString*) defaultContent
                                mboxParameters: (nullable NSDictionary<NSString*, NSString*>*) mboxParameters
                                                                      callback: (nullable void (^) (NSString* __nullable content)) callback;
```

### ACPTargetPrefetchObject

This class contains the name of the Target location/mbox and parameter dictionary for mbox parameters, product parameters, and order parameters that will be used in a prefetch:

```objectivec
@interface ACPTargetPrefetchObject : NSObject​

///< The name of the Target location/mbox
@property(nonatomic, strong, nullable) NSString* name;​

///< Dictionary containing key-value pairs of mbox parameters
@property(nonatomic, strong, nullable) NSDictionary<NSString*, NSString*>* mboxParameters;​

///< Dictionary containing key-value pairs of product parameters
@property(nonatomic, strong, nullable) NSDictionary<NSString*, NSString*>* productParameters;

​///< Dictionary containing key-value pairs of order parameters
@property(nonatomic, strong, nullable) NSDictionary* orderParameters;
@end
```

The following method can be used to create an instance of a Target prefetch object that might be used to make a batch request to the configured Target server to prefetch content for mbox locations:

```text
+ (nonnull instancetype) prefetchObjectWithName: (nonnull NSString*) name                                 mboxParameters: (nullable NSDictionary*) mboxParameters;
```

The following method can be used to create an instance of a Target prefetch object that might be used to make a batch request to the configured Target server to prefetch content for mbox locations:

```text
+ (nonnull instancetype) prefetchObjectWithName: (nonnull NSString*) name
                                 mboxParameters: (nullable NSDictionary*) mboxParamete
```
{% endtab %}
{% endtabs %}

