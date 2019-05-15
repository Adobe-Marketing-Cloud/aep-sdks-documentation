# Adobe Target

[Adobe Target](https://www.adobe.com/marketing/target/mobile-optimization.html) helps test, personalize, and optimize mobile app experiences based on user behavior and mobile context. You can deliver interactions that engage and convert through iterative testing and rules-based and AI-powered personalization.

To get started with Target, follow these steps:

1. Configure the Target extension in Launch.
2. Add the Target Extension to your app.
3. Implement Target APIs to:
   * Request activities.
   * Prefetch offers.
   * Enter visual preview mode.

## Configure the Target extension in Launch   <a id="configuring-the-adobe-target-extension-in-adobe-launch"></a>

![Adobe Target Extension Configuration](../../.gitbook/assets/screen-shot-2018-10-05-at-1.47.51-pm.png)

1. In Launch, click the **Extensions** tab.
2. On the **Installed** tab, locate the Adobe Target extension, and click **Configure**.
3. Type your **Target** client code.
4. Optionally, provide your Environment ID.
5. Set the timeout value to at least 5 seconds.
6. Click **Save**.
7. Follow the publishing process to update SDK configuration

To find your Target client code, go to the **Set up** tab and select **Implementation** in the left pane. To see the client code in the dialog box that is displayed under **Implementation Method**, click **Edit at.js Settings**.

## Add Target to your app

#### Java

1. Add the Target extension to your project using the app's Gradle file.
2. Import the Target extension in your application's main activity.  `import com.adobe.marketing.mobile.*;`
3. Add the Target library to your project via your `Podfile` by adding `pod 'ACPTarget'`

#### Objective-C

Import the Target and Identity library.

```objectivec
   #import "ACPCore.h"
   #import "ACPTarget.h"
   #import "ACPIdentity.h"
   #import "ACPTargetRequestObject.h"
   #import "ACPTargetPrefetchObject.h"
```

#### Swift

```swift
   #import ACPCore
   #import ACPTarget
   #import ACPIdentity
```

### Register Target with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### Java

After calling the `setApplication()` method in the `onCreate()` method, register Target with Mobile Core.

Here is code sample that calls these set up methods:

```java
public class TargetApp extends Application {

 @Override
 public void onCreate() {
     super.onCreate();
     MobileCore.setApplication(this);

     try {
         Target.registerExtension();
         Identity.registerExtension();
     } catch (Exception e) {
         //Log the exception
     }
 }
}
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

1. In your app's `didFinishLaunchingWithOptions` function register the Target extension

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  [ACPTarget registerExtension];

  // Override point for customization after application launch.
  return YES;
}
```

#### Swift
{% endtab %}
{% endtabs %}

## Prefetch offers   <a id="integrating-adobe-target-with-analytics-a-4-t"></a>

The SDK can minimize the number of times it reaches out to Target servers to fetch offers by caching server responses. When this feature is enabled, offer content is retrieved and cached during the prefetch call. This content is retrieved from the cache for all future calls that contain cached content for the specified mbox name. This prefetch process reduces offer load time, network calls made to Target servers, and allows Target to be notified which mbox was visited by the mobile app user.

{% hint style="warning" %}
Prefetched offer content does not persist across launches. The prefetch content is cached as long as the application lives or until the API that is used to clear the cache is called. For more information, see [Clear prefetch offer cache](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target#clear-prefetch-offer-cache).
{% endhint %}

### Using the prefetch APIs

{% tabs %}
{% tab title="Android" %}
#### Java


#### Using the `TargetPrefetch` Constructor

Using `TargetPrefetch` Constructor, you can create a `TargetPrefetch` instance with the specified data. It currently accepts location name and an optional `TargetParameters` object. The returned instance can be used with `prefetchContent`, which accepts a `TargetPrefetch` object list to prefetch offers for the specified mbox locations. 


#### Syntax

```java
TargetParameters parameters = new TargetParameters.Builder()
                              .product(TargetProduct.fromMap(productParameters))
                              .order(TargetOrder.fromMap(orderParameters))
                              .parameters(mboxParameters)
                              .profileParameters(profileParameters).build();

TargetPrefetch prefetchRequest = new TargetPrefetch("mboxName", parameters);
```

#### Using `prefetchContent`

Sends a prefetch request to your configured Target server with the `TargetPrefetch` list and specified `TargetParameters`. The callback is invoked when the prefetch is complete, which returns a null if prefetch completed successfully or error message for the prefetch request.

#### Syntax

```java
public static void prefetchContent(final List<TargetPrefetch>                                                                         targetPrefetchList,
                                   final TargetParameters parameters,
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

TargetParameters parameters1 = new TargetParameters.Builder()
                              .parameters(mboxParameters1)
                              .build();
TargetPrefetch prefetchRequest1 = new TargetPrefetch("mboxName1", parameters1);

TargetParameters parameters2 = new TargetParameters.Builder()
                              .parameters(mboxParameters2)
                              .product(targetProduct)
                              .order(targetOrder)
                              .build();
TargetPrefetch prefetchRequest2 = new TargetPrefetch("mboxName2", parameters2);


List<TargetPrefetchObject> prefetchMboxesList = new ArrayList<>();
prefetchMboxesList.add(prefetchRequest1);
prefetchMboxesList.add(prefetchRequest2);


// Call the prefetchContent API.
TargetParamters parameters = null;
Target.prefetchContent(prefetchMboxesList, parameters, prefetchStatusCallback);
```

#### Using the `TargetPrefetch` Builder(Marked as deprecated)

The `TargetPrefetch` builder helps create a `TargetPrefetch` instance with the specified data. The returned instance can be used with `prefetchContent`, which accepts a `TargetPrefetch` object list to prefetch offers for the specified mbox locations.

#### Syntax

```java
TargetPrefetch prefetchRequest = new TargetPrefetch.Builder("mboxName")
                .setMboxParameters(new HashMap<String, String>())
                .setOrderParameters(new HashMap<String, Object>())
                .setProductParameters(new HashMap<String, String>())
                .build();
```

#### Using `prefetchContent` (Marked as deprecated)

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
#### Objective C

Use `prefetchContent` to send a prefetch request to your configured Target server with the `ACPTargetPrefetchObject` array and specified `ACPTargetParameters`. The callback will be invoked when the prefetch is complete, which returns null if prefetch completed sucessfully or error message for the prefetch request.

#### Syntax

```objectivec
+ (void) prefetchContent: (nonnull NSArray<ACPTargetPrefetchObject*>*) targetPrefetchObjectArray
          withParameters: (nullable ACPTargetParameters*) parameters
                callback: (nullable void (^) (NSError* _Nullable error)) callback;
```

#### Objective-C Example

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
NSArray *purchaseIDs = @[@"id1",@"id2"];
ACPTargetOrder *order2 = [ACPTargetOrder targetOrderWithId:@"ADCKKIM" total:@(344.30) purchasedProductIds:purchaseIDs];
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
{% endtabs %}

### Using TargetParameters, TargetOrder and TargetProduct object

Using `TargetParameters`, you can encapsulate various parameters (namely mbox-Parameters, profile-parameters, order-parameters and product-parameters) for easy use
With `TargetOrder`, you can encapsulate the order parameters and use it in TargetParameters.
With `TargetProduct`, you can encapsulate the product parameters and use it in TargetParameters.

**Merging behavior of parameters passed in API's  with parameters passed in TargetPrefetch/TargetRequest Object**

There can be cases, when some global parameters are passed in API's. If target-parameters are also passed in corresponding prefetch/request objects, then those parameters will be merged along with global parameters. 

Corresponding TargetOrder and TargetProduct parameters will be overridden by API level global parameters.
Mbox-parameters and profile-parameters will be appended only if the key names differ. Otherwise if key name matches then they will be overridden.

{% tabs %}
{% tab title="Android" %}
#### **Syntax**

```java
public TargetOrder(final String id, final double total, final List<String> purchasedProductIds)

public TargetProduct(final String id, final String categoryId)

TargetParameters targetParameters = new TargetParameters.Builder()
                                    .parameters(new HashMap<String, String>())
                                    .profileParameters(new HashMap<String, String>())
                                    .product(targetProduct)
                                    .order(targetOrder)
                                    .build();
```

#### **Example**

```java
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("34");
purchasedProductIds.add("125"); 
TargetOrder targetOrder = new TargetOrder("123", 567.89, purchasedProductIds);

TargetProduct targetProduct = new TargetProduct("123", "Books");

Map<String, Object> mboxParameters1 = new HashMap<>();
mboxParameters1.put("status", "platinum");

Map<String, Object> profileParameters1 = new HashMap<>();
profileParameters1.put("gender", "male");

TargetParameters targetParameters = new TargetParameters.Builder()
                                    .parameters(mboxParameters1)
                                    .profileParameters(profileParameters1)
                                    .product(targetProduct)
                                    .order(targetOrder)
                                    .build();
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (nonnull instancetype) targetOrderWithId: (nonnull NSString*) orderId
                                     total: (nullable NSNumber*) total
                       purchasedProductIds: (nullable NSArray <NSString*>*) purchasedProductIds;

+ (nonnull instancetype) targetProductWithId: (nonnull NSString*) productId
                                  categoryId: (nullable NSString*) categoryId;

+ (nonnull instancetype) targetParametersWithParameters: (nullable NSDictionary*) parameters
                                      profileParameters: (nullable NSDictionary*) profileParameters
                                                product: (nullable ACPTargetProduct*) product
                                                  order: (nullable ACPTargetOrder*) order;
```

#### Objective-C Example

```objectivec
NSDictionary *mboxParameters = @{@"status":@"Platinum"};
NSDictionary *profileParameters = @{@"gender":@"female"};
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];
ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];
ACPTargetParameters *targetParameters = [ACPTargetParameters targetParametersWithParameters:mboxParameters
                                                    profileParameters:profileParameters
                                                              product:product
                                                                order:order];
```
{% endtab %}
{% endtabs %}

### Using Locations Displayed API for Prefetch

In some situations, you may want to want to inform Target that the corresponding location (mbox) has been viewed. This API sends a display notification to Target for a given prefetched mbox. This helps Target record location display events.

Note: If you're only using regular mboxes, and not prefetching any mbox content, this method should not be called.

{% tabs %}
{% tab title="Android" %}
#### **Syntax**

```java
public static void locationsDisplayed(final List<String> mboxNames, final TargetParameters parameters)
```

#### **Example**

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
Target.locationsDisplayed(null, targetParameters);
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (void) locationsDisplayed: (nonnull NSArray<NSString*>*) mboxNames withTargetParameters: (nullable ACPTargetParameters*) parameters;
```

#### Objective-C Example

```objectivec
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];
ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];
ACPTargetParameters *targetParameters = [ACPTargetParameters targetParametersWithParameters:nil
                                                    profileParameters:nil
                                                              product:product
                                                                order:order];
