# Adobe Media Analytics for Audio and Video

## **Configure Media Analytics Extension in Launch**

1. In Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Media Analytics for Audio and Video** extension and click **Install**.
3. Provide extension settings \(see [Configure Media Analytics Extension](./#configure-media-analytics-extension)\)
4. Click **Save**.
5. Follow the publishing process, to update SDK configuration

### **Configure Media Analytics Extension**

![Adobe Media Analytics Extension Configuration](../../.gitbook/assets/ext-ma-configuration.png)

#### **Tracking Server**

{% hint style="info" %}
This is different from your Analytics tracking server.
{% endhint %}

Provide the tracking domain to which all Media heartbeat requests should be made.

#### **Channel**

Channel name property.

{% hint style="tip" %}
In analytics dashboard you can group metrics for all media views that occur within any channel.
{% endhint %}

#### **Online Video Provider**

Name of the online platform through which content gets distributed.

#### **Player Name**

Name of the media player in use (e.g., "AVPlayer", "Native Player", "Custom Player")

#### **Application Version**

The version of the media player app/SDK.

#### **Debug Logging**

Enables or Disables Media SDK logs.

{% hint style="danger" %}
This should be disabled for your production application.
{% endhint %}

### Add Media Analytics to your app

{% hint style="info" %}
This extension requires [Adobe Analytics Extension](../adobe-analytics/README.md) extension. You must also add the analytics extension to your launch property and configure them.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
Add the Analytics extension to your project using the app's Gradle file.

#### Java

1. Import the Media extension in your application's main activity.

```java
import com.adobe.marketing.mobile.*;
```

{% endtab %}

{% tab title="iOS" %}
Add the library to your project via your Cocoapods `Podfile` by adding `pod 'ACPMedia'`

#### Objective-C

```objectivec
#import <ACPMedia_iOS/ACPMedia_iOS.h>
```

#### Swift

```swift
import ACPMedia_iOS
```

{% endtab %}
{% endtabs %}

### Register Media with Mobile Core

{% tabs %}
{% tab title="Android" %}

#### Java

You may do the following after calling the `setApplication()` method in the `onCreate()` method. Here is code sample which calls these setup methods:

```java
public class MobileApp extends Application {

  @Override
  public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);

      try {
          //Register Media with Mobile Core
          Media.registerExtension();
          //Register Dependent extensions
          Analytics.registerExtension();
          Identity.registerExtension();
      } catch (Exception e) {
          //Log the exception
      }
  }
}
```

{% endtab %}

{% tab title="iOS" %}
In your app's`application:didFinishLaunchingWithOptions`, register Analytics with Mobile Core:

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    //Register Media with Mobile Core
    [ACPMedia registerExtension];
    //Register Dependent extensions
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];

    //Override point for customization after application launch.
    return YES;
  }
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    //Register Media with Mobile Core
    ACPMedia.registerExtension();
    //Register Dependent extensions
    ACPAnalytics.registerExtension();
    ACPIdentity.registerExtension();

    //Override point for customization after application launch. 
    return true;
}
```

{% endtab %}
{% endtabs %}

## Configuration Keys

If you need to update SDK configuration, programmatically, please use the following information to change your Analytics configuration values. For more information, [Configuration Methods Reference](../mobile-core/configuration-reference/#update-configuration).

<table>
  <thead>
    <tr>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Required</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">media.trackingServer</td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">See <a href="./#tracking-server">Tracking Server</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">media.channel</td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">See <a href="./#channel">Channel</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">media.ovp</td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">See <a href="./#online-video-provider">Online Video Provider</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">media.playerName</td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">See <a href="./#player-name">Player Name</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">media.appVersion</td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">See <a href="./#application-version">Application Version</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">media.debugLogging</td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">See <a href="./#debug-logging">Debug Logging</a>
      </td>
    </tr>
  </tbody>
</table>