# Target API reference \(deprecated\)

### Using the prefetch APIs

{% hint style="warning" %}
The `prefetchContent` API signature has changed. We recommend that you  use parameters encapsulated in `TargetParameters`.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

#### Using the `TargetPrefetch` builder

The `TargetPrefetch` builder helps create a `TargetPrefetch` instance with the specified data. The returned instance can be used with `prefetchContent`, which accepts a `TargetPrefetch` object list to prefetch offers for the specified mbox locations.

#### Syntax

```java
TargetPrefetch prefetchRequest = new TargetPrefetch.Builder("mboxName")
                .setMboxParameters(new HashMap<String, String>())
                .setOrderParameters(new HashMap<String, Object>())
                .setProductParameters(new HashMap<String, String>())
                .build();
```

#### Using `prefetchContent`

Sends a prefetch request to your configured Target server with the `TargetPrefetch` list and specified `profileParameters`. The callback is invoked when the prefetch is complete, which returns a success status for the prefetch request.

#### Syntax

```java
public static void prefetchContent(final List<TargetPrefetch>                                                                         targetPrefetchList,
                                   final Map<String, Object> profileParameters,
                                   final AdobeCallback<Boolean> callback);
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

Map<String, Object> orderParameters2 = new HashMap<>();
orderParameters2.put("id", "ADCKKIM");
orderParameters2.put("total", "344.30");
orderParameters2.put("purchasedProductIds",  purchasedIds);

Map<String, Object> productParameters2 = new HashMap<>();
productParameters2.put("id", "24D3412");
productParameters2.put("categoryId","Books");

TargetPrefetch prefetchRequest1 = new TargetPrefetch.Builder("mboxName1")
                .setMboxParameters(mboxParameters1)
                .build();


TargetPrefetch prefetchRequest2 = new TargetPrefetch.Builder("mboxName2")
                .setMboxParameters(mboxParameters2)
                .setOrderParameters(orderParameters2)
                .setProductParameters(productParameters2)
                .build();


List<TargetPrefetchObject> prefetchMboxesList = new ArrayList<>();
prefetchMboxesList.add(prefetchRequest1);
prefetchMboxesList.add(prefetchRequest2);


// Call the prefetchContent API.
Target.prefetchContent(prefetchMboxesList, profileParameters, prefetchStatusCallback);
```
{% endtab %}

{% tab title="iOS" %}
### prefetchContent

#### Objective C

Use `prefetchContent` to send a prefetch request to your configured Target server with the `ACPTargetPrefetchObject` array and specified `profileParameters`. The callback will be invoked when the prefetch is complete, which returns a success status for the prefetch request.

#### Syntax

```objectivec
+ (void) prefetchContent: (nonnull NSArray<ACPTargetPrefetchObject*>*) targetPrefetchObjectArray
         withProfileParameters: (nullable NSDictionary<NSString*, NSString*>*) profileParameters
                      callback: (nullable void (^) (BOOL success)) callback;
```

#### Example

```objectivec
NSDictionary *mboxParameters1 = @{@"status":@"platinum"};
NSDictionary *productParameters1 = @{@"id":@"24D3412",
                                        @"categoryId":@"Books"};
NSDictionary *orderParameters1 = @{@"id":@"ADCKKIM",
                                      @"total":@"344.30",
                                      @"purchasedProductIds":@"34, 125, 99"};

NSDictionary *mboxParameters2 = @{@"userType":@"Paid"};
NSDictionary *productParameters2 = @{@"id":@"764334",
                                         @"categoryId":@"Online"};
NSArray *purchaseIDs = @[@"id1",@"id2"];
NSDictionary *orderParameters2 = @{@"id":@"4t4uxksa",
                                       @"total":@"54.90",
                                       @"purchasedProductIds":purchaseIDs};

// Creating Prefetch Objects
ACPTargetPrefetchObject *prefetch1 = [ACPTargetPrefetchObject prefetchObjectWithName:@"logo" mboxParameters:mboxParameters1];
prefetch1.productParameters = productParameters1;
prefetch1.orderParameters = orderParameters1;

ACPTargetPrefetchObject *prefetch2 = [ACPTargetPrefetchObject prefetchObjectWithName:@"buttonColor" mboxParameters:mboxParameters2];
prefetch2.productParameters = productParameters2;
prefetch2.orderParameters = orderParameters2;

// Creating prefetch Array
NSArray *prefetchArray = @[prefetch1,prefetch2];

// Creating Profile parameters
NSDictionary *profileParameters = @{@"age":@"20-32"};

// Target API Call
[ACPTarget prefetchContent:prefetchArray withProfileParameters:profileParameters callback:^(BOOL isSuccess){
       // do something with the Boolean result
}];
```
{% endtab %}
{% endtabs %}

