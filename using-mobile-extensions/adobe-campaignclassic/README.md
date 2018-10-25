# Adobe Campaign Classic \(Beta\)

{% hint style="warning" %}
This extension is considered beta functionality and is available only in Launch's [Integration](http://launch-integration.adobe.com) environment.
{% endhint %}

## Configure Campaign Classic Extension in Launch

1. In Launch's Integration environment, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Campaign Classic** extension and click **Install**.
3. Provide extension settings \(see screen capture below\)
4. Click **Save**.
5. Follow the publishing process to update SDK configuration

### Configure Campaign Classic Extension

![ACC-configure-extension](../.gitbook/assets/ACC-configure-extension.png)

{% hint style="info" %}
Trying to find your ACC registration or tracking endpoint URLs? Contact your beta program manager.
{% endhint %}

#### Registration Endpoints

Provide registration endpoint URL\(s\) for your Campaign Classic instances. You may specify up to three unique endpoints for your development, staging, and production environments. 

#### Tracking Endpoints

Provide tracking endpoint URL\(s\) for your Campaign Classic instances. Like the registration URL's, you may specify up to three unique endpoints for your development, staging, and production environments. 

#### Integration Key (iOS)

Specify up to three unique iOS integration keys for your development, staging, and production environments. iOS integration keys are generated after creating a service containing iOS applications using the Adobe Campaign Classic [client console](https://docs.campaign.adobe.com/doc/AC/en/INS_Installation_steps_for_Windows__Installing_the_client_console.html). For more information on where to find the integration key, please see [Configuring the mobile application in Adobe Campaign](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Configuring_the_mobile_application_in_Adobe_Campaign).

#### Integration Key (Android)

Specify up to three unique Android integration keys for your development, staging, and production environments. Similar to iOS, Android integration keys are generated after creating a service containing Android applications using the Adobe Campaign Classic [client console](https://docs.campaign.adobe.com/doc/AC/en/INS_Installation_steps_for_Windows__Installing_the_client_console.html). For more information on where to find the integration key, please see [Configuring the mobile application in Adobe Campaign](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Configuring_the_mobile_application_in_Adobe_Campaign).

#### Request Timeout

Time in seconds to wait for a response from the registration endpoint before timing out.

## Add Campaign Classic to your app

{% tabs %}
{% tab title="Android" %}
Add the **beta** Campaign Classic extension to your project using the app's Gradle file.

#### Java

1. Import the CampaignClassic extension in your application's main activity.

```java
import com.adobe.marketing.mobile.CampaignClassic;
```

{% endtab %}

{% tab title="iOS" %}
{% hint style="warning" %}
This **beta** Campaign Classic extension requires the [Mobile Core](mobile-core/) **beta** extension. If you are using other versions of the Mobile Core library, use the beta version instead, as the instructions below indicate.
{% endhint %}

Add the Campaign Classic and [Mobile Core](mobile-core/) beta libraries to your project. You'll need to add the following pods to your `Podfile`:

```text
pod 'ACPCampaignClassicBeta', '1.0.0beta'
pod 'ACPCoreBeta', '1.0.2beta'
```

or you may manually include the [Mobile Core](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/tag/v1.0.2beta-ACPCore) and [Campaign Classic](update to campaign classic beta location) beta extensions found in Github.

In Xcode, import the Mobile Core beta and Campaign Classic beta extensions:

#### Objective-C

```objectivec
#import <ACPCore_iOS/ACPCore_iOS.h>
#import <ACPCampaignClassic_iOS/ACPCampaignClassic_iOS.h>
#import <ACPLifecycle_iOS/ACPLifecycle_iOS.h>
```

#### Swift

```swift
import ACPCore_iOS
import ACPCampaign_iOS
import ACPLifecycle_iOS
```
{% endtab %}
{% endtabs %}

### Register Campaign Classic with Mobile Core

{% tabs %}

{% tab title="Android" %}

In the App's OnCreate method register the Campaign Classic extension:

```java
public class CampaignClassicTestApp extends Application {

	@Override
	public void onCreate() {
		super.onCreate();
		MobileCore.setApplication(this);
		MobileCore.setLogLevel(LoggingMode.VERBOSE);

		try {
			CampaignClassic.registerExtension();
			MobileCore.start(null);
		} catch (Exception e) {
			Log.e("CampaignClassicTestApp", e.getMessage());
		}

	}
}
```

{% endtab %}

{% tab title="iOS" %}
In your app's`application:didFinishLaunchingWithOptions:` method, register the Campaign Classic extension:

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