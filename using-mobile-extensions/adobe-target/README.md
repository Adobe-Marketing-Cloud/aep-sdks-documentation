# Adobe Target

[Adobe Target](https://www.adobe.com/marketing/target/mobile-optimization.html) helps test, personalize, and optimize mobile app experiences based on user behavior and mobile context. You can deliver interactions that engage and convert through iterative testing and rules-based and AI-powered personalization.

To get started with Target, follow these steps:

1. Configure the Target extension in Experience Platform Launch.
2. Add the Target Extension to your app.
3. Implement Target APIs to:
   * Request mbox offers.
   * Prefetch mbox offers.
   * Track mboxes.
   * Enter visual preview mode.

## Configure the Target extension in Experience Platform Launch

![Adobe Target Extension Configuration](../../.gitbook/assets/adobe-target-launch-options.png)

1. In Experience Platform Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the Adobe Target extension, and click **Install**.
3. Your **Target** client code will be detected automatically.
4. Optionally, provide your Environment ID.
5. Set the timeout value to at least 5 seconds.
6. Optionally, enter the Target workspace property token that was generated from Target UI.
7. Click **Save**.
8. Follow the publishing process to update SDK configuration.

## Add Target to your app

{% tabs %}
{% tab title="Android" %}

#### Java

1. Add the Target extension to your project using the app's Gradle file.
2. Import the Target extension in your application's main activity.  
```java
import com.adobe.marketing.mobile.*;
```
{% endtab %}

{% tab title="iOS" %}

1. Add the Target library to your project via your `Podfile` by adding `pod 'ACPTarget'`
2. Import the Target and Identity libraries.

#### Objective-C

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
{% endtab %}
{% endtabs %}

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
     MobileCore.ConfigureWithAppId("yourAppId");

     try {
         Target.registerExtension();
         Identity.registerExtension();
         MobileCore.start(null);
     } catch (Exception e) {
         //Log the exception
     }
 }
}
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

1. In your app's `didFinishLaunchingWithOptions` function register the Target extension with Mobile Core:

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPCore configureWithAppId:@"yourAppId"];
  [ACPIdentity registerExtension];
  [ACPTarget registerExtension];
  [ACPCore start:nil];
  // Override point for customization after application launch.
  return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPCore.configure(withAppId: "yourAppId")   
  ACPTarget.registerExtension()
  ACPIdentity.registerExtension()
  ACPCore.start(nil)
  // Override point for customization after application launch. 
  return true;
}
```

{% endtab %}
{% endtabs %}

## Parameters in a Target request

### Target Order

`TargetOrder` encapsulate order ID, order total and purchased product IDs. You can instantiate `TargetOrder` class to create order parameters. For more information on Target Order parameters, see [here](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/orderconfirm-create.html)

{% tabs %}
{% tab title="Android" %}
#### Syntax

```java
public TargetOrder(final String id, final double total, final List<String> purchasedProductIds)
```

#### Example

```java
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("34");
purchasedProductIds.add("125"); 
TargetOrder targetOrder = new TargetOrder("123", 567.89, purchasedProductIds);
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (nonnull instancetype) targetOrderWithId: (nonnull NSString*) orderId
total: (nullable NSNumber*) total
purchasedProductIds: (nullable NSArray <NSString*>*) purchasedProductIds;
```
#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```objectivec
ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];
```

**Swift**

```swift
let order = ACPTargetOrder(id: "ADCKKBC", total: NSNumber(value: 400.50), purchasedProductIds: ["34", "125"])
```

{% endtab %}
{% endtabs %}

### Target Product

`TargetProduct` encapsulates product ID and product category ID. You can instantiate `TargetProduct` class to create order parameters. For more information on Target Product parameters, see [here](https://docs.adobe.com/content/help/en/target/using/recommendations/entities/entity-attributes.html)

{% tabs %}
{% tab title="Android" %}
#### Syntax

```java
public TargetProduct(final String id, final String categoryId)
```

#### Example

```java
TargetProduct targetProduct = new TargetProduct("123", "Books");
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (nonnull instancetype) targetProductWithId: (nonnull NSString*) productId
categoryId: (nullable NSString*) categoryId;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**


```objectivec
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];
```

**Swift**

```swift
let product = ACPTargetProduct(id: "24D334", categoryId: "Stationary")
```
{% endtab %}
{% endtabs %}


### Target Parameters

`TargetParameters` encapsulates `mboxParameters`, `profileParameters`, `orderParameters` and `productParameters` and provides an easy way to pass these parameters in a Target request. 

{% tabs %}
{% tab title="Android" %}

#### Syntax

```java
TargetParameters targetParameters = new TargetParameters.Builder()
.parameters(new HashMap<String, String>())
.profileParameters(new HashMap<String, String>())
.product(new TargetProduct("productId", "productCategoryId"))
.order(new TargetOrder("orderId", 0.0, new ArrayList<String>()))
.build();
```

#### Example

```java
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("34");
purchasedProductIds.add("125"); 
TargetOrder targetOrder = new TargetOrder("123", 567.89, purchasedProductIds);

TargetProduct targetProduct = new TargetProduct("123", "Books");

Map<String, String> mboxParameters = new HashMap<String, String>();
mboxParameters1.put("status", "platinum");

Map<String, String> profileParameters = new HashMap<String, String>();
profileParameters1.put("gender", "male");

TargetParameters targetParameters = new TargetParameters.Builder()
.parameters(mboxParameters)
.profileParameters(profileParameters)
.product(targetProduct)
.order(targetOrder)
.build();
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (nonnull instancetype) targetParametersWithParameters: (nullable NSDictionary*) targetParameters
profileParameters: (nullable NSDictionary*) profileParameters
product: (nullable ACPTargetProduct*) product
order: (nullable ACPTargetOrder*) order;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

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
**Swift**

```objectivec
let mboxParameters = [
"status": "Platinum"
]
let profileParameters = [
"gender": "female"
]

