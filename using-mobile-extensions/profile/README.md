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

{% tab title="iOS" %}
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

{% tab title="iOS" %}
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

When using Cordova, registering User Profile with Mobile Core must be done in native code which is shown under the Android and iOS tabs.
{% endtab %}
{% endtabs %}

