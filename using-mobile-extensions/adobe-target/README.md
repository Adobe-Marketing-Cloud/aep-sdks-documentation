# Adobe Target

Adobe Target helps test, personalize, and optimize mobile app experiences based on user behavior and mobile context. You can deliver interactions that engage and convert through iterative testing and rules-based and AI-powered personalization.

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

To add Target to your app:

{% tabs %}
{% tab title="Android" %}
#### Java

1. Add the Mobile Core and Target extensions to your project using the app's Gradle file.

   ```java
    implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
    implementation 'com.adobe.marketing.mobile:target:1.+'
   ```

2. Import the Target extension to your application's main activity.

   ```java
   import com.adobe.marketing.mobile.*;
   ```
{% endtab %}

{% tab title="iOS" %}
1. Add the Mobile Core and Target CocoaPods to your project via your `Podfile`.

   ```text
    pod 'ACPCore'
    pod 'ACPTarget'
   ```

2. Import the Target and Identity libraries.

   **Objective C**

   ```objectivec
       #import "ACPCore.h"
       #import "ACPTarget.h"
       #import "ACPIdentity.h"
       #import "ACPTargetRequestObject.h"
       #import "ACPTargetPrefetchObject.h"
   ```

   **Swift**

   ```swift
       #import ACPCore
       #import ACPTarget
       #import ACPIdentity
   ```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

1. Install Target.

   ```javascript
    npm install @adobe/react-native-acptarget
    react-native link @adobe/react-native-acptarget
   ```

2. Import the extension and related libraries.

   ```javascript
    import {ACPTarget, ACPTargetPrefetchObject, ACPTargetRequestObject, ACPTargetOrder, ACPTargetProduct, ACPTargetParameters} from '@adobe/react-native-acptarget';
   ```

3. Get the extension version.

   ```javascript
    ACPTarget.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPTarget version: " + version));
   ```
{% endtab %}
{% endtabs %}

### Register Target with Mobile Core

To register Target with Mobile Core:

{% tabs %}
{% tab title="Android" %}
#### Java

In your application's `onCreate()` method, after calling the `setApplication()` method, register Target with Mobile Core.

Here is code sample that calls these set up methods:

```java
public class TargetApp extends Application {

 @Override
 public void onCreate() {
     super.onCreate();
     MobileCore.setApplication(this);
     MobileCore.configureWithAppId("yourAppId");

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
#### Objective C

In your app's `didFinishLaunchingWithOptions` function, register the Target extension with Mobile Core:

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPCore configureWithAppId:@"yourAppId"];
  [ACPTarget registerExtension];
  [ACPIdentity registerExtension];
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

{% tab title="React Native" %}
To register the Target extension with the Mobile Core extension, use the following API:

#### JavaScript

```javascript
ACPTarget.registerExtension();
```
{% endtab %}
{% endtabs %}

## Parameters in a Target request

Here is some information about the parameters in a Target request:

### Target Order class

The `TargetOrder` class encapsulates the order ID, the order total, and the purchased product IDs. You can instantiate this class to create order parameters. For more information about Target Order parameters, see [Create an Order Confirmation mbox - mbox.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/orderconfirm-create.html).

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

Here are some examples in Objective C and Swift:

**Objective C**

```objectivec
ACPTargetOrder *order = [ACPTargetOrder targetOrderWithId:@"ADCKKBC" total:@(400.50) purchasedProductIds:@[@"34", @"125"]];
```

**Swift**

```swift
let order = ACPTargetOrder(id: "ADCKKBC", total: NSNumber(value: 400.50), purchasedProductIds: ["34", "125"])
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```javascript
var targetOrder = new ACPTargetOrder("ADCKKBC", 400.50, ["34","125"]);
```
{% endtab %}
{% endtabs %}

### Target Product class

