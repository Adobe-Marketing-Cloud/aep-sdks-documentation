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

