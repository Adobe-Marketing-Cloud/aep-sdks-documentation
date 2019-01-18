# Adobe Audience Manager

[Adobe Audience Manager](https://www.adobe.com/analytics/audience-manager.html) is a versatile audience data management platform. With the SDK, you can update audience profiles for users and retrieve user segment information from your mobile app.

To get started with **Audience Manager**, follow these steps:

1. Configure the **Audience Manager Extension** in **Launch**
2. Add the **Audience Manager Extension** to your app
3. Implement **Audience Manager** APIs to:
   1. Get user profile
   2. Send signals to Audience Manager
   3. Reset Audience Manager identifiers, visitor profiles

## Configuring the Audience Manager Extension in Adobe Launch <a id="configuring-the-audience-manager-extension-in-adobe-launch"></a>

![Adobe Audience Manager Extension Configuration](../../.gitbook/assets/screen-shot-2018-10-04-at-7.51.32-pm%20%281%29.png)

1. In Launch, click the **Extensions** tab.
2. Choose **Catalog**, locate the **Adobe Audience Manager** extension and click **Install**.
3. Provide your Audience Manager server.
4. Provide a timeout value - this value is the amount of time, in seconds, to wait for a response from Audience Manager before timing out. We recommend a default value of 2s.
5. Click **Save**.
6. Follow the publishing process to update SDK configuration.

## Add Audience Manager to your App

{% tabs %}
{% tab title="Android" %}
**Java**

1. Add the library to your project.
2. Import the library:

`import com.adobe.marketing.mobile.*;`
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

1. Add the library to your project via your `Podfile` by adding:

   `pod 'ACPAudience'`

2. Import the Audience and Identity library:

   ```text
    #import "ACPCore.h"
    #import "ACPAudience.h"
    #import "ACPIdentity"
   ```

   **Important**: Audience Manager depends on the Identity extension and is automatically included in the Core pod. When installing manually, ensure that you have also added the `ACPIdentity.framework` to your project.
   {% endtab %}
   {% endtabs %}

### Register Audience Manager with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### **Java**

Call the `setContext()` method once in the `onCreate()` method of your main activity. 

For example, your code may look like:

```java
public class AudiencetApp extends Application {

@Override
public void onCreate() {
     super.onCreate();
     MobileCore.setApplication(this);
     
     try {
         Audience.registerExtension(); //Register Audience Manager w Mobile Core
         Identity.registerExtension();
     } catch (Exception e) {
     //Log the exception
     }
  }
}
```



```java
public class AudienceApp extends Application {​ 
	@Override public void onCreate() {     
		super.onCreate();     
		MobileCore.setApplication(this);​     
		try {         
			Audience.registerExtension();
			Identity.registerExtension();     
		} catch (Exception e) {         
			//Log the exception     
		} 
	}
}
```
{% endtab %}

{% tab title="iOS" %}
#### **Objective-C**

Register the Audience Manager extension with the Mobile Core in your app's `didFinishLaunchingWithOptions` function.

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
   [ACPIdentity registerExtension];
   [ACPAudience registerExtension];
   
   // Override point for customization after application launch.
   return YES;
   
}
```
{% endtab %}
{% endtabs %}

## Implement Audience Manager APIs

See [Audience Manager API Reference](audience-manager-api-reference.md)

## Configuration Keys

If you need to update SDK configuration, programmatically, please use the following information to change your Audience Manager configuration values. For more information, [Configuration Methods Reference](../mobile-core/configuration-reference/#update-configuration).

| Key | Required | Description |
| :--- | :--- | :--- |
| audience.server | Yes | Server endpoint used to collect Audience Manager data |
| audience.timeout | No | Time, in seconds, to wait for a response from Audience Manager before timing out. Default value is 2 seconds. |

## Further Reading

* How to find your Audience Manager server?
* How to setup Adobe Analytics server-side forwarding to Audience Manager?
  * See - [Analytics server-side forwarding](https://marketing.adobe.com/resources/help/en_US/reference/ssf.html)
  * Also see - Setup [SDK Analytics server-side forwarding](../adobe-analytics/#server-side-forwarding-with-audience-manager)

