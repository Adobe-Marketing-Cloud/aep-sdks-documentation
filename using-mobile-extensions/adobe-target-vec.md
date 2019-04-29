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
- func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPTargetVEC.registerExtension()
  ACPTarget.registerExtension()
  
  return true
}
```
{% endtab %}
{% endtabs %}

## Implementation Methods for Target VEC   <a id="implementation-methods-for-target-vec"></a>

### Auto-Fetch Target Activities

#### Fetch in a blocking call (background is OFF)

#### Fetch in an asynchronous mode (background is ON)

### Fetch Target Activities Programmatically

### Handle Target Workspace Restrictions

