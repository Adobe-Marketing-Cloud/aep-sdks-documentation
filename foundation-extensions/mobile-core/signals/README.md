# Signal

The Signal extension allows marketers to send a "signal" to their apps through the Adobe Experience Platform Mobile SDKs. This signal might tell the Mobile SDKs or the apps to complete tasks, such as send PII-labeled data, to trigger a postback to a third-party ad-network and open an app deep link or URL. To ensure that signals are sent or are activated, the marketers need to configure triggers and traits in the Data Collection UI.

The Signal extension is bundled with the [MobileCore (Android)/ACPCore (iOS)](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/) extension and allows you to send postbacks to third-party endpoints and open URLs, such as web URLs or application deep links, when using rules actions in the Data Collection UI.

To send PII data to external destinations, the `PII` action can trigger the Rules Engine when certain triggers and traits match. When setting a rule, you can also set the `PII` action for a Signal event. The `collectPii` API can then be used to trigger the rule and send the PII data to a remote server.

To get started with Signal extension, complete the following steps:

1. Add the **Signal** extension to your app.
2. Define the necessary rules in the Data Collection UI. 
3. (Optional) When using Send PII actions in the Data Collection UI, implement the APIs to collect PII data and send it to the configured third party destination.

For more information about creating and configuring a rule in the Data Collection UI, see [Rules](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/rules.html?lang=en).

## Watch the Video

{% embed url="https://www.youtube.com/watch?v=r-z9ivQjzOY" caption="Video: Sending Postbacks with Adobe Experience Platform Mobile SDKs" %}

## Add the Signal extension to your app

{% tabs %}
{% tab title="Android" %}
#### Java

Add the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) extension to your project using the app's Gradle file.

```java
implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
```

Import the Signal extension in your application's main activity.

```java
import com.adobe.marketing.mobile.*;
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
​Add the AEPSignal extension and it's dependency, the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) extension to your project using Cocoapods.

Add following pods in your `Podfile`:

```pod
pod 'AEPCore','~> 3.0'
pod 'AEPSignal','~> 3.0'
```

Import the Signal libraries:

#### Swift

```swift
import AEPCore
import AEPSignal
```

#### Objective-C

```objectivec
@import AEPCore;
@import AEPSignal;
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
​The Signal extension is included in the Mobile Core extension. Add the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) extension to your project using Cocoapods.

Add following pods in your `Podfile`:

```pod
pod 'ACPCore', '~> 2.0'
```

Import the Signal libraries:

#### Swift

In Swift, the ACPCore includes ACPSignal:

```swift
import ACPCore
```

#### Objective-C

```objectivec
#import "ACPCore.h"
#import "ACPSignal.h"
```

{% endtab %}

{% tab title="React Native" %}
#### JavaScript

Importing the Signal extension:

```jsx
import {ACPSignal} from '@adobe/react-native-acpcore';
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

Importing the Signal extension:

```dart
import 'package:flutter_acpcore/flutter_acpsignal.dart';
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

After creating your Cordova app and adding the Android and iOS platforms, the Signal extension for Cordova can be added with this command:

```text
cordova plugin add https://github.com/adobe/cordova-acpcore.git
```
{% endtab %}

{% tab title="Unity" %}
### C\#

