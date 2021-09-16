# Adobe Experience Platform Assurance

This extension enables capabilities for [Project Griffon](../../beta/project-griffon/).

{% hint style="info" %}
Project Griffon is a beta product. To use it, you must accept the terms on [https://experience.adobe.com/griffon](https://experience.adobe.com/griffon).
{% endhint %}

To get started with [Project Griffon](../../beta/project-griffon/) in your app, you'll need to:

1. Install the AEP Assurance extension in Experience Platform Launch
2. Add AEP Assurance SDK extension library to your app
   1. Import AEP Assurance into your app
   2. Register and implement extension APIs

## Install the AEP Assurance extension in Experience Platform Launch

Follow these steps to add the install the extension in Experience Platform Launch:

1. In Experience Platform Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **AEP Assurance** extension, and click **Install**.
3. Follow the publishing process to update SDK configuration.

![](../../.gitbook/assets/screen-shot-2020-10-07-at-11.15.47-am.png)

## Add AEPAssurance to your app

### Import the library to your app code

{% tabs %}
{% tab title="Android" %}
**Java**

1. Add the following libraries in your project's `build.gradle` file:

   ```java
   implementation 'com.adobe.marketing.mobile:core:1+'
   implementation 'com.adobe.marketing.mobile:assurance:1+'
   ```

2. Import the Project Griffon libraries with the other SDK libraries:

   ```java
   import com.adobe.marketing.mobile.Assurance; 
   import com.adobe.marketing.mobile.MobileCore;
   ```
{% endtab %}

{% tab title="iOS" %}
Add the library to your project via your [Cocoapods](https://cocoapods.org/pods/AEPAssurance) `Podfile`

```text
pod 'ACPCore'
pod 'AEPAssurance'
```

Import the Project Griffon libraries along with other SDK libraries:

#### Objective-C

```objectivec
#import "ACPCore.h"
#import "AEPAssurance.h" // <-- import the AEPAssurance library
```

#### Swift

```swift
import ACPCore
import AEPAssurance // <-- import the AEPAssurance library
```
{% endtab %}

{% tab title="React Native" %}
#### React Native

1. Install AEP Assurance.

   ```bash
   npm install @adobe/react-native-aepassurance
   ```

   1.1 Link

   * **React Native 0.60+**

[CLI autolink feature](https://github.com/react-native-community/cli/blob/master/docs/autolinking.md) links the module while building the app.

* **React Native &lt;= 0.59**

```bash
   react-native link @adobe/react-native-aepassurance
```

_Note_ For `iOS` using `cocoapods`, run:

```bash
   cd ios/ && pod install
```

1. Import the extension.

   ```jsx
    import {AEPAssurance} from '@adobe/react-native-aepassurance';
   ```

2. Get the extension version.

   ```jsx
    AEPAssurance.extensionVersion().then(version => console.log("AdobeExperienceSDK: AEPAssurance version: " + version));
   ```
{% endtab %}

{% tab title="Flutter" %}
#### Flutter

1. Install AEP Assurance.

   Flutter install instructions for AEP Assurance can be found [here](https://pub.dev/packages/flutter_assurance/install).

2. Import the extension.

   ```dart
   import 'package:flutter_assurance/flutter_assurance.dart';
   ```

3. Get the extension version.

   ```dart
   String version = await FlutterAEPAssurance.extensionVersion;
   ```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

1. After creating your Cordova app and adding the Android and iOS platforms, the AEPAssurance extension for Cordova can be added with this command:

   ```text
   cordova plugin add https://github.com/adobe/cordova-aepassurance.git
   ```

2. Get the extension version.

   ```jsx
   AEPAssurance.extensionVersion(function(version) {  
      console.log("AEPAssurance version: " + version);
   }, function(error) {  
      console.log(error);  
   });
   ```
{% endtab %}

{% tab title="Unity" %}
#### C\#

1. After importing the [AEPAssurance.unitypackage](https://github.com/adobe/unity-aepassurance/tree/master/bin), the AEP Assurance extension for Unity can be added with the following code in the MainScript:

   ```csharp
   using com.adobe.marketing.mobile;
   ```

2. Get the extension version.

   ```csharp
   AEPAssurance.extensionVersion();
   ```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

1. After adding the [iOS](https://www.nuget.org/packages/Adobe.AEPAssurance.iOS/) or [Android](https://www.nuget.org/packages/Adobe.AEPAssurance.Android/) AEP Assurance NuGet package, the Assurance extension can be added by this import statement:

   ```text
   using Com.Adobe.Marketing.Mobile;
   ```

2. Get the extension version.

   ```text
   AEPAssurance.ExtensionVersion();
   ```
{% endtab %}
{% endtabs %}

### Register AEPAssurance with Mobile Core

{% tabs %}
{% tab title="Android" %}
Registering the extension with Core, sends Experience Platform SDK events to an active Project Griffon session. To start using the extension library, you must first register the extension with the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) extension.

#### Java

1. Register the extension when you register other extensions.

   ```java
     public class MobileApp extends Application {
      @Override
      public void onCreate() {
         super.onCreate();
         MobileCore.setApplication(this);
         MobileCore.configureWithAppId("yourAppId");
         try {
            Assurance.registerExtension();
            MobileCore.start(null);
         } catch (Exception e) {
            // Log the exception
         }
      }
     }
   ```
{% endtab %}

{% tab title="iOS" %}
Registering the extension with Core sends Experience Platform SDK events to an active Project Griffon session. To start using the extension library, you must first register the extension with the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) extension.

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore configureWithAppId:@"yourAppId"];
    [AEPAssurance registerExtension]; // <-- register AEPAssurance with Core
    [ACPCore start:nil];
    // Override point for customization after application launch.
    return YES;
 }
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
     ACPCore.configure(withAppId: "yourAppId")   
     AEPAssurance.registerExtension() // <-- register AEPAssurance with Core
     ACPCore.start(nil)
     // Override point for customization after application launch. 
     return true;
}
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

When using React Native, register AEP Assurance with Mobile Core in native code as shown on the Android and iOS tabs.
{% endtab %}

{% tab title="Flutter" %}
### Dart

When using Flutter, register AEP Assurance with Mobile Core in native code as shown on the Android and iOS tabs.
{% endtab %}

{% tab title="Cordova" %}
### Cordova

When using Cordova, register AEP Assurance with Mobile Core in native code as shown on the Android and iOS tabs.
{% endtab %}

{% tab title="Unity" %}
#### C\#

Register the extension in the `start()` function:

```csharp
using com.adobe.marketing.mobile;
using using AOT;

public class MainScript : MonoBehaviour
{
    [MonoPInvokeCallback(typeof(AdobeStartCallback))]
    public static void HandleStartAdobeCallback()
    {   
        ACPCore.ConfigureWithAppID("yourAppId"); 
    }

    // Start is called before the first frame update
    void Start()
    {   
        AEPAssurance.registerExtension();
        ACPCore.Start(HandleStartAdobeCallback);
    }
}
```
{% endtab %}

{% tab title="Xamarin" %}
**iOS**

Register the AEPAssurance extension in your app's `FinishedLaunching()` function:

```csharp
public override bool FinishedLaunching(UIApplication app, NSDictionary options)
{
  global::Xamarin.Forms.Forms.Init();
  LoadApplication(new App());
  AEPAssurance.RegisterExtension();
  // start core
  ACPCore.Start(startCallback);
  return base.FinishedLaunching(app, options);
}

private void startCallback()
{
  // set launch config
  ACPCore.ConfigureWithAppID("yourAppId");
}
```

**Android**

Register the AEPAssurance extension in your app's `OnCreate()` function:

```csharp
protected override void OnCreate(Bundle savedInstanceState)
{
  base.OnCreate(savedInstanceState);
  global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
  LoadApplication(new App());
  AEPAssurance.RegisterExtension();

  // start core
  ACPCore.Start(new CoreStartCompletionCallback());
}

class CoreStartCompletionCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object callback)
  {
    // set launch config
    ACPCore.ConfigureWithAppID("yourAppId");
  }
}
```
{% endtab %}
{% endtabs %}

### Implement AEP Assurance session start APIs (iOS only)

The `startSession` API needs to be called to begin a Project Griffon session. When called, SDK displays a PIN authentication overlay to begin a session.

{% hint style="info" %}
You may call this API when the app launches with a url (see code snippet below for sample usage)
{% endhint %}

{% tabs %}
{% tab title="iOS" %}
### startSession

#### Objective-C

#### Syntax

```objectivec
+ (void) startSession: (NSURL* _Nonnull) url;
```

#### Example

```objectivec
- (BOOL)application:(UIApplication *)app openURL:(nonnull NSURL *)url options:(nonnull NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options {
    [AEPAssurance startSession:url];
    return true;
}
```

In iOS 13 and later, for a scene-based application, use the `UISceneDelegate`'s `scene(_:openURLContexts:)` method as follows:

```objectivec
- (void) scene:(UIScene *)scene openURLContexts:(NSSet<UIOpenURLContext *> *)URLContexts {
    UIOpenURLContext * urlContext = URLContexts.anyObject;
    if (urlContext != nil) {
        [AEPAssurance startSession:urlContext.URL];
    }
}
```

#### Swift

#### Example

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    AEPAssurance.startSession(url)
    return true
}
```

In iOS 13 and later, for a scene-based application, use the `UISceneDelegate`'s `scene(_:openURLContexts:)` method as follows:

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
        AEPAssurance.startSession((URLContexts.first!).url)
}
```
{% endtab %}
{% endtabs %}

