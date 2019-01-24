# Adobe Campaign Classic

## Configure Campaign Classic Extension in Launch

1. In Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Campaign Classic** extension, and click **Install**.
3. Type in the settings for your extension.
4. Click **Save**.
5. Complete the publishing process to update the SDK configuration.

   For more information about publishing, see [Publishing](https://docs.adobelaunch.com/publishing).

### Configure Campaign Classic Extension

![ACC-configure-extension](../../.gitbook/assets/acc-configure-extension.png)

{% hint style="info" %}
Trying to find your ACC registration or tracking endpoint URLs? Contact your program manager.
{% endhint %}

#### Registration Endpoints

Provide registration endpoint URL\(s\) for your Campaign Classic instances. You can specify up to three unique endpoints for your development, staging, and production environments.

{% hint style="warning" %}
For this extension, the registration endpoint URLs should be entered **without** a prefixing `https://.`
{% endhint %}

#### Tracking Endpoints

Provide tracking endpoint URL\(s\) for your Campaign Classic instances. Like the registration URL's, you can specify up to three unique endpoints for your development, staging, and production environments.

{% hint style="warning" %}
For this extension, the tracking endpoint URLs should be entered **without** a prefixing `https://.`
{% endhint %}

#### Integration Key \(iOS\)

You can specify up to three unique iOS integration keys for your development, staging, and production environments. iOS integration keys are generated after creating a service that contains iOS applications using the Adobe Campaign Classic [client console](https://docs.campaign.adobe.com/doc/AC/en/INS_Installing_Campaign_in_Windows__Installing_the_client_console.html). For more information on where to find the integration key, see [Configuring the mobile application in Adobe Campaign](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Configuring_the_mobile_application_in_Adobe_Campaign).

#### Integration Key \(Android\)

Specify up to three unique Android integration keys for your development, staging, and production environments. Similar to iOS, Android integration keys are generated after creating a service that contains Android applications using the Adobe Campaign Classic [client console](https://docs.campaign.adobe.com/doc/AC/en/INS_Installing_Campaign_in_Windows__Installing_the_client_console.html). For more information on where to find the integration key, see [Configuring the mobile application in Adobe Campaign](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Configuring_the_mobile_application_in_Adobe_Campaign).

#### Request Timeout

Time, in seconds, to wait for a response from the registration or tracking endpoint before timing out. The SDK default timeout value is 30 seconds.

## Add Campaign Classic to your app

{% tabs %}
{% tab title="Android" %}
#### Java

1. Add the Campaign Classic extension to your project using the app's Gradle file.
2. Import the CampaignClassic and Lifecycle extensions in your application's main activity.

```java
import com.adobe.marketing.mobile.CampaignClassic;
import com.adobe.marketing.mobile.Lifecycle;
```
{% endtab %}

{% tab title="iOS" %}
1. Add the Campaign Classic and [Mobile Core](../mobile-core/) libraries to your project. You will need to add the following pods to your `Podfile`:

```text
pod 'ACPCampaignClassic', '2.0.0'
pod 'ACPLifecycle', '2.0.0'
pod 'ACPCore', '2.0.0'
```

or you can manually include the [Mobile Core](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/tag/v1.0.1-ACPCore) and [Campaign Classic](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/tag/v1.0.0-ACPCampaignClassic) libraries found in Github.

1. In Xcode project, import Mobile Core and Campaign Classic extensions:

#### Objective-C

```objectivec
#import "ACPCore.h"
#import "ACPCampaignClassic.h"
#import "ACPLifecycle.h"
```

#### Swift

```swift
import ACPCore
import ACPCampaignClassic
import ACPLifecycle
```
{% endtab %}
{% endtabs %}

### Register Campaign Classic with Mobile Core

{% tabs %}
{% tab title="Android" %}
In your App's `OnCreate` method register the Campaign Classic and Lifecycle extensions:

```java
public class CampaignClassicTestApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.VERBOSE);

        try {
            CampaignClassic.registerExtension();
            Lifecycle.registerExtension();
            MobileCore.start(null);
        } catch (Exception e) {
            Log.e("CampaignClassicTestApp", e.getMessage());
        }

    }
}
```
{% endtab %}

{% tab title="iOS" %}
In your App's `application:didFinishLaunchingWithOptions:` method, register the Campaign Classic and Lifecycle extensions:

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCampaignClassic registerExtension];
    [ACPLifecycle registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
   ACPCampaignClassic.registerExtension();
   ACPLifecycle.registerExtension();
  // Override point for customization after application launch.
  return true;
}
```
{% endtab %}
{% endtabs %}

## Configuration Keys

If you need to update SDK configuration programmatically, use the following information to change your Adobe Campaign Classic configuration values. For more information, see [Configuration Methods Reference](../mobile-core/configuration-reference/#update-configuration).

| Key | Required | Description |
| :--- | :--- | :--- |
| build.environment | Yes | Specifies which environment to use \(prod, dev, or staging\) when sending registration and tracking information. It is also used to specify which mobile app integration key to use. |
| campaignclassic.timeout | No | Specifies the amount of time to wait for a response from the Adobe Campaign Classic registration or tracking server. |
| \_\_dev\_\_campaignclassic.marketingServer | No | Sets the development environment marketing server, which receives registration requests. |
| \_\_dev\_\_campaignclassic.trackingServer | No | Sets the development environment tracking server, which receives tracking requests. |
| \_\_dev\_\_campaignclassic.ios.integrationKey | No | Sets the development environment iOS mobile app integration key, which links the app to a specific iOS application campaign on Adobe Campaign Classic. |
| \_\_dev\_\_campaignclassic.android.integrationKey | No | Sets the development environment Android mobile app integration key which links the app to a specific Android application campaign on Adobe Campaign Classic. |
| \_\_stage\_\_campaignclassic.marketingServer | No | Sets the staging environment marketing server, which receives registration requests. |
| \_\_stage\_\_campaignclassic.trackingServer | No | Sets the staging environment tracking server, which receives tracking requests. |
| \_\_stage\_\_campaignclassic.ios.integrationKey | No | Sets the staging environment iOS mobile app integration key, which links the app to a specific iOS application campaign on Adobe Campaign Classic. |
| \_\_stage\_\_campaignclassic.android.integrationKey | No | Sets the staging environment Android mobile app integration key, which links the app to a specific Android application campaign on Adobe Campaign Classic. |
| campaignclassic.marketingServer | Yes | Sets the production environment marketing server, which receives registration requests. |
| campaignclassic.trackingServer | Yes | Sets the production environment tracking server, which receives tracking requests. |
| campaignclassic.ios.integrationKey | Yes | Sets the production environment iOS mobile app integration key, which links the app to a specific iOS application campaign on Adobe Campaign Classic. |
| campaignclassic.android.integrationKey | Yes | Sets the production environment Android mobile app integration key, which links the app to a specific Android application campaign on Adobe Campaign Classic. |