After importing the [ACPCore.unitypackage](https://github.com/adobe/unity-acpcore/blob/master/bin/ACPCore-0.0.1-Unity.zip), the Signal extension for Unity can be added with following code in the MainScript

```csharp
using com.adobe.marketing.mobile;
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

After adding the iOS ACPCore NuGet package or the Android ACPSignal NuGet package, the Signal extension can be added by this import statement

```csharp
using Com.Adobe.Marketing.Mobile;
```
{% endtab %}
{% endtabs %}

### Register the Signal extension

The `registerExtension()` API registers the Signal extension with the Mobile Core extension. This API allows the extension to send and receive events to and from the Mobile SDK.

To register the Identity extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
#### Java

After calling the `setApplication()` method in the `onCreate()` method, register the Signal extension. If the registration was not successful, an `InvalidInitException` is thrown.

```java
public class MobileApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        try {
            Signal.registerExtension();
            // register other extensions
            MobileCore.start(new AdobeCallback () {
                @Override
                public void call(Object o) {
                    MobileCore.configureWithAppID("yourAppId");
                }
            });    
        } catch (Exception e) {
            //Log the exception
         }
    }
}
```

**Important**: The Signal extension is automatically included in the Mobile Core extension by Maven. When you manually install the Signal extension, ensure that you add the `signal-1.x.x.aar` library to your project.
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

In your app's `application:didFinishLaunchingWithOptions`, register the Signal extension with Mobile Core:

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
     MobileCore.registerExtensions([Signal.self, ...]) {
       MobileCore.configureWith(appId: "yourAppId")
       // Any other post registration processing
     }
     return true;
}
```

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@[AEPMobileSignal.class, ...] completion:^{
        [AEPMobileCore configureWithAppId: @"yourAppId"];
        // Any other post registration processing
    }];
    return YES;
 }
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
In your app's`application:didFinishLaunchingWithOptions`, register the Signal extension with Mobile Core:

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
     ACPCore.configure(withAppId: "yourAppId")   
     ACPSignal.registerExtension()
     ACPCore.start(nil)
     // Override point for customization after application launch.
     return true;
}
```

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore configureWithAppId:@"yourAppId"];
    [ACPSignal registerExtension];
    [ACPCore start:nil];
    // Override point for customization after application launch.
    return YES;
 }
```

**Important**: The Signal extension is automatically included in the Mobile Core pod. When you manually install the Signal extension, ensure that you add the `libACPSignal_iOS.a` library to your project.
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

When using React Native, registering Signal with Mobile Core should be done in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Flutter" %}
#### Dart

When using Flutter, registering Signal with Mobile Core should be done in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

When using Cordova, registering Signal with Mobile Core must be done in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Unity" %}
#### C\#

Register the extension in the `start()` function:

```csharp
void Start()
{   
  ACPSignal.RegisterExtension();
}
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

**iOS**

Register the Signal extension with the Mobile Core by adding the following to your app's `FinishedLaunching:` delegate method:

```csharp
public override bool FinishedLaunching(UIApplication app, NSDictionary options)
{
  ACPSignal.RegisterExtension();
  // start Mobile Core
  ACPCore.Start(startCallback);

  return base.FinishedLaunching(app, options);
}

private void startCallback()
{
  // set app id from the Data Collection UI
  ACPCore.ConfigureWithAppID("yourAppId");
}
```

**Android**

Register the Signal extension with the Mobile Core by adding the following to your app's `OnCreate:` method:

```csharp
protected override void OnCreate(Bundle savedInstanceState)
{
  base.OnCreate(savedInstanceState);
    LoadApplication(new App());
  ACPCore.Application = this.Application;
  ACPSignal.RegisterExtension();
  // start Mobile Core
  ACPCore.Start(new CoreStartCompletionCallback());
}

class CoreStartCompletionCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object callback)
  {
  // set app id from the Data Collection UI
    ACPCore.ConfigureWithAppID("yourAppId");
  }
}
```
{% endtab %}
{% endtabs %}

## Implement the Mobile SDK to send PII data to external destinations

To send PII data to external destinations, the `PII` action can trigger the Rules Engine when the configured triggers and traits match. When creating a rule, you can set the `PII` action for a Signal event, so that `collectPii` can trigger the rule and send the `PII` data.

For more information about `collectPii` and its usage, see [collectPii](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#collect-pii).

For more information about how to configure the Signal postbacks in the Data Collection UI, see [Signal extension and Rules Engine integration](../../../resources/user-guides/signal-extension-and-rules-engine-integration).

