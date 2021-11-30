# Adobe Journey Optimizer

The [Adobe Journey Optimizer](https://business.adobe.com/products/journey-optimizer/adobe-journey-optimizer.html) extension for Adobe Experience Platform Mobile SDKs powers push notifications for your mobile apps. This extension helps you collects user push tokens and manages interaction measurement with Adobe Experience Platform services.

The following documentation details how to use the extension and required configurations to get started with push notifications for Adobe Journey Optimizer for Adobe Experience Platform services, app stores, and your apps.

## Before starting

1. Read the tutorial on [getting started with push configuration](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/configuration/push-config/push-gs.html?lang=en) to learn how to configure push channels in Adobe Journey Optimizer.
2. [Update your app's Datastream](#update-datastream-with-profile-dataset) in [Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection/)
3. Integrate with following extensions:
   * [Mobile Core](../../foundation-extensions/mobile-core/)
   * [Adobe Experience Platform Edge Network](../../foundation-extensions/experience-platform-extension/)
   * [Identity for Edge Network](../../foundation-extensions/identity-for-edge-network/)

### Update Datastream with a Profile dataset

Navigate to a previously configured Datastream by following the instructions in the [configure datastreams tutorial](../../getting-started/configure-datastreams.md) in [Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection/).

Select the pre-created **CJM Push Profile Dataset** in **Profile Dataset** dropdown (under the **Adobe Experience Platform** section) and select **Save**.

![](../../.gitbook/assets/screen-shot-2021-05-12-at-9.19.31-am.png)

## Setup Adobe Journey Optimizer extension

### Configure extension in the Data Collection UI

Go to the [Experience Platform Data Collection UI](https://experience.adobe.com/#/data-collection/), select mobile property and navigate to **Extensions** from the left navigation panel:

1. Navigate to the **Catalog** tab, locate the **Adobe Journey Optimizer** extension, and select **Install**
2. Select the pre-created **CJM Push Tracking Event Dataset** from the **Event Dataset** dropdown.
3. Select **Save**.
4. Follow the publishing process to update SDK configuration.

{% hint style="info" %}
The datasets selected should use a schema that uses the "Push Notification Tracking" XDM field group. The pre-created CJM Push Tracking Dataset contains this XDM field group in its schema definition. For more information, please read the tutorial on [setting up schemas and datasets](../../getting-started/setup-schemas-and-datasets.md).
{% endhint %}

![](../../.gitbook/assets/aoj-launch-configuration.png)

### Implement extension in mobile app

Follow these steps to integrate the Adobe Journey Optimizer extension.

#### Import the extension

{% tabs %}
{% tab title="Android" %}
### Java

1. Add the Mobile Core, Edge, Edge Identity, and Messaging extensions to your project using the app's Gradle file.

   ```java
   implementation 'com.adobe.marketing.mobile:core:1.+'
   implementation 'com.adobe.marketing.mobile:edge:1.+'
   implementation 'com.adobe.marketing.mobile:edgeidentity:1.+'
   implementation 'com.adobe.marketing.mobile:messaging:1.+'
   ```

2. Import the Mobile Core, Edge, Edge Identity, and Messaging extensions in your application class.

   ```java
    import com.adobe.marketing.mobile.*;
    import com.adobe.marketing.mobile.edge.identity.Identity;
   ```
{% endtab %}

{% tab title="iOS" %}
1. Add the Mobile Core, Edge, Edge Identity, and Messaging extensions to your project using Cocoapods. Add the following pods to your `Podfile`:

   ```swift
   use_frameworks!
   target 'YourTargetApp' do
       pod 'AEPCore'
       pod 'AEPEdge'
       pod 'AEPEdgeIdentity'
       pod 'AEPMessaging'
   end
   ```

2. Import the Mobile Core, Edge, Edge Identity, and Messaging libraries:

### Swift

```swift
// AppDelegate.swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPMessaging
```

### Objective-C

```objc
// AppDelegate.h
@import AEPCore;
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPMessaging;
```
{% endtab %}
{% endtabs %}

#### Register the extension with Mobile Core

{% tabs %}
{% tab title="Android" %}
### Java

```java
public class MobileApp extends Application {
    @Override
    public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);
      MobileCore.configureWithAppID("yourLaunchEnvironmentID");
      try {
        Edge.registerExtension();
        Identity.registerExtension();
        Messaging.registerExtension(); // register Messaging
        MobileCore.start(new AdobeCallback() {
          @Override
          public void call(final Object o) {
            // processing after start
          }});
      } catch (Exception e) {
        //Log the exception
      }
    }
}
```
{% endtab %}

{% tab title="iOS" %}
### Swift

```swift
// AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([Identity.self, Edge.self, Messaging.self], {
        MobileCore.configureWith(appId: "yourLaunchEnvironmentID")
    })
  ...
}
```

### Objective-C

```objc
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileEdgeIdentity.class, AEPMobileEdge.class, AEPMobileMessaging.class] completion:^{
    [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
  }];
  ...
}
```
{% endtab %}
{% endtabs %}

#### Sync the user push token with Adobe

After importing and registering the extensions with your application, you need to sync the push token with Adobe Experience Platform, by using the setPushIdentifier API.

{% tabs %}
{% tab title="Android" %}
To retrieve the push token from Firebase Messaging Service, please read the tutorial on [retrieving the registration token](https://firebase.google.com/docs/cloud-messaging/android/client#retrieve-the-current-registration-token) within the Firebase documentation. After retrieving the push token, you can use the following API to sync it with Profile in Platform.

### Java

#### Syntax

```java
public static void setPushIdentifier(final String pushIdentifier);
```

| **Variable** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `pushIdentifier` | String | The push token value. |

#### Example

```java
FirebaseMessaging.getInstance().getToken()
        .addOnCompleteListener(new OnCompleteListener<String>() {
            @Override
            public void onComplete(@NonNull Task<String> task) {
                if (task.isSuccessful()) {
                    String token = task.getResult();
                    MobileCore.setPushIdentifier(token);
                }
            }
        });
```
{% endtab %}

{% tab title="iOS" %}
### Swift

To retrieve the push token in iOS, please read the tutorial on [registering your application](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns) within Apple's documentation. After retrieving the push token, you can use the following API to sync it with Profile in Platform.

#### Syntax

```swift
public static func setPushIdentifier(_ deviceToken: Data?)
```

| **Variable** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `deviceToken` | Data | The push token value. |

#### Example

```swift
func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    MobileCore.setPushIdentifier(deviceToken)
}
```

### Objective-C

#### Syntax

```objc
public static func setPushIdentifier(_ deviceToken: Data?)
```

| **Variable** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `deviceToken` | Data | The push token value. |

#### Example

```objc
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken { 
    [AEPMobileCore setPushIdentifier:deviceToken];
}
```
{% endtab %}
{% endtabs %}

## Next steps

* [Track Push Interactions](api-reference.md#addpushtrackingdetails)

## Configuration keys

You can update the SDK configuration, including the Messaging configuration values, programatically by using the following information.

| Key | Required | Description | Data Type | Operating System |
| :--- | :--- | :--- | :--- | :--- |
| messaging.eventDataset | Yes | Experience Event Dataset ID which can be found from Experience Platform | String | Android/iOS |
| messaging.useSandbox | No | A variable that lets the `apnsSandbox` environment be used for receiving push notifications. More details can be found in the [messaging documentation](https://github.com/adobe/aepsdk-messaging-ios/blob/dev/Documentation/SetupSDK.md#using-apnssandbox-environment-for-push-notification) | Boolean | iOS |

