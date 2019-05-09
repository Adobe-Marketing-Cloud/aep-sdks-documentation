# Adobe Target - VEC
This extension enables Target VEC (Visual Experience Composer) functionality. The Target VEC for Native Mobile Apps lets you create activities and personalize content on native mobile apps in a do-it-yourself fashion without continuous development dependencies and app-release cycles.

{% hint style="info" %}
Review the following Target VEC functionality documentation for context before implementation at these links:

* [Mobile App Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/composer/mobile-visual-experience-composer.html)
* [Setup Mobile VEC for Android](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/composer/mobile-visual-experience-composer-android.html)
* [Setup Mobile VEC for iOS](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/composer/mobile-visual-experience-composer-ios.html)
* [Set up click tracking in the Mobile VEC](https://docs.adobe.com/content/help/en/target/using/implement-target/mobile-apps/composer/set-up-click-tracking-in-the-mobile-vec.html)
{% endhint %}

To get started with Target VEC, follow these steps:

1. Configure the Adobe Target - VEC extension. The VEC extension is dependent on the Adobe Target Extension. Make sure Adobe Target extension is already configured and enabled.
2. Add the Target VEC Extension to your app
3. Different Implementation Methods for Target VEC
   1. Auto-Fetch Target Activities
      a. Fetch in a blocking call (background is OFF)
      b. Fetch in an asynchronous mode (background is ON)
   2. Fetch Target Activities Programmatically
   3. Handle Target Workspace Restrictions

## Configure the Adobe Target - VEC extension in Launch   <a id="configuring-the-adobe-target-vec-extension-in-adobe-launch"></a>

![Adobe Target VEC Extension Configuration](../.gitbook/assets/adobe-target-vec-1.png)

1. In Launch, click the **Extensions** tab.
2. On the **Installed** tab, locate the Adobe Target VEC extension, and click **Configure**.
3. The default configuration options loads Target VEC activities as a blocking call on App launch. See [Implementation Methods for Target VEC](implementation-methods-for-target-vec) for details.
4. Click **Save**.
5. Follow the publishing process to update SDK configuration

## Add Target VEC to your app

#### Java

1. Add the Target VEC extension to your project using the app's Gradle file.
2. Import the Target VEC extension in your application's main activity.  `import com.adobe.marketing.mobile.*;`
3. Add the Target VEC library to your project via your `Podfile` by adding `pod 'ACPTargetVEC'`

#### Objective-C

Import the Target and Identity library.

```objectivec
   #import "ACPCore.h"
   #import "ACPTargetVEC.h"
   #import "ACPTarget.h"
   #import "ACPIdentity.h"
   #import "ACPTargetRequestObject.h"
   #import "ACPTargetPrefetchObject.h"
```

#### Swift

```swift
   #import ACPCore
   #import ACPTarget
   #import ACPTargetVEC
   #import ACPIdentity
```

### Register Target VEC with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### Java

After calling the `setApplication()` method in the `onCreate()` method, register Target VEC with Mobile Core.

Here is code sample that calls these set up methods:

```java
public class TargetApp extends Application {

 @Override
 public void onCreate() {
     super.onCreate();
     MobileCore.setApplication(this);

     try {
         TargetVEC.registerExtension();
         Target.registerExtension();
         Identity.registerExtension();
     } catch (Exception e) {
         //Log the exception
     }
 }
}
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

1. In your app's `didFinishLaunchingWithOptions` function register the Target VEC extension

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  [ACPTargetVEC registerExtension];
  [ACPTarget registerExtension];

  // Override point for customization after application launch.
  return YES;
}
```

#### Swift
1. In your app's `didFinishLaunchingWithOptions` function register the Target VEC extension

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPTargetVEC.registerExtension()
  ACPTarget.registerExtension()
  
  return true
}
```
{% endtab %}
{% endtabs %}

## Implementation Methods for Target VEC   <a id="implementation-methods-for-target-vec"></a>
The Target VEC extension retrieves the relevant Target experiences for your app through a single network request. Offers are retrieved via this network call and applied automatically on the targeted screens. It should be noted that no network requests are made to retrieve VEC experiences as the user navigates through multiple screens of the app.

The default behavior of the extension is to make a synchronous network request (blocking call) at the time of Application launch. You can use Launch to control the behavior of this network request to meet your application behavior.

### Auto-Fetch Target Activities
This is the default behavior where a network request is initiated automatically by the Target VEC extension. You can use one of the following options to make this request a blocking call or an asynchronous request.

#### Fetch in a synchronous call (background is OFF)
When selected Target VEC extension makes a network request as a blocking call on App launch. Offers are applied immediately and there is no flicker in the app. This is the default behavior of the extension.

#### Fetch in an asynchronous call (background is ON)
When selected Target VEC extension makes a network request in the background on App launch, but does not block the app from loading. If you have experiences authored on the home screen of your app, this will cause flicker as the offers may not always be available before the app screen is rendered.

### Fetch Target Activities Programmatically
You can disable the Target VEC extension to make the network request automatically and decide to programmatically call the Extension API. This gives your developers control on how they want to integrate Target VEC offers in the App. The Target VEC extension has two static methods `prefetchOffers` and `prefetchOffersBackground` that can used to programmatically retrieve Target VEC offers.
1. `prefetchOffers` method will hide the current screen until Target VEC offers are fetched. The offers are automatically applied to the current screen if applicable and the screen is visible again.
2. `prefetchOffersBackground` method will not hide the current screen and a call will be made to retrieve the relevant Target offers. Target offers will *not* be applied on the current screen and there will not be a flicker. As the user navigates to subsequent screens, offers will be automatically applied as applicable.

### Handle Target Workspace Restrictions
You can set the `at_property` value for your workspace using the Launch interface. This ensures only activities in that workspace will be delivered to your Mobile App.
