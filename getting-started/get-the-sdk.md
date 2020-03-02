# Get the Experience Platform SDK

The Adobe Experience Platform SDK is available for iOS via [Cocoapods](https://cocoapods.org/), for Android via [Gradle](https://gradle.org), and for React Native projects via [Node Package Manager](https://nodejs.org).

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

1. Open the mobile property you created earlier in Experience Platform Launch.
2. On your mobile property's details page, click on the **Environments** tab.

   The **Environments** tab lists the different environments where you can publish.

3. In the row for the **Development** environment, click on the install package icon \(![](../.gitbook/assets/package.png)\).

   You should see a dialog box similar to the following:

   ![](../.gitbook/assets/android.png)

4. On the **Mobile Install Instructions** dialog box, make sure you are on the **Android** tab.
5. Follow the instructions for using Gradle with Android.

   The necessary dependencies and initialization code can be copied from the dialog box to your mobile application project.

6. For Android, the SDK requires standard network connection permissions in your manifest to send data, collect cellular provider, and record offline tracking calls. To enable these permissions, add the following lines to your AndroidManifest.xml file, located in your app's application project directory:

```markup
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```
{% endtab %}

{% tab title="iOS" %}
### Objective C / Swift

{% hint style="warning" %}
**Important:** Adobe Experience Platform SDKs for iOS supports **iOS 10 or later.**
{% endhint %}

1. Open a previously created and configured **Mobile** property in Launch, and click on the **Environments** tab, and then click on the install package icon  \(![](../.gitbook/assets/package.png)\). 
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

## Installation instructions

If you cannot access the **Mobile Install Instructions** dialog box in Experience Platform Launch, complete the following sections to get the Adobe Experience Platform SDK. If you already completed the steps in the Mobile Install Instructions dialog box, no need to complete these steps.

### 1. Add dependencies to your project

Each extension needs added as a dependency to the mobile application project. The examples below will add the Mobile Core and Profile extensions.

{% tabs %}
{% tab title="Android" %}
#### Android

Add the dependencies to build.gradle for each extension.

```java
implementation 'com.adobe.marketing.mobile:userprofile:1.+'
implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

Add the dependencies to your Podfile for each extension.

```objectivec
use_frameworks!
pod 'ACPUserProfile', '~> 2.0'
pod 'ACPCore', '~> 2.0'
```
{% endtab %}
{% endtabs %}

### 2. Add initialization code

Each extension needs imported and registered in your mobile application project. Besides Mobile Core, all Adobe Experience Platform SDK extensions provide a `registerExtension` API. This API registers the extension with Mobile Core. After an extension is registered, it can dispatch and listen for events. You are required to register each of your extensions before making API calls and failing to do so will lead to undefined behavior.

After you register the extensions, you will want to call the `start` API in Core. This step is required to boot up the SDK for event processing. The following code snippets demonstrate how to import and register the Mobile Core and Profile extensions. You will also see Identity, Lifecycle, Signal, and UserProfile imported and registered. These are part of the Mobile Core extension bundle. You will see that logging is turned on in DEBUG mode. Mobile Core is also configured with the AppID. This is the ID that matches the mobile application with the configuration published in Adobe Platform Launch.

{% hint style="info" %}
To find your Environment ID for an environment, in Experience Platform Launch, go to the **Environments** tab \(found in a previously created and configured mobile property\) and click on the corresponding![](../.gitbook/assets/screen-shot-2018-10-18-at-11.22.17-am.png)icon. Find the Environment File ID at the top and copy it.
{% endhint %}

Formerly known as Marketing Cloud ID \(MCID\), the Experience Cloud ID \(ECID\) service provides a cross-channel notion of identity across Experience Cloud solutions and is a prerequisite for most implementations. After importing and configuring Identity below, an Experience Cloud identifier is generated and included on every network hit that is sent to Adobe solutions. Other automatically generated and custom synced identifiers are also sent with each hit.

{% tabs %}
{% tab title="Android" %}
#### Android

Add the following initialization code. It may need to be adjusted depending on how your application is structured.

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.InvalidInitException;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
...
import android.app.Application;
...
public class MainApp extends Application {
  ...
  @Override
  public void on Create(){
    super.onCreate();
    MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
    ...
    try {
      UserProfile.registerExtension();
            Identity.registerExtension();
            Lifecycle.registerExtension();
            Signal.registerExtension();
            MobileCore.start(new AdobeCallback () {
            @Override
            public void call(Object o) {
            MobileCore.configureWithAppID("<your_environment_id_from_Launch>");
    }
});
    } catch (InvalidInitException e) {
      ...
    }
  }
}
```
{% endtab %}

{% tab title="iOS - Objective C" %}
#### iOS - Objective C

Add the following initialization code. It may need to be adjusted depending on how your application is structured.

```objectivec
#import "AppDelegate.h"
#import "ACPCore.h"
#import "ACPUserProfile.h"
#import "ACPIdentity.h"
#import "ACPLifecycle.h"
#import "ACPSignal.h"
...
@implementation AppDelegate
-(BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPCore setLogLevel:ACPMobileLogLevelDebug];
  [ACPCore configureWithAppId:@"<your_environment_id_from_Launch>"];
    ...
  [ACPUserProfile registerExtension];
    [ACPIdentity registerExtension];
    [ACPLifecycle registerExtension];
    [ACPSignal registerExtension];
    [ACPCore start:^{
      [ACPCore lifecycleStart:nil];
    }];
    ...
  return YES;
}

@end
```
{% endtab %}

{% tab title="iOS - Swift" %}
#### iOS - Swift

Add the following initialization code. It may need to be adjusted depending on how your application is structured.

```swift
import ACPCore
import ACPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
  func application(_application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool{
    ACPCore.setLogLevel(.debug)
        ACPCore.configure(withAppId: "<your_environment_id_from_Launch>")
    ...
    ACPUserProfile.registerExtension()
        ACPIdentity.registerExtension()
        ACPLifecycle.registerExtension()
        ACPSignal.registerExtension()
        ACPCore.start {
        ACPCore.lifecycleStart(nil)
        }
    ...
    return true
  }
}
```
{% endtab %}

{% tab title="React Native" %}
#### Javascript

> Tip: We recommend you initialize the SDK by using native code in your `AppDelegate` and `MainApplication` in iOS and Android, respectively. You can also initialize the SDK in Javascript \([React Native](https://github.com/adobe/react-native-acpcore)\).

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

### 3. Ensure app permissions \(Android-only\)

The SDK requires standard [network connection](https://developer.android.com/training/basics/network-ops/connecting) permissions in your manifest to send data, collect cellular provider, and record offline tracking calls.

To enable these permissions, add the following lines to your `AndroidManifest.xml` file, located in your app's application project directory:

```markup
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### 3. Podfile init, update and install \(iOS-only\)

Create a Podfile if you do not already have one:

```text
pod init
```

If CocoaPods could not find the dependencies, you may need to run this command:

```text
pod repo update
```

Save the Podfile and run the install:

```text
pod install
```

## Watch the Video

{% embed url="https://www.youtube.com/watch?v=K99NwR6Y08E" caption="Video: How to use Cocoapods and Gradle with SDK extensions & dependencies" %}

## Additional Information

* [How to use Gradle for Android](https://docs.gradle.org/current/userguide/userguide.html)
* [How to use CocoaPods for iOS ](https://guides.cocoapods.org/using/using-cocoapods)
* [Current SDK Versions](../resources/upgrading-to-aep/current-sdk-versions.md)

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html) for immediate assistance

