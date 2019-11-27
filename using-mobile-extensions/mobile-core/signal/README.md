# Signal

The Signal extension is bundled with the [MobileCore (Android)/ACPCore (iOS)](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/) extension and allows you to send postbacks to third-party endpoints and open URLs, such as web URLs or application deep links, when using rules actions in Adobe Experience Platform Launch. 

By leveraging the same triggers and traits that you use to display an In-App message, you can configure the SDK to send customized data to a third-party destination. Also, with the appropriate permissions and configurations, you can use the `collectPii` API to send PII to a remote server.

To get started with Signal extension, complete the following steps:

1. Add the **Signal** extension to your app.
2. Define the necessary rules in Experience Platform Launch. 
3. (Optional) When using Send PII actions in Experience Platform Launch, implement the APIs to Experience Platform Launchcollect PII data and send it to the configured third-party destination.

For more information about creating and configuring a rule in Experience Platform Launch, see [Rules](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html).

## Add the Signal extension to your app

{% tabs %}
{% tab title="Android" %}

Add the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) extension to your project using the app's Gradle file.

```java
implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
```

#### Java

Import the Signal extension in your application's main activity.

```java
import com.adobe.marketing.mobile.*;
```

{% endtab %}

{% tab title="iOS" %}
​ Add the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) extension to your project using Cocoapods.

Add following pods in your `Podfile`:

```shell
pod 'ACPCore'
```

Import the Signal libraries:

#### Objective-C

```objective-c
#import "ACPCore.h"
#import "ACPSignal.h"
```

#### Swift

```swift
import ACPCore
import ACPSignal
```

{% endtab %}

{% tab title="React Native" %}

#### JavaScript

Install Signal

```jsx
npm install @adobe/react-native-acpcore
react-native link @adobe/react-native-acpcore
```

Importing the Signal extension

```jsx
import {ACPSignal} from '@adobe/react-native-acpcore';
```

Note: if using Cocoapods, run:

```
pod install
```

{% endtab %}
{% endtabs %}

### Register Signal extension

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
        MobileCore.configureWithAppId("yourAppId");
        try {
            Signal.registerExtension(); //Register Signal extension with Mobile Core
            MobileCore.start(null);
        } catch (Exception e) {
            //Log the exception
         }
    }
}
```

**Important**: The Signal extension is automatically included in Core by Maven. When you manually install the Signal extension, ensure that you add the `signal-1.x.x.aar` library to your project.
{% endtab %}

{% tab title="iOS" %}
In your app's`application:didFinishLaunchingWithOptions`, register the Signal extension with Mobile Core:

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore configureWithAppId:@"yourAppId"];
    [ACPSignal registerExtension];
    [ACPCore start:nil];
    // Override point for customization after application launch.
    return YES;
 }
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
     ACPCore.configure(withAppId: "yourAppId")   
     ACPSignal.registerExtension()
     ACPCore.start(nil)
     // Override point for customization after application launch.
     return true;
}
```

**Important**: The Signal extension is automatically included in the Core pod. When you manually install the Signal extension, ensure that you add the `libACPSignal_iOS.a` library to your project.
{% endtab %}

{% tab title="React Native" %}

#### JavaScript

```jsx
import {ACPSignal} from '@adobe/react-native-acpcore';

initSDK() {
    ACPSignal.registerExtension();
}
```

{% endtab %}
{% endtabs %}

##Define rules in Experience Platform Launch

To define the rules in Experience Platform Launch, complete the steps in [Signal extension and Rules Engine integaration](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals/signals-extension-and-rules-engine-integration).

##Implement the Mobile SDK to send PII data to external destinations

To send PII data to external destinations, the `PII` action can trigger the Rules Engine when the configured triggers and traits match. When setting a rule, you can set the `PII` action for a Signal event, so that `collectPii` can trigger the rule and send the `PII` data..

For the information on collectPii and its usage, see collectPii in [AEP Mobile Core API reference Page](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#collect-pii)

For more information on how to configure the Signal postbacks in Adobe Experience Platform Launch refer [signals-extension-and-rules-engine-integration](https://aep-sdks.gitbook.io/docs/resources/user-guides/signals-extension-and-rules-engine-integration).