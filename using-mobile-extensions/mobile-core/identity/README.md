# Identity

The Identity framework is bundled with [Mobile Core](../) and enables your app with Adobe's Experience Cloud ID service. This service helps with the synchronization of Adobe and other customer identifiers. 

{% hint style="danger" %}
While on web or other platforms, there may be use cases where this framework may not be required, implementation of this SDK framework on mobile apps is required.
{% endhint %}

To get started with Identity, complete the following steps:

1. Add the **Identity** framework to your app
2. Implement SDK APIs to complete the following tasks:
   1. Update customer IDs
   2. Appends Adobe visitor data to a URL string
   3. Return customer IDs
   4. Retrieve Experience Cloud IDs
   5. Set advertising IDs
   6. Set the device notification for push notifications

## Add Identity to your App

{% tabs %}
{% tab title="Android" %}
Import the library**:**

**Java**

```java
import com.adobe.marketing.mobile.*;
```
{% endtab %}

{% tab title="iOS" %}
Import the library:

**Objective-C**

```objectivec
#import  "ACPIdentity.h"
```

#### Swift

In swift, the  ACPCore includes ACPIdentity :

```swift
import ACPCore
```
{% endtab %}
{% endtabs %}

## **Register the Extension**

Here is the code sample to register the Identity extension:

{% tabs %}
{% tab title="Android" %}
#### Java

You may do the following after calling the `setApplication()` method in the `onCreate()` method. Here is code sample which calls these setup methods:

```java
public class MobiletApp extends Application {
@Override
public void onCreate() {
super.onCreate();
     MobileCore.setApplication(this);
     try {
         Identity.registerExtension();
     } catch (Exception e) {
         //Log the exception
     }
  }
}
```
{% endtab %}

{% tab title="iOS" %}
Register Identity extension in your app's `didFinishLaunchingWithOptions` function:

**Objective-C**

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPIdentity.registerExtension();
  // Override point for customization after application launch.
  return true;
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Experience Cloud organization IDs uniquely identify each client company in the Adobe Experience Cloud and are similar to the following value:`016D5C175213CCA80A490D05@AdobeOrg`. The trailing `@AdobeOrg` is required.
{% endhint %}

After the configuration is complete, an Experience Cloud ID will be generated and, where applicable, be included on all Analytics and Audience Manager hits. Other IDs, such as custom and automatically-generated IDs, will continue to be sent with each hit.  


