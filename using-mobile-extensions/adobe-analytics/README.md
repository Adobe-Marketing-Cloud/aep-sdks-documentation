# Adobe Analytics

## **Configure the Analytics extension in Launch**

1. In Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Analytics** extension, and click **Install**.
3. Type the extension settings.   For more information, see [Configure the Analytics Extension](./#configure-analytics-extension).
4. Click **Save**.
5. Follow the publishing process to update SDK configuration.

### **Configure the Analytics Extension**

![Adobe Analytics Extension Configuration](../../.gitbook/assets/mobile-analytics-configuration.png)

#### **Report suites**

{% hint style="info" %}
Want to know how to find report suite IDs? See [Report Suites](https://docs.adobe.com/content/help/en/analytics/admin/manage-report-suites/report-suites-admin.html).
{% endhint %}

Type one or more report suite identifiers to which the Analytics data should be sent. To add multiple report suite IDs, click **Add Another**; to remove these IDs, click **Remove Circle.** Report suite IDs can also be configured for the Development and Staging environments.

#### **Tracking server**

{% hint style="info" %}
Want to know what a tracking server is and where to find it? For more information, see [Correctly populate the trackingServer and trackingServerSecure variable](https://helpx.adobe.com/analytics/kb/determining-data-center.html).
{% endhint %}

Type the tracking domain to which all Analytics requests should be made.

#### **Offline enabled**

{% hint style="info" %}
Do you need offline tracking? For more information, see [Offline tracking](https://docs.adobe.com/content/help/en/analytics/implementation/javascript-implementation/offline-tracking.html).
{% endhint %}

When the **Offline Enabled** checkbox is selected, Analytics hits are queued when your device is offline and are sent later when your device is back online. To use offline tracking, ensure that your report suite is timestamp enabled .

{% hint style="danger" %}
If your report suite is timestamp enabled, the checkbox must be selected. If your report suite is not timestamped enabled, leave the checkbox deselected. If this setting is not configured correctly, data will be lost.

If you are not sure whether your report suite is timestamp enabled, contact Customer Care**.**
{% endhint %}

{% hint style="info" %}
If you currently send mobile SDK data to a report suite that also collects data from web JavaScript, you might need to set up a separate report suite for mobile data or include a custom timestamp on all JavaScript hits that use the`s.timestamp`variable. For more information, contact Customer Care.
{% endhint %}

#### Audience Manager forwarding

{% hint style="info" %}
For more information about Analytics server-side forwarding to Audience Manager, see [Analytics sever-side forwarding](./#server-side-forwarding-with-audience-manager).
{% endhint %}

If you set up Analytics server-side forwarding to Audience Manager, select the **Audience Manager Forwarding** checkbox. When this checkbox is selected, all SDK requests to Analytics servers are sent with an expected response code of **10**. This step ensures that Analytics traffic is forwarded to Audience Manager and that the Audience Manager User Profile is correctly updated in the SDK.

#### Backdate previous session info

{% hint style="warning" %}
Select the **Backdate Previous Session Info** checkbox **only** if you have timestamp-enabled report report suites.
{% endhint %}

When you select this checkbox, the SDK backdates the end-of-session lifecycle information so that this information can be attributed into its correct session. Session information currently consists of crashes and session length. The SDK also backdates the session information hit to 1 second after the last hit of the previous session. This means that crashes and session data will correlate with the correct date on which they occurred. One hit is backdated each time a new launch of the application is occurs.

For example, if you select the checkbox, Lifecycle session information or crash events are backdated to one second after the last hit was sent. If you do not select the checkbox, Lifecycle data is attached to the first hit of the subsequent session.

If this option is disabled, the Adobe SDK attaches the session information to the current lifecycle.

#### Batch limit

This setting creates a threshold number of hits to be sent in consecutive calls. For example, if you type or select **10**, each Analytics hit before the 10th hit is stored in the queue. When the 10th hit comes in, all 10 hits are sent to Analytics in the order in which they were generated.

{% hint style="info" %}
If you set a value greater than 0, ensure that the **Offline Enabled** checkbox is also selected.
{% endhint %}

The default value for this setting is 0, which means that hit batching is disabled, and all hits are immediately sent to Analytics as they are generated.

#### Launch hit delay

Number of seconds to wait before Analytics launch hits are sent from the SDK. Ensure that this setting is set at 5s or greater when using acquisition functionality from the [Mobile Services](../adobe-analytics-mobile-services.md) extension.

## Add Analytics to your app

{% tabs %}
{% tab title="Android" %}
Add the Analytics extension to your project using the app's Gradle file.

#### Java

Import the Analytics extension in your application's main activity.

```java
import com.adobe.marketing.mobile.*;
```
{% endtab %}

{% tab title="iOS" %}
​ 1. Add the library to your project via your Cocoapods `Podfile` by adding `pod 'ACPAnalytics'` ​ 2. Import the Analytics and Identity libraries:

#### Objective-C

```objectivec
#import "ACPCore.h"
#import "ACPAnalytics.h"
#import "ACPIdentity.h"
```

#### Swift

```swift
import ACPCore
import ACPAnalytics
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

Install Analytics

```jsx
npm install @adobe/react-native-acpanalytics
react-native link @adobe/react-native-acpanalytics
```

Importing the extension

```jsx
import {ACPAnalytics} from '@adobe/react-native-acpanalytics';
```

Getting the extension version

```jsx
ACPAnalytics.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPAnalytics version: " + version));
```
{% endtab %}
{% endtabs %}

### Register Analytics with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### Java

To call the set up methods that call the `setApplication()` method in the `onCreate()` method:

```java
public class MobileApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.ConfigureWithAppId("yourAppId");
        try {
            Analytics.registerExtension(); //Register Analytics with Mobile Core
            Identity.registerExtension();
            MobileCore.start(null);
        } catch (Exception e) {
            //Log the exception
         }
    }
}
```

**Important**: Analytics depends on the Identity extension and is automatically included in Core by Maven. When manually installing the Analytics extension, ensure that you add the `identity-1.x.x.aar` library to your project.
{% endtab %}

{% tab title="iOS" %}
In your app's`application:didFinishLaunchingWithOptions`, register Analytics with Mobile Core:

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore configureWithAppId:@"yourAppId"];
    [ACPAnalytics registerExtension];
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
     ACPAnalytics.registerExtension()
     ACPIdentity.registerExtension()
     ACPCore.start(nil)
     // Override point for customization after application launch. 
     return true;
}
```

**Important**: Analytics depends on the Identity extension and is automatically included in the Core pod. When installing the Analytics extension manually, ensure that you added the `libACPIdentity_iOS.a` library to your project.
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```jsx
import {ACPAnalytics} from '@adobe/react-native-acpcore';

initSDK() {
    ACPAnalytics.registerExtension();
}
```
{% endtab %}
{% endtabs %}

## Send Lifecycle Metrics to Analytics

To automatically report on the application lifecycle details in Analytics, ensure that you properly configure the lifecycle data collection. For more information, see [Lifecycle Metrics.](../mobile-core/lifecycle/)

## Send app states and actions to Analytics

To track mobile app states and actions in Adobe Analytics, implement the `trackAction` and `trackState` APIs from the Mobile Core extension. For more information, see [Track app actions](../mobile-core/mobile-core-api-reference.md#track-app-actions) and [Track app states](../mobile-core/mobile-core-api-reference.md#track-app-states-and-views).

{% hint style="info" %}
`trackState` reports the View State as **Page Name**, and state views are reported as **Page View** in Analytics. The value is sent to Analytics by using the page name variable \(`pagename=value`\).

`trackAction` reports the Action as an **event** and does not increment your page views in Analytics. The value is sent to Analytics by using the action variable \(`action=value`\).
{% endhint %}

## Integrations with Experience Platform solutions and services

### Analytics for Target \(A4T\)

To see the performance of your Target activities for some segments, you can set up the Analytics extension for Target \(A4T\) cross-solution integration by enabling the A4T campaigns. This integration allows you to use Analytics reports to examine your results. If you use Analytics as the reporting source for an activity, all reporting and segmentation for that activity is based on Analytics data collection. For more information, see [Target](https://docs.adobe.com/content/help/en/target/using/integrate/a4t/a4t.html).

### Server-side forwarding with Audience Manager

To enable the ability to share Analytics data with Audience Manager, in the Launch UI, select the **Audience Manager Forwarding** checkbox and install the Audience Manager extension. For more information, go to [Audience Manager](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-audience-manager).

### Video Analytics

For more information about collecting video analytics, see [Media Analytics for Audio and Video](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/).

## Set Products Variable

As _products_ variable cannot be set by processing rules, you need the syntax below in context data parameters to set serialized events directly on the hits that are sent to Analytics.

To set the products variable, set a context data key to `&&products`, and set the value by using the syntax that is defined for the products or merchandising variable. For more information, see [Implementing a Merchandising Variable](https://docs.adobe.com/content/help/en/analytics/components/variables/merchandising-variables/var-merchandising.html).

{% tabs %}
{% tab title="Android" %}
#### Java

#### Syntax

```java
cdata.put("&&products", "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]");
```

#### Example

```java
//create a context data dictionary
HashMap cdata = new HashMap<String, Object>();

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
cdata.put("&&products", ";Running Shoes;1;69.95,;Running Socks;10;29.99");
cdata.put("myapp.purchase", "1");
cdata.put("myapp.purchaseid", "1234567890");

// send the tracking call - use either a trackAction or TrackState call.
// trackAction example:
MobileCore.trackAction("purchase", cdata);
// trackState example:
MobileCore.trackState("Order Confirmation", cdata);
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

#### Syntax

```objectivec
[contextData setObject:@"Category;Product;Quantity;Price[,Category;Product;Quantity;Price]" forKey:@"&&products"];
```

#### Example

```objectivec
//create a context data dictionary
NSMutableDictionary *contextData = [NSMutableDictionary dictionary];

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
[contextData setObject:@";Running Shoes;1;69.95,;Running Socks;10;29.99" forKey:@"&&products"];
[contextData setObject:@"1234567890" forKey:@"m.purchaseid"];
[contextData setObject:@"1" forKey:@"m.purchase"];

// send the tracking call - use either a trackAction or TrackState call.
// trackAction example:
[ACPCore trackAction:@"purchase" data:contextData];
// trackState example:
[ACPCore trackState:@"Order Confirmation" data:contextData];
```

#### Swift

#### Syntax

```swift
contextData["&&products"] = "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]"
```

#### Example

```swift
//create a context data dictionary

//create a context data dictionary
var contextData: [AnyHashable : Any] = [:]

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
contextData["&&products"] = ";Running Shoes;1;69.95,;Running Socks;10;29.99"
contextData["m.purchaseid"] = "1234567890"
contextData["m.purchase"] = "1"

// send the tracking call - use either a trackAction or TrackState call.
// trackAction example:
ACPCore.trackAction("purchase", data: contextData)
// trackState example:
ACPCore.trackState("Order Confirmation", data: contextData)
```
{% endtab %}
{% endtabs %}

![Example Network Request](../../.gitbook/assets/products-bloodhound.png)

{% hint style="info" %}
You do not need to map the products variable with processing rules because the variable is directly set on the image request by the SDK.
{% endhint %}

### Set Products variable with merchandising eVars and product-specific events

Here is an example of the products variable with Merchandising eVars and product-specific events.

{% hint style="info" %}
If you trigger a product-specific event by using the `&&products` variable, you must also set that event in the `&&events` variable. If you do not set that event, it is filtered out during processing.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

#### Example

```java
//create a context data dictionary
HashMap cdata = new HashMap<String, Object>();

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
cdata.put("&&events", "event1");
cdata.put("&&products", ";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99");
cdata.put("myapp.purchase", "1");
cdata.put("myapp.purchaseid", "1234567890");

// send the tracking call - use either a trackAction or TrackState call.
// trackAction example:
MobileCore.trackAction("purchase", cdata);
// trackState example:
MobileCore.trackState("Order Confirmation", cdata);
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

#### Example

```objectivec
//create a context data dictionary
NSMutableDictionary *contextData = [NSMutableDictionary dictionary];

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
[contextData setObject:@"event1" forKey:@"&&events"];
[contextData setObject:@";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99" forKey:@"&&products"];
[contextData setObject:@"1234567890" forKey:@"m.purchaseid"];
[contextData setObject:@"1" forKey:@"m.purchase"];

// send the tracking call - use either a trackAction or TrackState call.
// trackAction example:
[ACPCore trackAction:@"purchase" data:contextData];
// trackState example:
[ACPCore trackState:@"Order Confirmation" data:contextData];
```
{% endtab %}
{% endtabs %}

## Event serialization

Event serialization is not supported by processing rules. To set serialized events directly on the hits sent to Analytics, use the following syntax in context data parameters:

{% tabs %}
{% tab title="Android" %}
#### Java

#### Syntax

```java
cdata.put("&&events", "event1:12341234");
```

#### Example

```java
//create a context data dictionary
HashMap cdata = new HashMap<String, Object>();

// add events
cdata.put("&&events", "event1:12341234");

// send a tracking call - use either a trackAction or TrackState call.
// trackAction example:
MobileCore.trackAction("Action Name", cdata);
// trackState example:
MobileCore.trackState("State Name", cdata);
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

#### Syntax

```objectivec
[contextData setObject:@"eventN:serial number" forKey:@"&&events"];
```

#### Example

```objectivec
//create a context data dictionary
NSMutableDictionary *contextData = [NSMutableDictionary dictionary];

// add events
[contextData setObject:@"event1:12341234" forKey:@"&&events"];

// send the tracking call - use either a trackAction or trackState call.
// trackAction example:
[ACPCore trackAction:@"Action Name" data:contextData];
// trackState example:
[ACPCore trackState:@"State Name" data:contextData];
```
{% endtab %}
{% endtabs %}

## Videos

### Using [trackState](../mobile-core/mobile-core-api-reference.md#track-app-states-and-views) APIs to send data to Adobe Analytics

{% embed url="https://video.tv.adobe.com/v/26260/?quality=12" caption="" %}

## Configuration keys

To update the SDK configuration programmatically, use the following information to change your Analytics configuration values. For more information, see [Configuration Methods Reference](./).

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Required</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>analytics.server</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">See <a href="./#tracking-server">Tracking Server</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>analytics.rsids</code>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">
        <p>See <a href="./#report-suites">Report Suites</a>
        </p>
        <p>Multiple report suite IDs can be comma separated with no space in- between.
          For example:
          <br /><code>&quot;rsids&quot; : &quot;rsid&quot; &quot;rsids&quot; : &quot;rsid1,rsid2&quot;</code>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>analytics.batchLimit</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">See <a href="./#batch-limit">Batch Limit</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>analytics.aamForwardingEnabled</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">See <a href="./#audience-manager-forwarding">Audience Manager Forwarding</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>analytics.offlineEnabled</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">See <a href="./#offline-enabled">Offline Enabled</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>analytics.backdatePreviousSessionInfo</code>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">See <a href="./#backdate-previous-session-info">Backdate Previous Session Info.</a>
      </td>
    </tr>
  </tbody>
</table>