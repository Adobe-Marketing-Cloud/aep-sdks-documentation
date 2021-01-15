# Adobe Analytics Edge

## **Configure the Adobe Experience Platform Edge extension in** Experience Platform **Launch**

1. In Experience Platform Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Experience Platform Edge** extension, and click **Install**.
3. Within the Edge Extension configuration page add your Edge configuration and environment settings. For more information on creating an Edge configuration for use with your mobile app, see [Experience Platform Setup](../../beta/experience-platform-extension/experience-platform-setup). Additionally, Analytics Edge extension setup steps are available in a tutorial at [Enable Analytics in Edge configuration.](../../beta/experience-platform-extension/tutorials/tutorial-5-analytics-edge-extension#enable-analytics-in-edge-configuration)
4. Click **Save**.
5. Publish the latest changes to your **Adobe Experience Platform Launch** configuration and proceed to adding the Analytics Edge extension in your mobile app.

## Add the Analytics Edge extension to your app

{% tabs %}
{% tab title="Android" %}
**Java**

1. Add the Mobile Core, Edge, and Analytics Edge extensions to your project using the app's Gradle file.

   ```java
    implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
    implementation 'com.adobe.marketing.mobile:edge:1.+'
    implementation 'com.adobe.marketing.mobile:analyticsedge:1.+'
   ```

2. Import the AEP SDK extensions in your application's main activity.

   ```java
    import com.adobe.marketing.mobile.*;
   ```
{% endtab %}

{% tab title="iOS" %}
1. Add the Mobile Core, Edge, Identity, and Analytics Edge extensions to your project using Cocoapods.

2. Add the following pods in your `Podfile`:

   ```ruby
    pod 'AEPCore', :git => 'https://github.com/adobe/aepsdk-core-ios.git', :branch => 'main'
    pod 'AEPServices', :git => 'https://github.com/adobe/aepsdk-core-ios.git', :branch => 'main'
    pod 'AEPEdge', :git => 'https://github.com/adobe/aepsdk-edge-ios.git', :branch => 'main'
    pod 'AEPIdentity', :git => 'https://github.com/adobe/aepsdk-core-ios.git', :branch => 'main'
    pod 'AEPAnalyticsEdge', :git => 'https://github.com/adobe/aepsdk-analyticsedge-ios', :branch => 'main' 
   ```

3. Import the Mobile Core, Edge, Identity, Analytics Edge, and AEP Services libraries:

   **Objective-C**

   ```text
    @import AEPCore;
    @import AEPEdge;
    @import AEPIdentity;
    @import AEPAnalyticsEdge;
    @import AEPServices;
   ```

   **Swift**

   ```swift
    import AEPCore
    import AEPEdge
    import AEPIdentity
    import AEPAnalyticsEdge
    import AEPServices
   ```
   {% endtab %}

   {% endtabs %}

### Register Analytics Edge with Mobile Core

{% tabs %}
{% tab title="Android" %}
#### Java

To call the set up methods that call the [setApplication\(\)](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#setapplication) method in the `onCreate()` method:

```java
public class MobileApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.configureWithAppID("yourAppId");
        try {
            Analytics.registerExtension(); //Register Analytics Edge with Mobile Core
            Identity.registerExtension();
            Edge.registerExtension();
            MobileCore.start(null);
        } catch (Exception e) {
            //Log the exception
         }
    }
}
```

**Important**: Analytics Edge depends on the Identity extension and is automatically included in Core by Maven. When manually installing the Analytics Edge extension, ensure that you add the `identity-1.x.x.aar` library to your project.
{% endtab %}

{% tab title="iOS" %}
In your app's`application:didFinishLaunchingWithOptions`, register Analytics Edge with Mobile Core:

#### Objective C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [AEPMobileCore setLogLevel: AEPLogLevelTrace];
    NSArray *extensionsToRegister = @[AEPMobileEdge.class, AEPMobileIdentity.class, AEPMobileAnalytics.class];
    [AEPMobileCore registerExtensions:extensionsToRegister completion:nil];
    // Use the App id assigned to this application via Adobe Experience Platform Launch
    [AEPMobileCore configureWithAppId: @"yourAppId];
    // Override point for customization after application launch.
    return YES;
 }
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
     MobileCore.setLogLevel(.trace)
     MobileCore.registerExtensions([Edge.self, Identity.self, Analytics.self])
     // Use the App id assigned to this application via Adobe Experience Platform Launch
     MobileCore.configureWith(appId: "yourAppId")
     // Override point for customization after application launch.
     return true;
}
```

{% endtab %}
{% endtabs %}

## Send app states and actions to Analytics

To track mobile app states and actions in Adobe Analytics, implement the `trackAction` and `trackState` APIs from the Mobile Core extension. For more information, see [Track app actions](../mobile-core/mobile-core-api-reference.md#track-app-actions) and [Track app states](../mobile-core/mobile-core-api-reference.md#track-app-states-and-views).

{% hint style="info" %}
`trackState` reports the View State as **Page Name**, and state views are reported as **Page View** in Analytics. The value is sent to Analytics by using the page name variable \(`pagename=value`\).

`trackAction` reports the Action as an **event** and does not increment your page views in Analytics. The value is sent to Analytics by using the action variable \(`action=value`\).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

```java
// create a context data dictionary
Map<String, String> additionalContextData = new HashMap<>();
                                          
// add data
additionalContextData.put("exampleCustomKey", "exampleValue");

// send a tracking call - use either a trackAction or TrackState call.
// trackAction example:
MobileCore.trackAction("Action Name", additionalContextData);
// trackState example:
MobileCore.trackState("State Name", additionalContextData);
```
{% endtab %}

{% tab title="iOS" %}
#### Objective C

```objectivec
// create a context data dictionary
NSMutableDictionary *additionalContextData = [NSMutableDictionary dictionary];

// add data
[additionalContextData setObject:@"key" forKey:@"value"];

// send the tracking call - use either a trackAction or trackState call.
// trackAction example:
[AEPMobileCore trackAction:@"Action Name" data:additionalContextData];
// trackState example:
[AEPMobileCore trackState:@"State Name" data:additionalContextData];
```
#### Swift

```swift
// create a context data dictionary
let additionalContextData = ["key":"value"]

// send the tracking call - use either a trackAction or trackState call.
// trackAction example:
MobileCore.track(action: "Action Name", data: additionalContextData)
// trackState example:
MobileCore.track(state: "State Name", data: additionalContextData)
```

{% endtab %}
{% endtabs %}