[ACPTarget locationsDisplayed:@[@"mboxName1", @"mboxName2"] withTargetParameters:targetParameters];
```
{% endtab %}
{% endtabs %}

### Clear prefetch offer cache

To clear prefetched, cached offer data, use the following:

{% tabs %}
{% tab title="Android" %}
#### **Syntax**

```java
public static void clearPrefetchCache()
```

#### **Example**

```java
Target.clearPrefetchCache();
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (void) clearPrefetchCache;
```

#### Objective-C Example

```objectivec
[ACPTarget clearPrefetchCache];
```
{% endtab %}
{% endtabs %}

## Visual preview   <a id="integrating-adobe-target-with-analytics-a-4-t"></a>

Visual preview mode allows you to easily perform end-to-end QA for Target activities by enrolling and previewing these activities on your device. This mode does not require a specialized testing set up. To get started, set up a URL scheme and generate the preview links. For more information, see [Target mobile preview](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/target-mobile-preview.html).

You can also set an app deep link that can be triggered when selections are made in the preview mode by using the following methods:

{% tabs %}
{% tab title="Android" %}
#### **Syntax**

```java
public static void setPreviewRestartDeepLink(final Uri deepLink);
```

#### **Example**

```java
Target.setPreviewRestartDeepLink("myApp://HomePage");
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