The `TargetProduct` class encapsulates the product ID and the product category ID, and you can instantiate this class to create order parameters. For more information about Target Product parameters, see [Entity attributes](https://docs.adobe.com/content/help/en/target/using/recommendations/entities/entity-attributes.html)

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

Here are some examples in Objective C and Swift:

**Objective C**

```objectivec
ACPTargetProduct *product = [ACPTargetProduct targetProductWithId:@"24D334" categoryId:@"Stationary"];
```

**Swift**

```swift
let product = ACPTargetProduct(id: "24D334", categoryId: "Stationary")
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

```javascript
var targetProduct = new ACPTargetProduct("24D334", "Stationary");
```
{% endtab %}
{% endtabs %}

### Target Parameters

`TargetParameters` encapsulates `mboxParameters`, `profileParameters`, `orderParameters`, and `productParameters` and allows you easily pass these parameters in a Target request.

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

Here are some examples in Objective C and Swift:

**Objective C**

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

{% tab title="React Native" %}
**JavaScript**

```javascript
var mboxParameters = {"status": "platinum"};
var profileParameters = {"gender": "female"};
var targetProduct = new ACPTargetProduct("24D334", "Stationary");
var purchaseIDs = ["34","125"];
var targetOrder = new ACPTargetOrder("ADCKKBC", 400.50, purchaseIDs);
var targetParameters = new ACPTargetParameters(mboxParameters, profileParameters, targetProduct, targetOrder);
```
{% endtab %}
{% endtabs %}

### Merge behavior of Target parameters

`TargetParameters`, such as `mboxParameters`, `profileParameters`, `orderParameters`, and `productParameters`, can be passed in the Target APIs and can also be passed in when you create `TargetPrefetch` or `TargetRequest` objects. The `TargetParameters` that are passed in the public APIs are global parameters and are merged with the corresponding parameters in the individual `TargetRequest` or `TargetPrefetch` objects.

When merging, the new keys in the mbox parameters or the profile parameters are appended to the final dictionary, and the keys with the same name are overwritten in each `TargetRequest` or `TargetPrefetch` object by the keys from the global parameters. For `TargetOrder` or `TargetProduct` objects, the object that is passed to the global parameters replaces the corresponding object in the `TargetRequest` or `TargetPrefetch` objects.

## Target sessions

The Target extension \(version 2.1.4 for iOS\) and \(version 1.1.3 for Android\) now supports persistent sessions. When a Target request is received, if a session ID does not exist, a new ID is generated and is sent in the request. This ID, with the Edge Host that is returned from Target, is kept in persistent storage for the configured `target.sessionTimeout` period. If the timeout value is not configured, the default value is 30 minutes.

If no Target request is received during the configured `target.sessionTimeout` or if the [resetExperience](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#resetExperience) API is called, these variables are reset and removed from persistent storage.

## Visual preview

The visual preview mode allows you to easily perform end-to-end QA activities by enrolling and previewing these activities on your device. This mode does not require a specialized testing set up. To get started, set up a URL scheme and generate the preview links. For more information about setting up Target visual preview, see [Target mobile preview](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/target-mobile-preview.html). For more information about setting URL schemes for iOS, see [Defining a Custom URL Scheme for Your App](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app). For more information about setting URL schemes for Android, see [Create Deep Links to App Content](https://developer.android.com/training/app-links/deep-linking).

You can also set an application deep link that can be triggered when selections are made in the preview mode by using the [setPreviewRestartDeeplink](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#setPreviewRestartDeeplink) API.

To enter the preview visual mode, use the `collectLaunchInfo` API to enable the mode and click the red floating button that appears on the app screen. For more information, see [collectLaunchInfo](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#collect-launch-information).

{% hint style="info" %}
After making preview mode selections, the first mbox request made may fail due to a caching issue on the Target server. For more information see [https://docs.adobe.com/content/help/en/target/using/release-notes/known-issues-resolved-issues.html\#preview](https://docs.adobe.com/content/help/en/target/using/release-notes/known-issues-resolved-issues.html#preview).

The mbox request that failed can be retried to successfully retrieve the test offer content.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
On Android, when the application is launched as a result of a deep link, the `collectLaunchInfo` API is internally invoked, and the Target activity and deep link information is extracted from the Intent extras.

{% hint style="info" %}
The SDK can only collect information from the launching Activity if [`setApplication`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#application-reference-android-only) has been called. Setting the Application is only necessary on an Activity that is also an entry point for your application. However, setting the Application on each Activity has no negative impact and ensures that the SDK always has the necessary reference to your Application. We recommend that you call `setApplication` in each of your Activities.
{% endhint %}
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

## Offer Prefetch

The SDK can minimize the number of times it reaches out to Target servers to fetch offers by caching server responses. With a successful prefetch call for mbox locations, offer content is retrieved and cached in the SDK. This content is retrieved from the cache for all future [retrieveLocationContent](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#retrieveLocationContent) API calls for the specified mbox names. This prefetch process reduces the offer load time and network calls that were made to the Target servers, and the prrocess allows Target to be notified which mbox was visited by the mobile app user.

{% hint style="warning" %}
Prefetched offer content does not persist across application launches. The prefetch content is cached as long as the application lives in memory or until the API to clear the cache is called. For more information, see [clearPrefetchCache](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/target-api-reference#clearPrefetchCache).
{% endhint %}

{% hint style="warning" %}
Offer prefetch is not available while visual preview mode is enabled.
{% endhint %}

## Target with Analytics \(A4T\) <a id="integrating-adobe-target-with-analytics-a-4-t"></a>

To track the performance of your Target activities for certain segments, set up the Analytics for Target \(A4T\) cross-solution integration by enabling the A4T campaigns. This integration allows you to use Analytics reports to examine your results. If you use Analytics as the reporting source for an activity, all reporting and segmentation for that activity is based on Analytics data collection. For more information, see [Adobe Analytics for Adobe Target \(A4T\)](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html).

Once Analytics is listed as the reporting source for an activity on Target UI, A4T works out of the box in the Target SDK. The Target SDK extension extracts the A4T payload from the Target server response, dispatches an event for Analytics SDK extension to send an internal track action request to the configured Analytics server.

The A4T payload returned from Target servers is sent to Adobe Analytics in the following cases:

* When one or more locations are retrieved using [retrieveLocationContent](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#retrievelocationcontent) API call.
* When one or more prefetched locations are loaded and a subsequent [locationsDisplayed](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-target/target-api-reference#locationsdisplayed) API call is made for the location\(s\).

{% hint style="warning" %}
For A4T data to be sent to Adobe Analytics client-side, make sure Analytics SDK extension is installed and registered in your mobile application. For more information, see [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics).
{% endhint %}

## Configuration keys

To programmatically update SDK configuration, use the following information to change your Target configuration values:

For more information, see [Programmatic updates to Configuration](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference#programmatic-updates-to-configuration).

| Key | Description | Data Type |
| :--- | :--- | :--- |
| target.clientcode | Client code for your account. | String |
| target.timeout | Time, in seconds, to wait for a response from Target servers before timing out. | Integer |
| target.environmentId | Environment ID you want to use. If the value is left blank, the default production environment will be used. | Integer |
| target.propertyToken | `at_property` token value, which is generated from the Target UI. If this value is left blank, no token is sent in the Target network calls. | String |
| target.previewEnabled | Boolean parameter, which can be used to enable/disable Target Preview. If not specified, then Preview will be enabled by default. | Boolean |
| target.sessionTimeout | The duration, in seconds, during which the Target session ID and Edge Host are persisted. If this value is not specified, the default timeout value is 30 minutes. | Integer |
| target.server | _Optional_. If provided, all Target requests will be sent to this host. Available since v2.1.7 \(iOS\), v1.1.6 \(Android\). e.g. - `mytargetdomain.com` | String |

{% hint style="warning" %}
We recommend that, instead of passing the property token as a mbox parameter, you use an Experience Platform Launch configuration so that Target can pass the token. If the token is passed both in an Experience Platform Launch configuration, and as a mbox parameter, the token that was provided as the mbox parameter is discarded.
{% endhint %}

{% hint style="warning" %}
Currently, the `target.sessiontimeout` value can only be configured programmatically. For more information, see [updateConfiguration](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference#programmatic-updates-to-configuration).
{% endhint %}

## Additional information

* Want to get your Target client code? See the **Client** row in [Configure mbox.js](https://docs.adobe.com/content/help/en/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html).
* What is an mbox? See [How Target works in mobile apps](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/mobile-how-target-works-mobile-apps.html).
* What is Analytics for Target \(A4T\)? See [Adobe Analytics as the reporting source for Adobe Target \(A4T\)](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html).

