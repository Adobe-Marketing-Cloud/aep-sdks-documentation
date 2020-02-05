# Get the Experience Platform SDK

The Adobe Experience Platform SDK is available for iOS via [Cocoapods](https://cocoapods.org/), Android via [Gradle](https://gradle.org), and for React Native projects via [Node Package Manager](https://nodejs.org).

Follow the directions below to include the SDK into your mobile application.

{% hint style="info" %}
For iOS and Android projects, the recommended approach to integrating the SDK is to use Cocoapods, Gradle, and/or npmjs. SDK libraries are also available on [Github](https://github.com/Adobe-Marketing-Cloud/acp-sdks/).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### Java

{% hint style="warning" %}
The Experience Platform SDK for Android supports Android 4.0 \(API 14\) or later.
{% endhint %}

1. Open the mobile property you created earlier in Experience Platform.
2. On your property's details page, click on the **Environments** tab.

   The **Environments** tab lists the different environments that you can publish. 
   
2. In the row for the **Development** environment, click on the install package icon (![](../.gitbook/assets/package.png)).

   You should see a dialog box similar to the following:

   ![](../.gitbook/assets/android.png)
   
3. On the **Mobile Install Instructions** dialog box, select the **Android** tab.
4. Follow the instructions for using Gradle with Android.

    The necessary dependencies and initialization code can be copied from the dialog box to your app project.

{% endtab %}

{% tab title="iOS" %}
### Objective C / Swift

{% hint style="warning" %}
**Important:** Adobe Experience Platform SDKs for iOS supports **iOS 10 or later.**
{% endhint %}

1. Open a previously created and configured **Mobile** property in Launch, and click on the **Environments** tab, and then click on the install package icon  (![](../.gitbook/assets/package.png)). 
2. On the **Mobile Install Instructions** dialog box, select **iOS**.
3. Follow the instructions for using CocoaPods with iOS.
4. Under the initialization code, choose Objective C or Swift.

The necessary dependencies and initialization code can be copied from the dialog box to your app project.

You should see a pop-up similar to the following \(image below shows iOS\):

![](../.gitbook/assets/obj-c.png)
{% endtab %}

{% tab title="React Native" %}
### React Native

{% hint style="info" %}
For React Native, we recommend that you first install [Node.js](https://nodejs.org) to download packages from [npm](https://npmjs.com). For additional instructions on getting started with React Native applications, see this [tutorial](https://facebook.github.io/react-native/docs/getting-started).
{% endhint %}

For the latest React Native installation instructions, see the README file in the [react-native-acpcore](https://github.com/adobe/react-native-acpcore) repository.
{% endtab %}
{% endtabs %}

## Manual installation

If you cannot access the installation dialog box, complete the following sections to get the Mobile SDKs. 

### Configure the SDK with an Environment ID

To initialize the SDK, you will need to first configure the SDK with an **Environment ID** from Adobe Experience Platform Launch. The **Environment ID** links the configuration from a mobile property with your SDK implementation.

{% hint style="info" %}
To find your Environment ID for an environment, in Experience Platform Launch, go to the **Environments** tab \(found in a previously created and configured mobile property\) and click on the corresponding![](../.gitbook/assets/screen-shot-2018-10-18-at-11.22.17-am.png)icon.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

1. In the app, create `MainActivity.java` .
2. Add `MobileCore.configureWithAppID("PASTE_ENVIRONMENT_ID_HERE");`
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

In Xcode, find your `didFinishLaunchingWithOptions` in `AppDelegate.m` and add:

```objectivec
[ACPCore configureWithAppId:@"PASTE_ENVIRONMENT_ID_HERE"];
```

#### Swift

In Xcode, find your `didFinishLaunchingWithOptions` in AppDelegate.swift and add:

```swift
ACPCore.configure(withAppId: "PASTE_ENVIRONMENT_ID_HERE")
```
{% endtab %}
{% endtabs %}

### Initializing the SDK

{% tabs %}
{% tab title="Android" %}
#### Java

```jsx
@Override
public void onCreate() {
  //...
  MobileCore.setApplication(this);
  MobileCore.configureWithAppID("PASTE_ENVIRONMENT_ID_HERE");

  try {
    Identity.registerExtension();
    Lifecycle.registerExtension();
    Signal.registerExtension();
  } catch (Exception e) {
    // handle exception
  }

  MobileCore.start(null);
}
```
{% endtab %}

{% tab title="iOS" %}
#### Objective C

```jsx
// Import the SDK
#import "ACPCore.h"
#import "ACPLifecycle.h"
#import "ACPIdentity.h"
#import "ACPSignal.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  //...
  [ACPCore configureWithAppId:@"PASTE_ENVIRONMENT_ID_HERE"];
  [ACPIdentity registerExtension];
  [ACPLifecycle registerExtension];
  [ACPSignal registerExtension];

  [ACPCore start:nil];
}
```
{% endtab %}

{% tab title="React Native" %}
#### Javascript

> Tip: We recommend that you initialize the SDK by using native code in your `AppDelegate` and `MainApplication` in iOS and Android, respectively. You can also initialize the SDK in Javascript \([React Native](https://github.com/adobe/react-native-acpcore)\).

```jsx
import {ACPCore, ACPLifecycle, ACPIdentity, ACPSignal, ACPMobileLogLevel} from '@adobe/react-native-acpcore';

initSDK() {
    ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
    ACPCore.configureWithAppId("PASTE_ENVIRONMENT_ID_HERE");
    ACPLifecycle.registerExtension();
    ACPIdentity.registerExtension();
    ACPSignal.registerExtension();
    ACPCore.start();
}
```
{% endtab %}
{% endtabs %}

### Ensure app permissions \(Android\)

The SDK requires standard [network connection](https://developer.android.com/training/basics/network-ops/connecting) permissions in your manifest to send data, collect cellular provider, and record offline tracking calls.

To enable these permissions, add the following lines to your `AndroidManifest.xml` file, located in your app's application project directory:

```markup
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

## Enable the Experience Cloud Identity service

Formerly known as Marketing Cloud ID \(MCID\), the Experience Cloud ID \(ECID\) service provides a cross-channel notion of identity across Experience Cloud solutions and is a prerequisite for most implementations.

{% hint style="info" %}
To confirm that you have the correct Experience Cloud Org ID in the Mobile Core settings page, see [Get the SDK](get-the-sdk.md).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Import the Identity framework to your project:

#### Java

```java
import com.adobe.marketing.mobile.*;
```

Register the framework with Mobile Core:

```java
public class MobileApp extends Application {
  @Override
  public void onCreate(){
     super.onCreate();
     MobileCore.setApplication(this);
     try {
        Identity.registerExtension();
     } catch (Exception e) {
       //Log the exception
       }
    }
 }
```
{% endtab %}

{% tab title="iOS" %}
Add the Identity framework to your project:

#### Objective-C

```objectivec
#import "ACPIdentity.h"
```

#### Swift

```swift
import ACPCore
```

Register the Identity framework with Mobile Core

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplicationLaunchOptionsKey: Any]?) -> Bool {
  ACPIdentity.registerExtension()
  return true
}
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

Import the Identity extension

```jsx
import {ACPIdentity} from '@adobe/react-native-acpcore';
```

Get the extension version \(optional\)

```jsx
ACPIdentity.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPIdentity version: " + version));
```

Register the extension with Core

```jsx
ACPIdentity.registerExtension();
```
{% endtab %}
{% endtabs %}

After successful configuration, an Experience Cloud identifier is generated and included on every network hit that is sent to Adobe solutions. Other automatically generated and custom synced identifiers are also sent with each hit.


## Watch the Video

{% embed url="https://www.youtube.com/watch?v=K99NwR6Y08E" caption="Video: How to use Cocoapods and Gradle with SDK extensions & dependencies" %}

## Additional Information

* [How to use Gradle for Android](https://docs.gradle.org/current/userguide/userguide.html)
* [How to use CocoaPods for iOS ](https://guides.cocoapods.org/using/using-cocoapods)
* [Current SDK Versions](../resources/frequently-asked-questions/current-sdk-versions.md)

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html) for immediate assistance

