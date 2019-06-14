# Adobe Campaign Standard

{% hint style="info" %}
**Before** you install or configure the Campaign Standard extension, read [_Getting Started_](../../getting-started/create-a-mobile-property.md) and [Configuring a mobile application using Adobe Experience Platform SDKs](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html).
{% endhint %}

{% hint style="danger" %}
If you participated in the Campaign Standard beta, to use the new Campaign Standard extension, go to [launch.adobe.com](https://launch.adobe.com), instead of the Launch integration environment, .
{% endhint %}

## Configure the Campaign Standard extension in Launch

1. In Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Campaign Standard** extension, and click **Install**.
3. Provide the extension settings.
4. Click **Save**.
5. Follow the publishing process to update SDK configuration.

### Configure the Campaign Standard extension

![](../../.gitbook/assets/campaign-extension-config-v4.png)

#### Campaign Standard endpoints

Provide endpoint URL\(s\) for your Campaign Standard instances. You can specify up to three unique endpoints for your development, staging, and production environments. In most cases, the server endpoint is the root URL address, for example, `companyname.campaign.adobe.com`.

{% hint style="warning" %}
For this extension, these endpoint URLs should be typed in **without** the `http://` or `https://.`and **cannot** end with a forward slash.
{% endhint %}

#### pKey

A unique, auto-generated identifier for a mobile app that was configured in Adobe Campaign Standard. After you configured this extension in Launch, configure your Launch mobile property in Campaign Standard. For more information, see [Setting up your Adobe Launch application in Adobe Campaign](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html#SettingupyourAdobeLaunchapplicationinAdobeCampaign).  
  
When the configuration in Campaign is successful, the pKey is automatically generated, as per the Campaign Standard instance and configured in Launch Campaign extension for successful validation.

#### MCIAS region

Select an MCIAS region based on your customer's location or enter a custom endpoint. The SDK retrieves all in-app messaging rules and definition payloads from this endpoint.

{% hint style="warning" %}
For this extension, the custom MCIAS endpoint URL should be typed in **without** the `http://` or `https://` and **cannot** end with a forward slash.
{% endhint %}

#### Request timeout

Time in seconds to wait for a response from the in-app messaging service before timing out. The default timeout value is 5 seconds, and the minimum timeout value is 1 second.

{% hint style="warning" %}
The **Request Timeout** value must be a non-zero number.
{% endhint %}

## Add the Campaign Standard extension to your app

Remember the following information when you add the Campaign extension to your app:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Extension</th>
      <th style="text-align:left">Information</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Campaign Standard</td>
      <td style="text-align:left">
        <p></p>
        <p>This Campaign Standard extension requires the <a href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core">Mobile Core</a>,
          <a
          href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile">Profile</a>, <a href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle">Lifecycle</a>,
            and <a href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals">Signal</a> extensions.
            You should always ensure that you get the latest version of the extension.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Profile</td>
      <td style="text-align:left">
        <p></p>
        <p>The Profile extension is required for In-App trigger frequencies to work
          accurately. For more information, see <a href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile">Profile</a>.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Signal</td>
      <td style="text-align:left">The Signal extension is required for all postback rules to work. For more
        information, see <a href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals">Signal</a>.</td>
    </tr>
    <tr>
      <td style="text-align:left">Lifecycle</td>
      <td style="text-align:left">
        <p>Lifecycle extension is required for a profile to get registered in Campaign.
          You also need to implement Lifecycle APIs. For more information, see</p>
        <p><a href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-android">Lifecycle extension in Android</a> or
          <a
          href="https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-ios">Lifecycle extension in iOS</a>.</p>
      </td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
The instructions to add these extensions to your mobile app are also available in Launch. To access the installation dialog box, open your mobile property, click the **Environments** tab, and click **Install**.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
1. Add the Campaign Standard, [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) and [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile) extensions to your project using the app's Gradle file.

```java
implementation 'com.adobe.marketing.mobile:campaign:1.+'
implementation 'com.adobe.marketing.mobile:userprofile:1.+'
implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
```

2. Import the Campaign Standard, [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core), [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile), [Lifecycle](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle), and [Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals) extensions in your application's main activity.

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Campaign;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
```

{% hint style="info" %}
For a manual install, go to [https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android) and fetch the Mobile Core, Campaign Standard, Profile, Lifecycle, and Signal artifacts. 
{% endhint %}
{% endtab %}

{% tab title="iOS" %}
1. Add the Campaign Standard, [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) and [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile) extensions to your project using Cocoapods.

![](../../.gitbook/assets/acs-pods.png)

{% hint style="info" %}
For a manual install, go to [https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS) and fetch the Mobile Core, Campaign Standard, Profile, Lifecycle, and Signal artifacts. 
{% endhint %}

2. In Xcode, import the Mobile Core, Campaign Standard, Profile, Lifecycle, and Signal extensions:

#### Objective-C

```objectivec
#import "ACPCore.h"
#import "ACPCampaign.h"
#import "ACPUserProfile.h"
#import "ACPIdentity.h"
#import "ACPLifecycle.h"
#import "ACPSignal.h"
```

#### Swift

```swift
import ACPCore
import ACPCampaign
import ACPUserProfile
```
{% endtab %}

{% tab title="React Native" %}
You'll need to install the SDK with [npm](https://www.npmjs.com/) and configure the native Android/iOS project in your react native project. Before installing the Campaign Standard extension, you'll need to install the [Core](../mobile-core/) extension. Follow these steps to get started:

#### Create React Native Project

```bash
react-native init MyReactApp
```

#### Install JavaScript packages

Install and link the @adobe/react-native-acpcampaign package:

```bash
npm install @adobe/react-native-acpcampaign
react-native link @adobe/react-native-acpcampaign
```

#### Import the extension

```bash
import {ACPCampaign} from '@adobe/react-native-acpcampaign';
```
{% endtab %}
{% endtabs %}

### Register the Campaign Standard extension with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### **Java**

1. In your app's `OnCreate` method, call `MobileCore.setApplication()` for your Android app, register extensions, and start Mobile Core:

```java
public class CampaignTestApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);

        try {
            Campaign.registerExtension();
            UserProfile.registerExtension();
            Identity.registerExtension();
            Lifecycle.registerExtension();
            Signal.registerExtension();
            MobileCore.start(new AdobeCallback () {
                @Override
                public void call(Object o) {
                    MobileCore.configureWithAppID("launch-EN2c0ccd3a457a4c47b65a6b085e269c91-staging");
                }
            });
        } catch (InvalidInitException e) {
            Log.e("CampaignTestApp", e.getMessage());
        }

    }
}
```

2. Implement the Lifecycle APIs so that your Android app can send Mobile app registration data to Campaign \(the Experience Cloud ID and the Push Platform\).  

For more information about starting Lifecycle, see [Lifecycle extension in Android](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-android).
{% endtab %}

{% tab title="iOS" %}
Register the Campaign extension and start the Core extension:

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"launch-EN2c0ccd3a457a4c47b65a6b085e269c91-staging"];
	
	[ACPCampaign registerExtension];
    [ACPUserProfile registerExtension];
    [ACPIdentity registerExtension];
    [ACPLifecycle registerExtension];
    [ACPSignal registerExtension];
    [ACPCore start:^{
        [ACPCore lifecycleStart:nil];
    }];
  // Override point for customization after application launch.
  return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
   ACPCampaign.registerExtension()
	ACPUserProfile.registerExtension()
	ACPIdentity.registerExtension()
	ACPLifecycle.registerExtension()
	ACPSignal.registerExtension()
	ACPCore.start {
    	ACPCore.lifecycleStart(nil)
	}
}
  return true;
}
```

