# Adobe Analytics - Media Analytics for Audio and Video

{% hint style="warning" %}
This extension requires the [Adobe Analytics for Media](https://docs.adobe.com/content/help/en/media-analytics/using/media-overview.html) add-on SKU. To learn more, contact your Adobe Customer Success Manager.
{% endhint %}

## Configure Media Analytics extension in Experience Platform Launch

1. In Experience Platform Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Media Analytics for Audio and Video** extension, and click **Install**.
3. Type the extension settings.   For more information, see [Configure Media Analytics Extension](./#configure-media-analytics-extension).
4. Click **Save**.
5. Follow the publishing process to update your SDK configuration.

### Configure the Media Analytics extension

{% hint style="info" %}
If you update the Adobe Media Analytics for Audio and Video launch extension to v2.x in your launch property, you must make sure to update and use AEP SDK Media extension v2.0.0 and higher.
{% endhint %}

![Adobe Media Analytics Extension Configuration](../../.gitbook/assets/ext-ma-configuration.png)

To configure the Media Analytics extension, complete the following steps:

1. In **Collection API Server**, Type the name of the media collection API server to which the downloaded media tracking data should be sent. Important: You need to contact your Adobe account representative for this information.
2. In **Channel**, type the channel name property.
3. In **Player name**, type the name of the media player in use \(for example, _AVPlayer_, _Native Player_, or _Custom Player_\).
4. In Application Version, Type the version of the media player application/SDK.

## Add Media Analytics to your app

{% hint style="info" %}
This extension requires the [Adobe Analytics extension](../adobe-analytics/). You must add the Analytics extension to your Launch property and make sure the extension is correctly configured.
{% endhint %}

{% tabs %}
{% tab title="Android" %}

Latest Android SDK versions - [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/core.svg?logo=android&logoColor=white&label=core&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/core)  [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/analytics.svg?logo=android&logoColor=white&label=analytics&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/analytics)  [![Maven Central](https://img.shields.io/maven-central/v/com.adobe.marketing.mobile/media.svg?logo=android&logoColor=white&label=media&style=flat-square)](https://mvnrepository.com/artifact/com.adobe.marketing.mobile/media)


1. Add the Media extension and its dependencies to your project using the app's Gradle file.

   ```text
   implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
   implementation 'com.adobe.marketing.mobile:analytics:1.+'
   implementation 'com.adobe.marketing.mobile:media:2.+'
   ```
You can also manually include the libraries. Get `.aar` libraries from [Github](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/android).

2. Import the Media extension in your application's main activity.

   ```java
   import com.adobe.marketing.mobile.*;
   ```
{% endtab %}

{% tab title="iOS" %}

Latest iOS SDK versions - [![Cocoapods](https://img.shields.io/cocoapods/v/ACPCore.svg?color=orange&label=ACPCore&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPCore)  [![Cocoapods](https://img.shields.io/cocoapods/v/ACPAnalytics.svg?color=orange&label=ACPAnalytics&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPAnalytics)  [![Cocoapods](https://img.shields.io/cocoapods/v/ACPMedia.svg?color=orange&label=ACPMedia&logo=apple&logoColor=white&style=flat-square)](https://cocoapods.org/pods/ACPMedia)

1. To add the Media library and its dependencies to your project, add the following pods to your `Podfile`:

   ```text
   pod 'ACPCore', '~> 2.0'
   pod 'ACPAnalytics', '~> 2.0'
   pod 'ACPMedia', '~> 2.0'
   ```

You can also manually include the libraries. Get `.a` libraries from [Github](https://github.com/Adobe-Marketing-Cloud/acp-sdks/tree/master/iOS).

2. In Xcode project, import Media extension:

   **Objective C**

   ```objectivec
    #import <ACPMedia.h>
   ```

   **Swift**

   ```swift
   import ACPMedia
   ```

{% endtab %}
{% endtabs %}


### Register Media with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### Java

To register media with Mobile Core, call the `setApplication()` method in `onCreate()` and call set up methods, as shown in this sample:

```java
import com.adobe.marketing.mobile.*;

public class MobileApp extends Application {

  @Override
  public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);

      try {
          Media.registerExtension();
          Analytics.registerExtension();
          Identity.registerExtension();
          MobileCore.start(new AdobeCallback () {
              @Override
              public void call(Object o) {
                  MobileCore.configureWithAppID("your-launch-app-id");
              }
          });
      } catch (InvalidInitException e) {

      }
  }
}
```
{% endtab %}

{% tab title="iOS" %}
In your app's `application:didFinishLaunchingWithOptions`, register Media with Mobile Core:

#### Objective-C

```objectivec
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];

    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];

    [ACPCore start:^{

    }];

    return YES;
  }
```

#### Swift

```swift
import ACPCore
import ACPAnalytics
import ACPMedia
import ACPIdentity
import ACPLifecycle

func application(_ application: UIApplication,
                 didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    ACPCore.setLogLevel(.debug)
    ACPCore.configure(withAppId: "your-launch-app-id")

    ACPMedia.registerExtension()
    ACPAnalytics.registerExtension()
    ACPIdentity.registerExtension()

    ACPCore.start {

    }

    return true;
}
```
{% endtab %}
{% endtabs %}

## Configuration keys

To update your SDK configuration programmatically, use the following information to change your Media configuration values. For more information, see [Configuration API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| Key | Required | Description |
| :--- | :--- | :--- |
| `media.collectionServer` | Yes | For more information, see [Collection Server](./#collection-api-server). |
| `media.channel` | No | For more information, see [Channel](./#channel). |
| `media.playerName` | No | For more information, see [Player Name](./#player-name). |
| `media.appVersion` | No | For more information, see [Application Version](./#application-version). |


## Platform Support
| Platform | Support Status |
| :--- | :--- |
| Android | Supported |
| Apple iOS​ | Supported |
| React Native \(iOS & Android\) | Supported |
