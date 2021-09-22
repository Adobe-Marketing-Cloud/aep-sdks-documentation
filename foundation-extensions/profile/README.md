# Profile

You can use the Profile extension to store attributes about your user on the client. This information can be used later to target and personalize messages during online or offline scenarios, without having to connect to a server for optimal performance. The Profile extension manages the Client-Side Operation Profile \(CSOP\) and provides a way to react to APIs, updates user profile attributes, and shares the user profile attributes with the rest of the system as a generated event.

The Profile data is used by other extensions to perform profile-related actions. An example is the Rules Engine extension that consumes the profile data and runs rules based on the profile data.

**Important**: The Profile extension does not require any configuration.

To get started with the Profile extension:

1. Configure the Profile Extension in Launch.
2. Add the Profile extension to your app.
3. Implement Profile APIs to:
   * Update user attributes.
   * Remove user attributes.

## Add Profile to your App

To add the Profile extension to your app:

{% tabs %}
{% tab title="Android" %}
### Java

1. Add the `UserProfile` library to your project using the app's gradle file.
2. Import the `UserProfile` library and any other SDK library in your application's main activity.

   ```text
   import com.adobe.marketing.mobile.*;
   ```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
1. Add the UserProfile library to your project via your `Podfile` by adding `pod 'AEPUserProfile'`.
2. Import the UserProfile library.  

### Objective C

```text
  @import AEPUserProfile;
```

### Swift

```swift
   import AEPUserProfile
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### Objective C

1. Add the UserProfile library to your project via your `Podfile` by adding `pod 'ACPUserProfile'`.
2. Import the UserProfile and Identity library.   

```text
   #import "ACPCore.h"
   #import "ACPUserProfile.h"
```

### Swift

```swift
   import ACPCore
   import ACPUserProfile
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

1. After creating your Cordova app and adding the Android and iOS platforms, the User Profile extension for Cordova can be added with this command:

   ```text
   cordova plugin add https://github.com/adobe/cordova-acpuserprofile.git
   ```

2. Get the extension version.

   ```javascript
   ACPUserProfile.extensionVersion(function(version) {  
      console.log("ACPUserProfile version: " + version);
   }, function(error) {  
      console.log(error);  
   });
   ```
{% endtab %}

{% tab title="Flutter" %}
### Flutter

1. After creating your Flutter app and adding the Android and iOS platforms, the User Profile extension for flutter can be added in the `pubspec.yaml`:

   ```yaml
    dependencies:
      flutter_acpcore: ">= 1.0.0"
      flutter_acpuserprofile: ">= 1.0.0"
   ```

Then fetch the packages with:

```bash
flutter pub get
```

1. Get the extension version.

   ```dart
   import 'package:flutter_acpuserprofile/flutter_acpuserprofile.dart';
   String version = FlutterACPUserProfile.extensionVersion;
   ```

### Xamarin

1. After adding the iOS or Android ACPUserProfile NuGet package, the User Profile extension for Xamarin can be added by this import statement:

   ```csharp
   using Com.Adobe.Marketing.Mobile;
   ```

2. Get the extension version.

   ```csharp
   ACPUserProfile.ExtensionVersion();
   ```
{% endtab %}
{% endtabs %}

## Register the extension

{% tabs %}
{% tab title="Android" %}
### Java

**Required:** The `setApplication()` method must be called once in the `onCreate()` method of your main activity.

1. The `UserProfile` extension must be registered with Mobile Core before calling an `UserProfile` API.

   This can be done after calling `setApplication()` in the `onCreate()` method. Here is a code sample, which calls these set up methods:

```java
public class MobileApp extends Application {
​
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
​
        try {
            UserProfile.registerExtension();
        } catch (Exception e) {
            //Log the exception
        }
    }
   }
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Objective C

**Required**: You must complete the following steps in the app before calling other `UserProfile` APIs.

1. In your app's `didFinishLaunchingWithOptions` function register the `UserProfile` extension.

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore registerExtensions:@AEPMobileUserProfile.class] completion:^{
    ...
  }];
  ...
  // Override point for customization after application launch.
  return YES;
}
```

### Swift

```swift
// AppDelegate.swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    MobileCore.registerExtensions([UserProfile.self], {
  })
  ...
}
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### Objective C

**Required**: You must complete the following steps in the app before calling other `UserProfile` APIs.

1. In your app's `didFinishLaunchingWithOptions` function register the `UserProfile` extension.

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPUserProfile registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

When using Cordova, register AEP Assurance with Mobile Core in native code as shown on the Android and iOS tabs.
{% endtab %}

{% tab title="Flutter" %}
### Flutter

When using Flutter, register AEP Assurance with Mobile Core in native code as shown on the Android and iOS tabs.
{% endtab %}

{% tab title="Xamarin" %}
### Xamarin

#### C\#

**iOS**

Register the User Profile extension in your app's `FinishedLaunching()` function:

```csharp
public override bool FinishedLaunching(UIApplication app, NSDictionary options)
{
  global::Xamarin.Forms.Forms.Init();
  LoadApplication(new App());
  ACPUserProfile.RegisterExtension();
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

Register the User Profile extension in your app's `OnCreate()` function:

```csharp
protected override void OnCreate(Bundle savedInstanceState)
{
  base.OnCreate(savedInstanceState);
  global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
  LoadApplication(new App());
  ACPUserProfile.RegisterExtension();

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

