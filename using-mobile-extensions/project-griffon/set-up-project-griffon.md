# Set up Project Griffon

## **Configure the Project Griffon extension in Launch**

{% hint style="warning" %}
This extension is in beta. Use of this beta product requires acceptance of terms outlined on [https://griffon.adobe.com](https://griffon.adobe.com).
{% endhint %}

1. In Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Project Griffon** extension, and click **Install**.
3. Follow the publishing process to update SDK configuration.

### **Install the Project Griffon Extension**

&lt;screenshot&gt;

Simply click **Install** on the extension card. No extension settings are required.

## Add Project Griffon to your app

{% tabs %}
{% tab title="iOS" %}
1. Add the library to your project via your Cocoapods `Podfile` by adding `pod 'ACPGriffonBeta'` ​ 

2. Import the Project Griffon libraries along with other SDK libraries:

#### Objective-C

```objectivec
#import "ACPCore.h"
#import "ACPAnalytics.h"
#import "ACPGriffonBridge.h" // <-- import the Project Griffon library
```

#### Swift

```swift
import ACPCore
import ACPAnalytics
import ACPGriffonBridge // <-- import the Project Griffon library
```
{% endtab %}
{% endtabs %}

### Register Project Griffon with Mobile Core

{% tabs %}
{% tab title="iOS" %}
Registering the extension with Core will send Experience Platform SDK events to an active Project Griffon session. To start using the extension library, please register the extension with the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core).

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore configureWithAppId:@"yourAppId"];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPGriffonBridge registerExtension]; // <-- register Project Griffon with Core
    [ACPCore start:nil];
    // Override point for customization after application launch.
    return YES;
 }
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
     ACPCore.configure(withAppId: "yourAppId")   
     ACPAnalytics.registerExtension()
     ACPIdentity.registerExtension()
     ACPGriffonBridge.registerExtension() // <-- register Project Griffon with Core
     ACPCore.start(nil)
     // Override point for customization after application launch. 
     return true;
}
```
{% endtab %}
{% endtabs %}

### Start a Project Griffon session

Once the extension has been registered, you may begin a Project Griffon session using the following API.  

{% tabs %}
{% tab title="iOS" %}
### startSession

This API accepts a deep link in order to begin a session. When this API is called, the SDK will display a pin authentication overlay on your app to begin a session.

#### Syntax

```text
+ (void) startSession: (NSURL* _Nonnull) url;
```

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)app openURL:(NSURL *)url option (NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options {
    [ACPGriffonBridge startSession:url];
    return false;
}
```
{% endtab %}
{% endtabs %}

### End a Project Griffon session

Sessions may be ended in the app interface by pressing the floating indicator and selecting _Disconnect_. Alternatively, an active session can be closed, programmatically by using the following API.

{% tabs %}
{% tab title="iOS" %}
### endSession

This API ends the active session and will ensure that no data is sent to a Project Griffon session.

#### Objective-C

```objectivec
[ACPGriffon endSession];
```

#### Swift

```swift
ACPGriffon.endSession()
```
{% endtab %}
{% endtabs %}

