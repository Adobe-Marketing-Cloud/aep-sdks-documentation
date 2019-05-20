# Identity

The Identity framework is bundled with [Mobile Core](../) and enables your app with Adobe's Experience Cloud ID service. This service helps with the synchronization of Adobe and other customer identifiers.

{% hint style="danger" %}
On web or other platforms, there might situations where this framework might not be required, and the implementation of this SDK framework on mobile apps is required.
{% endhint %}

To get started with Identity, complete the following steps:

1. Add the **Identity** framework to your app.
2. Implement the SDK APIs to complete the following tasks:
   * Update customer IDs.
   * Append Adobe visitor data to a URL string.
   * Return customer IDs.
   * Retrieve Experience Cloud IDs.
   * Set advertising IDs.
   * Set the device notification for push notifications.

## Add Identity to your app

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

### Swift

In swift, the ACPCore includes ACPIdentity :

```swift
import ACPCore
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

Import the Identity extension

```jsx
import {ACPIdentity} from '@adobe/react-native-acpcore';
```

Get the extension version

```jsx
ACPIdentity.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPIdentity version: " + version));
```
{% endtab %}
{% endtabs %}

## **Register the extension**

Here is the code sample to register the Identity extension:

{% tabs %}
{% tab title="Android" %}
### Java

After calling the `setApplication()` method in the `onCreate()` method, register the extension.

Here is a code sample that calls these set up methods:

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

### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPIdentity.registerExtension();
  // Override point for customization after application launch.
  return true;
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```jsx
import {ACPIdentity} from '@adobe/react-native-acpcore';

initSDK() {
    ACPIdentity.registerExtension();
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Previously known as MCID, the Experience Cloud ID or ECID uniquely identifies each client company in the Adobe Experience Cloud and is similar to the following value:`016D5C175213CCA80A490D05@AdobeOrg`. The trailing `@AdobeOrg` is required.
{% endhint %}

After the configuration is complete, an Experience Cloud ID is generated and, where applicable, is included on all Analytics and Audience Manager hits. Other IDs, such as custom and automatically-generated IDs, continue to be sent with each hit.