## Load Target requests

Sends a batch request to your configured Target server for multiple mbox locations that are specified.

{% hint style="warning" %}
`loadRequests` API is deprecated and, for batch scenarios, has been replaced with `retrieveLocationContent`.

When working with prefetch APIs, and switching to the new `retrieveLocationContent` API, if you do not use `locationsDisplayed`, reporting will not work.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### TargetRequest Builder

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

### loadRequests

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
### loadRequests

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

NSDictionary *mboxParameters2 = @{@"userType":@"Paid"};
NSDictionary *productParameters2 = @{@"id":@"764334",
                                         @"categoryId":@"Online"};
NSArray *purchaseIDs = @[@"id1",@"id2"];
NSDictionary *orderParameters2 = @{@"id":@"4t4uxksa",
                                       @"total":@"54.90",
                                       @"purchasedProductIds":purchaseIDs};

ACPTargetRequestObject *request1 = [ACPTargetRequestObject requestObjectWithName:@"logo" defaultContent:@"BlueWhale" mboxParameters:mboxParameters1 callback:^(NSString *content){
        // do something with the received content
  }];
request1.productParameters = productParameters1;
request1.orderParameters = orderParameters1;


ACPTargetRequestObject *request2 = [ACPTargetRequestObject requestObjectWithName:@"buttonColor" defaultContent:@"red" mboxParameters:mboxParameters2 callback:^(NSString *content){
        // do something with the received content
}];
request2.productParameters = productParameters1;
request2.orderParameters = orderParameters1;

// create request object array
NSArray *requestArray = @[request1,request2];

// Creating Profile parameters
NSDictionary *profileParameters = @{@"age":@"20-32"};

// Call the API
[ACPTarget loadRequests:requestArray withProfileParameters:profileParameters];
```
{% endtab %}
{% endtabs %}

## Send an mbox click notification

Sends a click notification to the configured Target server for a prefetched or regular mbox location. The click metric should be enabled for the provided location name in Target.

{% hint style="warning" %}
`locationClicked` API signature is changed and the recommended way is to use parameters encapsulated in `TargetParameters`
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### locationClicked

If a notification is sent for a prefetched mbox, its contents should already have been requested with `loadRequests`, which indicates that the mbox was viewed.

#### Syntax

```java
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

Target.locationClicked("cartLocation", mboxParameters, productParameters, orderParameters, profileParameters);
```
{% endtab %}

{% tab title="iOS" %}
### locationClicked

If a notification is sent for a prefetched mbox, its contents should already have been requested with `loadRequests`, which indicates that the mbox was viewed.

#### Syntax

```objectivec
+ (void) locationClickedWithName: (nonnull NSString*) name
                  mboxParameters: (nullable NSDictionary<NSString*, NSString*>*) mboxParameters
               productParameters: (nullable NSDictionary<NSString*, NSString*>*) productParameters
                 orderParameters: (nullable NSDictionary*) orderParameters
               profileParameters: (nullable NSDictionary<NSString*, NSString*>*) profileParameters;
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