3. Implement the Lifecycle APIs so that your iOS app can send Mobile app registration data to Campaign \(the Experience Cloud ID and the Push Platform\).  
For more information about starting Lifecycle, see [Lifecycle extension in iOS](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/lifecycle/lifecycle-extension-in-ios).
{% endtab %}

{% tab title="React Native" %}
To register the Campaign Standard with Core, use the following API:

#### JavaScript

```javascript
ACPCampaign.registerExtension();
```
{% endtab %}
{% endtabs %}

### Set up in-app messaging

{% hint style="info" %}
Need help creating an in-app message using Adobe Campaign? For more information, see [Preparing and sending an In-App message](https://helpx.adobe.com/campaign/standard/channels/using/preparing-and-sending-an-in-app-message.html).
{% endhint %}

{% hint style="warning" %}
If you are developing an Android application, to correctly display fullscreen in-app messages, add the Campaign Standard extension's `FullscreenMessageActivity` to your AndroidManifest.xml file:

```markup
<activity android:name="com.adobe.marketing.mobile.FullscreenMessageActivity" />
```
{% endhint %}

For message types that allow you to target Adobe Campaign profiles \(CRM profiles\) that have subscribed to your mobile application, configure the personal attributes that are linked to their campaign profiles with the `setLinkageFields` API. For more information, see [Campaign API reference](adobe-campaign-standard-api-reference.md). 

#### Implementing local notifications

To implement local notifications in Android, update the AndroidManifext.xml file with `<receiver android:name="com.adobe.marketing.mobile.LocalNotificationHandler/>`. To configure the notification icons to use the Mobile Core APIs, see [Configuring notification icons](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#configuring-notification-icons).

### Set up push messaging

{% hint style="info" %}
Need help creating a push notification using Adobe Campaign? For more information, see [Preparing and sending a push notification](https://helpx.adobe.com/campaign/standard/channels/using/preparing-and-sending-a-push-notification.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Obtain the registration ID/token by using the [Firebase Cloud Messaging \(FCM\) APIs](https://firebase.google.com/docs/cloud-messaging/android/client).

### setPushIdentifier

#### Syntax

```java
void setPushIdentifier(final String registrationID)
```

#### Example

```java
MobileCore.setPushIdentifier(registrationID);
```
{% endtab %}

{% tab title="iOS" %}
{% hint style="warning" %}
iOS simulators do not support push messaging.
{% endhint %}

After you complete [Apple's instructions](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1) to get your app ready to handle push notifications, set the push token by using the [`setPushIdentifier`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#set-the-push-identifier) API:

### setPushIdentifier

#### Objective-C

#### Syntax

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

#### Example

```objectivec
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  // Set the deviceToken that the APNS has assigned to the device
  [ACPCore setPushIdentifier:deviceToken];
  //...
}
```

#### Swift

```swift
ACPCore.setPushIdentifier(deviceToken)
```
{% endtab %}

{% tab title="React Native" %}
Follow instructions in the Android/iOS tabs to setup platform specific push configuration, then use the following API in your React Native project:

### setPushIdentifier

#### JavaScript

```javascript
ACPCore.setPushIdentifier("pushIdentifier");
```
{% endtab %}
{% endtabs %}

### Tracking for push and in-app messaging

To set up postbacks to track push and in-app messages, go to [Step 3 Create rules for In-App tracking postback](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html#Step4Createrulesforpushnotificationstrackingpostback) and [Step 4 Create rules for push notifications tracking postback](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html#Step4Createrulesforpushnotificationstrackingpostback).

## Deleting mobile properties in Launch

{% hint style="danger" %}
Deleting your property in Launch might cause disruption to your recurring push and in-app messaging activities.
{% endhint %}

If you delete your mobile property in Launch, review your mobile property status in Campaign Standard and ensure that the property displays an updated **Deleted in Launch** status. For more information about deleting a property, see [Delete a Property](https://docs.adobelaunch.com/launch-reference/administration/companies-and-properties#delete-a-property).

To remove the corresponding mobile app in Campaign Standard, click **Remove from ACS**. For more information, see [Deleting your Adobe Launch mobile application](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html#DeletingyourAdobeLaunchapplication).

{% hint style="warning" %}
Deleting your mobile property in Launch does not automatically delete your Campaign Standard mobile app.
{% endhint %}

