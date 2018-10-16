# Profile

You can use the User Profile extension to store attributes about your user on the client. This information can later be used to target and personalize messages during online or offline scenarios, without having to connect to a server for optimal performance. The User Profile extension manages the Client-Side Operation Profile \(CSOP\) and provides a way to react to public APIs, updates user profile attributes, and shares the user profile attributes with the rest of the system as a generated event.

The Profile data is used by other extensions to perform profile-related actions. An example is the Rules Engine extension that consumes the profile data and runs rules based on the profile data.

**Important**: The Profile extension does not require any configuration.

To get started with the Profile extension:

1. Configure the **Profile Extension** in **Launch**.
2. Add the **Profile Extension** to your app.
3. Implement Profile APIs to:
   1. Update user attributes
   2. Remove user attributes

## Add Profile to your App

To add the Profile extension to your app:

{% tabs %}
{% tab title="Android" %}

#### Java

1. Add the UserProfile library to your project using the app's gradle file.
2. Import the UserProfile library \(and any other SDK library\) in your application's main activity.

   ```text
   import com.adobe.marketing.mobile.*;
   ```
{% endtab %}

{% tab title="iOS" %}

#### Objective-C

1. Add the UserProfile library to your project via your `Podfile` by adding `pod 'ACPUserProfile'`.
2. Import the UserProfile and Identity library.   


   ```text
   #import <ACPCore_iOS/ACPCore_iOS.h>#import <ACPUserProfile_iOS/ACPUserProfile_iOS.h>
   ```

#### Swift

 If you are building in Swift, this step is co
{% endtab %}
{% endtabs %}

## Register the Profile Extension

{% tabs %}
{% tab title="Android" %}

#### Java

**Required:** The `setApplication()` method must be called once in the `onCreate()` method of your main activity. For more details, see [Initial Configuration](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/sdk-core/configuration-methods-in-android)

1. The UserProfile extensions must be registered with the SDK core before calling any Target API.

   This may be done after calling the `setApplication()` method in the `onCreate()` method. Here is code sample which calls these setup methods:

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

#### Objective-C


**Required**: You must complete the following steps in the app before calling other UserProfile APIs.

1. In your app's `didFinishLaunchingWithOptions` function register the UserProfile extension.

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPUserProfile registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```

##  {#additional-information}
#### Swift

{% endtab %}
{% endtabs %}

##   {#additional-information}