let product = ACPTargetProduct(id: "24D334", categoryId: "Stationary")

let order = ACPTargetOrder(id: "ADCKKBC", total: NSNumber(value: 400.50), purchasedProductIds: ["34", "125"])

let targetParameters = ACPTargetParameters(parameters: mboxParameters, profileParameters: profileParameters, product: product, order: order)
```
{% endtab %}
{% endtabs %}

### Merge behavior of Target parameters

`TargetParameters` including `mboxParameters`, `profileParameters`, `orderParameters` and `productParameters` can be passed in Target APIs and also when creating `TargetPrefetch` or `TargetRequest` objects. The `TargetParameters` passed in public APIs are considered global parameters and are merged with the corresponding parameters in the individual `TargetRequest` or `TargetPrefetch` objects.

While merging, the new keys in the mbox parameters or the profile parameters are appended to the final dictionary while the keys with the same name are overwritten in each `TargetRequest` or `TargetPrefetch` object by those from global parameters. In the case or `TargetOrder` or `TargetProduct` objects, the object passed in global parameters shall replace the corresponding object in each of `TargetRequest` or `TargetPrefetch` objects.

## Target Sessions

With Target release v2.1.4 iOS and  v1.1.3 Android, Target extension now supports persistent sessions. When a Target request is received, a new session ID is generated if one doesn't already exist and is sent in the request. This session ID along with the Edge Host returned from the Target are stored in the persistent storage for the configured `target.sessionTimeout`. If not configured, the default value for the session timeout is 30 minutes. These variables are reset and removed from persistent storage if no Target request is received during the configured `target.sessionTimeout` or if  [resetExperience API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#reset-user-experience) is called.

## Visual preview

Visual preview mode allows you to easily perform end-to-end QA for Target activities by enrolling and previewing these activities on your device. This mode does not require a specialized testing set up. To get started, set up a URL scheme and generate the preview links. For more information, see [Target mobile preview](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/target-mobile-preview.html).

You can also set an application deep link that can be triggered when selections are made in the preview mode by using the [setPreviewRestartDeeplink API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#set-preview-restart-deep-link)

The `collectLaunchInfo` API is used to enter the visual preview mode. After the visual preview mode is enabled, a red floating button is displayed on the app screen. This button can be pressed to enter the visual preview mode.

{% tabs %}
{% tab title="Android" %}

On Android, when the application is launched as a result of a deeplink, `collectLaunchInfo` API will be invoked internally with the target Activity and deeplink information will be extracted from the Intent extras.

{% endtab %}

{% tab title="iOS" %}
#### Syntax

```text
+ (void) collectLaunchInfo: (nonnull NSDictionary*) userInfo;
```

#### Examples

Here are some examples in Objective-C and Swift:

**Objective-C**

```text
[ACPCore collectLaunchInfo: @{@"adb_deeplink":@"com.adobe.targetpreview://app.adobetarget.com?at_preview_token=tokenFromTarget"}];`
```

**Swift**

```swift
ACPCore.collectLaunchInfo(["adb_deeplink" : "com.adobe.targetpreview://app.adobetarget.com?at_preview_token=tokenFromTarget"])
```
{% endtab %}
{% endtabs %}

## Target with Analytics \(A4T\) <a id="integrating-adobe-target-with-analytics-a-4-t"></a>

To see the performance of your Target activities for certain segments, set up the Analytics for Target \(A4T\) cross-solution integration by enabling the A4T campaigns. This integration allows you use Analytics reports to examine your results. If you use Analytics as the reporting source for an activity, all reporting and segmentation for that activity is based on Analytics data collection. For more information, see [Adobe Analytics for Adobe Target \(A4T\)](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html).

## Configuration keys

If you need to update SDK configuration, programmatically, use the following information to change your Target configuration values. For more information, [Configuration API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| Key | Description |
| :--- | :--- |
| target.clientcode | Client code for your account. |
| target.timeout | Time, in seconds, to wait for a response from Target servers before timing out. |
| target.environmentId | Environment ID you want to use, if this is left blank, the default production environment will be used. |
| target.propertyToken | `at_property token` value, which is generated from the Target UI. If this value is left blank, no token is sent in the Target network calls. |
| target.previewEnabled | Boolean parameter, which can be used to enable/disable Target Preview. If not specified, then Preview will be enabled by default. |
| target.sessionTimeout | Time, in seconds, for which the Target session ID and Egde Host are persisted. If not specified, then default timeout value is 30 minutes. |

{% hint style="warning" %}
We recommend that you use Experience Platform Launch configuration to pass the property token instead of passing it in as a mbox parameter. If the property token is passed in Experience Platform Launch configuration and also as a mbox parameter, the token that was entered in the mbox parameter is discarded.
{% endhint %}

{% hint style="warning" %}
Currently `target.sessiontimeout` value can only be configured programmatically. For more information, refer [updateConfiguration API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference#programmatic-updates-to-configuration).
{% endhint %}

## Additional information

* Want to get your Target client code? See the **Client** row in [Configure mbox.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html).
* What is an mbox? See [How Target works in mobile apps](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html).
* What is Analytics for Target \(A4T\)? See [Adobe Analytics as the reporting source for Adobe Target \(A4T\)](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html).

