# Adobe Analytics - Mobile Service

## Configure Adobe Analytics - Mobile Service in Launch {#configuring-the-adobe-mobile-services-extension-in-adobe-launch}

![Adobe Mobile Servcies Extension Configuration](../../.gitbook/assets/mobile-services-launch-settings.png)

1. In Launch, click the **Extensions** tab.
2. On the Installed tab, locate the Adobe Mobile Services extension and click **Configure**.
3. Provide a Acquistion timeout value.
4. Provide the Acquistion app id.
5. Provide the Messages Url for In-app Messages.
6. Click **Save**.
7. Follow the publishing process, to update SDK configuration

## Add Mobile Services Extension to your app

{% tabs %}
{% tab title="Android" %}
#### Java

1. Add the Mobile Services extension to your project using the app's Gradle file.
2. Import the Mobile Services extension in your application's main activity.

   ```java
   import com.adobe.marketing.mobile.*;
   ```
{% endtab %}

{% tab title="iOS" %}
TBD

{% endtab %}
{% endtabs %}

### Register Mobile Services with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### Java

You may do the following after calling the `setApplication()` method in the `onCreate()` method. Here is code sample which calls these setup methods:

```java
public class TestApp extends Application {

 @Override
 public void onCreate() {
     super.onCreate();
     MobileCore.setApplication(this);

     try {
         MobileServices.registerExtension();
         Identity.registerExtension();
     } catch (Exception e) {
         //Log the exception
     }
 }
}
```
{% endtab %}

{% tab title="iOS" %}
TBD
{% endtab %}
{% endtabs %}

## In-App Messages {#integrating-adobe-mobile-services-in-app-messages}

Mobile Services Extension provides the support for the In-App messages defined in the Mobile Servcies UI, enable you to seamlessly migrage to new AEP SDK. 
Simialr with V4 SDK, In-App messages can be triggered off the track action call, track state call, and also lifecyle start call. Follow the migration docs to upgrad the SDK from v4 to v5, and config the Messages Url on Launch, then everything should work the same as in v4.

## Acquisition {#integrating-adobe-mobile-services-acquisition}

Mobile Services Extension supports the tracking of installation, deep link click through, Marketing Link click through, push message click through and also In-App locale notification click through. Analytics request will be sent when valid data is detected, and the data can then be used as traits for In-App messages.




## Configuration Keys

If you need to update SDK configuration, programmatically, please use the following information to change your Target configuration values. For more information, [Configuration Methods Reference](../mobile-core/configuration-reference/#update-configuration).

| Key | Description |
| :--- | :--- |
| mobile.acquisitionTimeout | Timeout value for acquisition, used to determine how long the extension should wait for the reposone of acquistion request. |
| mobile.acquisitionAppId | The app id of the app in Mobilce Services UI, used in the request to the fingerprinter server. |
| mobile.messagesUrl | The remote URL of the In-App messages. |

## Further Reading



