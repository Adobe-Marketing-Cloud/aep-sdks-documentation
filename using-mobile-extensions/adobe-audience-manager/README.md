# Adobe Audience Manager

Adobe Audience Manager is a versatile audience data management platform. With the SDK, you can update audience profiles for users and retrieve user segment information from your mobile app. For more information, see [Adobe Audience Manager](https://business.adobe.com/products/audience-manager/adobe-audience-manager.html).

## Configuring the Audience Manager extension in Experience Platform Launch

![Adobe Audience Manager Extension Configuration](../../.gitbook/assets/screen-shot-2018-10-04-at-7.51.32-pm-1.png)

1. In Experience Platform Launch, click the **Extensions** tab.
2. Choose **Catalog**, locate the **Adobe Audience Manager** extension, and click **Install**.
3. Type your Audience Manager server.
4. Type a timeout value. This value is the period, in seconds, to wait for a response from Audience Manager before timing out. We recommend a default value of 2s.
5. Click **Save**.
6. Follow the publishing process to update the SDK configuration.

## Add Audience Manager to your app

{% tabs %}
{% tab title="Android" %}
### Java

1. Add the library to your project.
2. Import the library.

```java
import com.adobe.marketing.mobile.*;
```

{% hint style="info" %}
Audience Manager depends on the Identity extension and is automatically included in the Core pod. When manually installing the Audience Manager extension, ensure that you add the `identity-1.x.x.aar` library to your project.
{% endhint %}
{% endtab %}

{% tab title="iOS" %}
1. Add the library to your project via your `Podfile` by adding `pod 'ACPAudience'`
2. Import the Audience and Identity library, using the respective language: 

### Objective-C

```objectivec
  #import "ACPCore.h"
  #import "ACPAudience.h"
  #import "ACPIdentity.h"
```

### Swift

```swift
   import ACPCore
   import ACPAudience
```

{% hint style="info" %}
Audience Manager depends on the Identity extension and is automatically included in the Core pod. When installing the Audience Manager extension manually, ensure that you added the `libACPIdentity_iOS.a` library to your project.
{% endhint %}
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

1. Install Audience Manager in your project.

```jsx
npm install @adobe/react-native-acpaudience
react-native link @adobe/react-native-acpaudience
```

1. Import the extension.

```jsx
import {ACPAudience} from '@adobe/react-native-acpaudience';
```

1. Ensure the extension version is correct.

```jsx
ACPAudience.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPAudience version: " + version));
```
{% endtab %}
{% endtabs %}

## Register Audience Manager with Mobile Core

{% tabs %}
{% tab title="Android" %}
### Java

Call the `setApplication()` method once in the `onCreate()` method of your main activity.

For example, your code might look like the following:

```java
public class AudiencetApp extends Application {

@Override
public void onCreate() {
     super.onCreate();
     MobileCore.setApplication(this);

     try {
         Audience.registerExtension(); //Register Audience Manager with Mobile Core
         Identity.registerExtension();
         MobileCore.start(null);
     } catch (Exception e) {
     //Log the exception
     }
  }
}
```
{% endtab %}

{% tab title="iOS" %}
In your app's `application:didFinishLaunchingWithOptions` function, register the Audience Manager extension with the Mobile Core:

### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
   [ACPIdentity registerExtension];
   [ACPAudience registerExtension];
   [ACPCore start:nil]

   // Override point for customization after application launch.
   return YES;
}
```

### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {  
 ACPIdentity.registerExtension()
 ACPAudience.registerExtension()
 ACPCore.start(nil)

 // Override point for customization after application launch.
 return true;
}
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
import {ACPAudience} from '@adobe/react-native-acpcore';

initSDK() {
    ACPAudience.registerExtension();
}
```
{% endtab %}
{% endtabs %}

## Implement Audience Manager APIs

For more information about implementing Audience Manager APIs, please read the [Audience Manager API reference](audience-manager-api-reference.md).

## Configuration keys

To update SDK configuration programmatically, use the following information to change your Audience Manager configuration values. For more information, see the [Configuration API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| Key | Required | Description | Data Type |
| :--- | :--- | :--- | :--- |
| `audience.server` | Yes | Server endpoint used to collect Audience Manager data | String |
| `audience.timeout` | No | Time, in seconds, to wait for a response from Audience Manager before timing out. Default value is 2 seconds. | Integer |

## Additional information

* How do you find your Audience Manager server?
* Want to know more about setting up Adobe Analytics server-side forwarding to Audience Manager?
  * [Server-side forwarding overview](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/server-side-forwarding/ssf.html)
  * [Set up server-side forwarding with Audience Manager](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics#server-side-forwarding-with-audience-manager) 

