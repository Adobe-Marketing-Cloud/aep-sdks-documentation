# Adobe Audience Manager

 Adobe Audience Manager is a versatile audience data management platform. With the SDK, you can update audience profiles for users and retrieve user segment information from your mobile app. For more information, see [Adobe Audience Manager](https://www.adobe.com/analytics/audience-manager.html).

To get started with Audience Manager, complete these steps:

1. Configure the Audience Manager extension in Launch.
2. Add the Audience Manager extension to your app
3. Implement the Audience Manager APIs to:
   1. Get the user profile.
   2. Send signals to Audience Manager.
   3. Reset the Audience Manager identifiers and visitor profiles.

## Configuring the Audience Manager extension in Adobe Launch   <a id="configuring-the-audience-manager-extension-in-adobe-launch"></a>

![Adobe Audience Manager Extension Configuration](../../.gitbook/assets/screen-shot-2018-10-04-at-7.51.32-pm%20%281%29.png)

1. In Launch, click the **Extensions** tab.
2. Choose **Catalog**, locate the **Adobe Audience Manager** extension, and click **Install**.
3. Type your Audience Manager server.
4. Type a timeout value. This value is the period, in seconds, to wait for a response from Audience Manager before timing out. We recommend a default value of 2s.
5. Click **Save**.
6. Follow the publishing process to update the SDK configuration.

### Add Audience Manager to your app

{% tabs %}
{% tab title="Android" %}
1. Add the library to your project.
2. Import the library:

#### Java

`import com.adobe.marketing.mobile.*;`   
  
**Important**: Audience Manager depends on the Identity extension and is automatically included in the Core pod. When manually installing the Audience Manager extension, ensure that you add the `identity-1.x.x.aar` library to your project.
{% endtab %}

{% tab title="iOS" %}
1. Add the library to your project via your `Podfile` by adding `pod 'ACPAudience'`
2. Import the Audience and Identity library:

#### Objective-C

```objectivec
  #import "ACPCore.h"
  #import "ACPAudience.h"
  #import "ACPIdentity.h"
```

#### Swift

```swift
   import ACPCore
   import ACPAudience
```

**Important**: Audience Manager depends on the Identity extension and is automatically included in the Core pod. When installing the Audience Manager extension manually, ensure that you added the `libACPIdentity_iOS.a` library to your project.
{% endtab %}
{% endtabs %}

### Register Audience Manager with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### Java

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

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
   [ACPIdentity registerExtension];
   [ACPAudience registerExtension];
   [ACPCore start:nil]

   // Override point for customization after application launch.
   return YES;
}
```

#### Swift

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
{% endtabs %}

## Implement Audience Manager APIs

For more information about implementing Audience Manager APIs, see [Audience Manager API reference](audience-manager-api-reference.md).

## Configuration keys

To update SDK configuration programmatically, use the following information to change your Audience Manager configuration values. For more information, see [Configuration API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference). 

| Key | Required | Description |
| :--- | :--- | :--- |
| `audience.server` | Yes | Server endpoint used to collect Audience Manager data |
| `audience.timeout` | No | Time, in seconds, to wait for a response from Audience Manager before timing out. Default value is 2 seconds. |

## Additional information

* How to find your Audience Manager server?
* How to set up Adobe Analytics server-side forwarding to Audience Manager?
  * [Server-side forwarding overview](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/server-side-forwarding/ssf.html)
  * Set up [SDK Analytics server-side forwarding](../adobe-analytics/#server-side-forwarding-with-audience-manager)