[ACPTarget locationClickedWithName:@"cartLocation"
                    mboxParameters:mboxParameters
                 productParameters:productParameters
                   orderParameters:orderParameters
                 profileParameters:profileParameters];
```
{% endtab %}
{% endtabs %}

## Public classes

{% tabs %}
{% tab title="Android" %}
### TargetRequest

{% hint style="warning" %}
Using Builder to construct TargetRequest Object has been deprecated, and constructors are preferred way.
{% endhint %}

Here is a code sample for this class in Android:

```java
public class TargetRequest extends TargetObject {

    /**
    * Builder used to construct a TargetRequest object.
    */
    @Deprecated
    public static class Builder {
        private TargetRequest targetRequest;

        /**
         * Create a TargetRequest Builder.
         *
         * @param mboxName String mbox name for this request
         * @param defaultContent String default content for this request
         */
        @Deprecated
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
         * Set profile parameters for this request.
         *
         * @param profileParameters Map<String, String> profile parameters
         * @return this builder
         */
        public Builder setProfileParameters(final Map<String, Object> profileParameters);

        /**
         * Set Target parameters for this request.
         *
         * @param targetParameters TargetParameters object
         * @return this builder
         */
        public Builder setTargetParameters(final TargetParameters targetParameters);

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

{% hint style="warning" %}
Using Builder to construct TargetPrefetch Object has been deprecated, and constructors are preferred way.
{% endhint %}

Here is a code sample for this class in Android:

```java
public class TargetPrefetch extends TargetObject {

    /**
     * Builder used to construct a TargetPrefetch object
     */
    @Deprecated
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
         * Set profile parameters for this request.
         *
         * @param profileParameters Map<String, String> profile parameters
         * @return this builder
         */
         public Builder setProfileParameters(final Map<String, Object> profileParameters);

        /**
         * Set Target parameters for this request.
         *
         * @param targetParameters TargetParameters object
         * @return this builder
         */
         public Builder setTargetParameters(final TargetParameters targetParameters);

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
@interface ACPTargetRequestObject : ACPTargetPrefetchObject

///< The default content that will be returned if Target servers are unreachable
@property(nonatomic, strong, nonnull) NSString* defaultContent;

///< Optional. When batch requesting Target locations, callback will be invoked when content is available for this location.
@property(nonatomic, strong, nullable) void (^callback)(NSString* __nullable content);
@end
```

The following method can be used to create an instance of a Target prefetch object that might be used to make a batch request to the configured Target server to prefetch content for mbox locations:

```text
+ (nonnull instancetype) requestObjectWithName: (nonnull NSString*) name
                                defaultContent: (nonnull NSString*) defaultContent
                                mboxParameters: (nullable NSDictionary<NSString*, NSString*>*) mboxParameters
                                      callback: (nullable void (^) (NSString* __nullable content)) callback;
```

### ACPTargetPrefetchObject

This class contains the name of the Target location/mbox and parameter dictionary for mbox parameters, product parameters, and order parameters that will be used in a prefetch:

```objectivec
@interface ACPTargetPrefetchObject : NSObject

///< The name of the Target location/mbox
@property(nonatomic, strong, nullable) NSString* name;

///< Dictionary containing key-value pairs of mbox parameters
@property(nonatomic, strong, nullable) NSDictionary<NSString*, NSString*>* mboxParameters;

///< Dictionary containing key-value pairs of product parameters
@property(nonatomic, strong, nullable) NSDictionary<NSString*, NSString*>* productParameters;

///< Dictionary containing key-value pairs of order parameters
@property(nonatomic, strong, nullable) NSDictionary* orderParameters;
@end
```

The following method can be used to create an instance of a Target prefetch object that might be used to make a batch request to the configured Target server to prefetch content for mbox locations:

```text
+ (nonnull instancetype) prefetchObjectWithName: (nonnull NSString*) name
                                 mboxParameters: (nullable NSDictionary*) mboxParameters;
```
{% endtab %}
{% endtabs %}