`+ (void) setPreviewRestartDeepLink: (nonnull NSURL*) deepLink;`

#### **Objective-C Example**

`[ACPTarget setPreviewRestartDeepLink:@"myApp://HomePage"];`

#### **Swift Example**

`ACPTarget.setPreviewRestartDeepLink("myApp://HomePage")`
{% endtab %}
{% endtabs %}

## Target with Analytics \(A4T\)   <a id="integrating-adobe-target-with-analytics-a-4-t"></a>

To see the performance of your Target activities for certain segments, set up the Analytics for Target \(A4T\) cross-solution integration by enabling the A4T campaigns. This integration allows you use Analytics reports to examine your results. If you use Analytics as the reporting source for an activity, all reporting and segmentation for that activity is based on Analytics data collection. For more information, see [Adobe Analytics for Adobe Target \(A4T\)](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html).

## Configuration keys

If you need to update SDK configuration, programmatically, please use the following information to change your Target configuration values. For more information, [Configuration API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| Key                  | Description                              |
| :------------------- | :--------------------------------------- |
| target.clientcode    | Client code for your account.            |
| target.timeout       | Time, in seconds, to wait for a response from Target servers before timing out. |
| target.environmentId | Environment ID you want to use, if this is left blank, the default production environment will be used. |

## Additional information

* Want to get your Target client code? See the **Client** row in [Configure mbox.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html).
* What is an mbox? See [How Target works in mobile apps](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html).
* What is Analytics for Target \(A4T\)? See [Adobe Analytics as the reporting source for Adobe Target \(A4T\)](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html).

