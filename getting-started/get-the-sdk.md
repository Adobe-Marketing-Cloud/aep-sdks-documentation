# Get the Experience Platform SDK

The Adobe Experience Platform Mobile SDK is available for Apple iOS \(includes iOS and iPadOS\) via [Cocoapods](https://cocoapods.org/) or [Swift Package Manager](https://swift.org/package-manager/) and for Android via [Gradle](https://gradle.org).

{% hint style="info" %}
We recommend integrating our SDKs through supported package and dependency managers for maximized ease of implementation.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
## Java / Kotlin

{% hint style="warning" %}
Adobe Experience Platform SDKs for Android supports Android 4.0 \(API 14\) or later.
{% endhint %}

To get the Adobe Experience Platform Core SDK for Android, follow the instructions below.

### 1. Add dependencies to your project

Each extension needs added as a dependency to the mobile application project. Add the Mobile Core and Profile extensions as dependencies to build.gradle for each extension.

```java
implementation 'com.adobe.marketing.mobile:userprofile:1.+'
implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
```

### 2. Add initialization code

Each extension needs imported and registered in your mobile application project. Besides Mobile Core, all Adobe Experience Platform SDK extensions provide a `registerExtension` API. This API registers the extension with Mobile Core. After an extension is registered, it can dispatch and listen for events. You are required to register each of your extensions before making API calls and failing to do so will lead to undefined behavior.

After you register the extensions, you will want to call the `start` API in Core. This step is required to boot up the SDK for event processing. The following code snippets demonstrate how to import and register the Mobile Core and Profile extensions. You will also see Identity, Lifecycle, Signal, and UserProfile imported and registered. These are part of the Mobile Core extension bundle. You will see that logging is turned on in DEBUG mode. Mobile Core is also configured with the AppID. This is the ID that matches the mobile application with the configuration published in Adobe Platform Launch.

{% hint style="info" %}
To find your Environment ID for an environment, in Experience Platform Launch, go to the **Environments** tab \(found in a previously created and configured mobile property\) and click on the corresponding![](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/7ba2e0893f3f7547f99634df7cba5794434688d4/Users/hardy/.gitbook/assets/screen-shot-2018-10-18-at-11.22.17-am.png)icon. Find the Environment File ID at the top and copy it.
{% endhint %}

Formerly known as Marketing Cloud ID \(MCID\), the Experience Cloud ID \(ECID\) service provides a cross-channel notion of identity across Experience Cloud solutions and is a prerequisite for most implementations. After importing and configuring Identity below, an Experience Cloud identifier is generated and included on every network hit that is sent to Adobe solutions. Other automatically generated and custom synced identifiers are also sent with each hit.

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

### 3. Ensure app permissions

The Android SDK requires standard [network connection](https://developer.android.com/training/basics/network-ops/connecting) permissions in your manifest to send data, collect cellular provider, and record offline tracking calls.

To enable these permissions, add the following lines to your `AndroidManifest.xml` file, located in your app's application project directory:

```markup
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```
{% endtab %}

{% tab title="iOS" %}
## Swift / Objective C

{% hint style="warning" %}
Adobe Experience Platform Mobile SDK for iOS supports **iOS 10 or later.**
{% endhint %}

The Adobe Experience Platform Core SDK for iOS is written in Swift and is open sourced. The documentation and code are available [here](https://github.com/adobe/aepsdk-core-ios).
{% endtab %}
{% endtabs %}

## Additional Information

* [How to use Gradle for Android](https://docs.gradle.org/current/userguide/userguide.html)
* [How to use CocoaPods for iOS ](https://guides.cocoapods.org/using/using-cocoapods)
* [Current SDK Versions](../current-sdk-versions.md)

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html) for immediate assistance

