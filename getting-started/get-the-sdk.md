# Get the Experience Platform SDK

The Adobe Experience Platform Mobile SDK is available for Apple iOS \(includes iOS and iPadOS\) via [Cocoapods](https://cocoapods.org/) or [Swift Package Manager](https://swift.org/package-manager/) and for Android via [Gradle](https://gradle.org).

{% hint style="info" %}
We recommend integrating our SDKs through supported package and dependency managers for maximized ease of implementation.
{% endhint %}

## Migration considerations 

Here are a few things to consider when installing the Adobe Experience Platform Edge Network mobile extension.

- The new AEP Edge Network extension requires the usage of the latest AEP SDKs, which for iOS is a new Swift-based SDK. If you are an ACP Mobile SDK user, read  [Adobe Experience Platform Edge Network Migration Considerations](introduction-to-aepedge.md#adobe-experience-platform-edge-network-migration-considerations).
- For the latest information on supported Swift SDK compatible extensions, see [Current SDK Versions](../current-sdk-versions.md).
- The AEP Edge Network extension requires the use of [Identity for Edge Network mobile extension](../using-mobile-extensions/adobe-edge-identity).
- When using the AEP Edge Network extension, it is strongly encouraged to use Consent mobile extension for managing and enforcing the collect consent settings. For more details see [Consent extension](../using-mobile-extensions/adobe-edge-consent) and [Privacy and GDPR](../resources/privacy-and-gdpr.md).

## Install the AEP Mobile SDK extensions

{% tabs %}
{% tab title="Android" %}

## Java

{% hint style="warning" %}
Adobe Experience Platform SDKs for Android supports Android 4.0 \(API 14\) or later (Edge, Identity and Consent extensions support min API 19).
{% endhint %}

To get the Adobe Experience Platform Core SDK for Android, follow the instructions below.

### 1. Add dependencies to your project

Each extension needs added as a dependency to the mobile application project. Add the Mobile Core and Profile extensions as dependencies to build.gradle for each extension.

```java
// Mobile Core and dependents, includes Identity used by Adobe Analytics extension
implementation 'com.adobe.marketing.mobile:sdk-core:1.+'

// Client-side user profile
implementation 'com.adobe.marketing.mobile:userprofile:1.+'

// Edge Network and dependents
implementation 'com.adobe.marketing.mobile:edge:1.+'
implementation 'com.adobe.marketing.mobile:edgeidentity:1.+'
implementation 'com.adobe.marketing.mobile:edgeconsent:1.+'

// Adobe Analytics and dependents
implementation 'com.adobe.marketing.mobile:analytics:1.+'
```

This is just an example, check the full list of supported extensions at [Current SDK Versions](current-sdk-versions.md).

### 2. Add initialization code

Each extension needs imported and registered in your mobile application project. Besides Mobile Core, all Adobe Experience Platform SDK extensions provide a `registerExtension` API. This API registers the extension with Mobile Core. After an extension is registered, it can dispatch and listen for events. You are required to register each of your extensions before making API calls and failing to do so will lead to undefined behavior.

{% hint style="info" %}
To find your Environment ID for an environment, in Experience Platform Launch, go to the **Environments** tab \(found in a previously created and configured mobile property\) and click on the corresponding![](../.gitbook/assets/screen-shot-2018-10-18-at-11.22.17-am.png)icon. Find the Environment File ID at the top and copy it, then replace the string `yourLaunchEnvironmentID` with the copied value.
{% endhint %}

Add the following initialization code. It may need to be adjusted depending on how your application is structured.

```java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.UserProfile;
import com.adobe.marketing.mobile.InvalidInitException;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.edge.consent.Consent;
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
      // Mobile Core and dependents
      Signal.registerExtension();
      Lifecycle.registerExtension();
      
      // Client-side user profile
      UserProfile.registerExtension();

       // Edge Network and dependents
       Edge.registerExtension();
       com.adobe.marketing.mobile.edge.identity.Identity.registerExtension();
       Consent.registerExtension();

       // Adobe Analytics and dependents
       Analytics.registerExtension();
       com.adobe.marketing.mobile.Identity.registerExtension();
       
      MobileCore.start(new AdobeCallback () {
            @Override
            public void call(Object o) {
            MobileCore.configureWithAppID("yourLaunchEnvironmentID");
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

{% hint style="warning" %}
Adobe Experience Platform Mobile SDK for iOS supports **iOS 10 or later.**
{% endhint %}

### 1. (Optional) Existing ACP users

Remove the Adobe pods prefixed with `ACP` from your Podfile so the Swift extensions can be installed in the following steps.

### 2. Add the dependencies to the Podfile

Add the Mobile Core and Edge extensions to your project using Cocoapods. Add following pods in the `Podfile`:

```swift
use_frameworks!
target 'YourTargetApp' do
    // Mobile Core and dependents
    pod 'AEPCore'
    pod 'AEPSignal'
    pod 'AEPLifecycle'

    // Client-side user profile
    pod 'AEPUserProfile'

    // Edge Network and dependents
    pod 'AEPEdge'
    pod 'AEPEdgeIdentity'
    pod 'AEPEdgeConsent'

    // Adobe Analytics and dependents
    pod 'AEPIdentity'
    pod 'AEPAnalytics'
end
```

This is just an example, check the full list of supported Swift SDK compatible extensions at [Current SDK Versions](current-sdk-versions.md). If you use additional extensions than the ones listed at [Current SDK Versions](current-sdk-versions.md), please contact your Adobe Customer Success Manager or account representative.

### 3. Add initialization code

#### Swift

```swift
// AppDelegate.swift

// Mobile Core and dependents
import AEPCore
import AEPSignal
import AEPLifecycle

// Client-side user profile
import AEPUserProfile

// Edge Network and dependents
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent

// Adobe Analytics and dependents
import AEPIdentity
import AEPAnalytics
```

#### Objective-C

```objective-c
// AppDelegate.h

// Mobile Core and dependents
@import AEPCore;
@import AEPSignal;
@import AEPLifecycle;

// Client-side user profile
@import AEPUserProfile;

// Edge Network and dependents
@import AEPEdge;
@import AEPEdgeIdentity;
@import AEPEdgeConsent;

// Adobe Analytics and dependents
@import AEPIdentity;
@import AEPAnalytics;
```

### 4. Add extensions registration code

{% hint style="info" %}

Note that the registration setup changed to a single API call `MobileCore.registerExtensions([...])`. There is no need to call `MobileCore.start` anymore, registerExtensions does that implicitly.
{% endhint %}

#### Swift

```swift
// AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([Signal.self, Lifecycle.self, UserProfile.self, Edge.self, AEPEdgeIdentity.Identity.self, Consent.self, AEPIdentity.Identity.self, Analytics.self], {
        MobileCore.configureWith(appId: "yourLaunchEnvironmentID")
    })
  ...
}
```

#### Objective-C

```objective-c
// AppDelegate.m
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileSignal.class, AEPMobileLifecycle.class, AEPMobileUserProfile.class, AEPMobileEdge.class, AEPMobileEdgeIdentity.class, AEPMobileEdgeConsent.class, AEPMobileIdentity.class, AEPMobileAnalytics.class] completion:^{
    [AEPMobileCore configureWithAppId: @"yourLaunchEnvironmentID"];
  }];
  ...
}
```

{% hint style="info" %}
To find your Environment File ID for an environment, in Experience Platform Launch, go to the **Environments** tab \(found in a previously created and configured mobile property\) and click on the corresponding![](../.gitbook/assets/screen-shot-2018-10-18-at-11.22.17-am.png)icon. Find the Environment File ID at the top and copy it, then replace the string `yourLaunchEnvironmentID` with the copied value.
{% endhint %}

### Partner extensions

If you are using any of the iOS partner extensions from the AEP Launch catalog, please contact your Adobe Customer Success Manager or account representative.

{% endtab %}
{% endtabs %}

## Additional Information

* [How to use Gradle for Android](https://docs.gradle.org/current/userguide/userguide.html)
* [How to use CocoaPods for iOS ](https://guides.cocoapods.org/using/using-cocoapods)
* [Current SDK Versions](../current-sdk-versions.md)

## Get help

* Visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk) to ask questions
* Contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html) for immediate assistance

