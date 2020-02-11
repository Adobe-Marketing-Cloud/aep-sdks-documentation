# Identity

The Identity framework is bundled with [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/) and enables your app with the ECID. This service helps with the synchronization of Adobe and other customer identifiers.

{% hint style="danger" %}
On web or other platforms, there might situations where this framework might not be required, and the implementation of this SDK framework on mobile apps is required.
{% endhint %}

To get started with Identity, complete the following steps:

1. Add the **Identity** framework to your app.
2. Implement the SDK APIs to complete the following tasks:
   * Update customer IDs.
   * Append Adobe visitor data to a URL string.
   * Return customer IDs.
   * Retrieve Experience Cloud IDs.
   * Set advertising IDs.
   * Set the device notification for push notifications.

## Add the Identity framework to your app

{% tabs %}
{% tab title="Android" %}
#### Java

Import the library:

```java
import com.adobe.marketing.mobile.*;
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

Import the Identity extension:

**Objective-C**

```objectivec
#import  "ACPIdentity.h"
```

**Swift**

In swift, the ACPCore includes ACPIdentity :

```swift
import ACPCore
```
{% endtab %}

{% tab title="React Native" %}
Import the Identity extension:

#### JavaScript

```jsx
import {ACPIdentity} from '@adobe/react-native-acpcore';
```
{% endtab %}
{% endtabs %}

## Register the Identity extension

The `registerExtension()` API registers the Identity extension with the Mobile Core extension. This API allows the extension to send and receive events to and from the Mobile SDK.

To register the Identity extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
After calling the `setApplication()` method in the `onCreate()` method, register the extension. If the registration was not successful, an `InvalidInitException` is thrown.

#### Java

```java
public class MobiletApp extends Application {
@Override
public void onCreate() {
super.onCreate();
     MobileCore.setApplication(this);
     try {
         Identity.registerExtension();
     } catch (Exception e) {
         //Log the exception
     }
  }
}
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

Register the Identity extension in your app's `didFinishLaunchingWithOptions` function:

**Objective-C**

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```

**Swift**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPIdentity.registerExtension();
  // Override point for customization after application launch.
  return true;
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```jsx
import {ACPIdentity} from '@adobe/react-native-acpcore';

initSDK() {
    ACPIdentity.registerExtension();
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Previously known as MCID, the Experience Cloud ID \(ECID\) uniquely identifies each visitor in the Adobe Experience Platform and is a 32-character ID.
{% endhint %}

After the configuration is complete, an ECID is generated and, where applicable, is included on all Analytics and Audience Manager hits. Other IDs, such as custom and automatically-generated IDs, continue to be sent with each hit.

## Version of the Identity extension

The `extensionVersion()` API returns the version of the Identity extension that is registered with the Mobile Core extension.

To get the version of the Identity extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
#### Java

```java
String identityExtensionVersion = Identity.extensionVersion();
```
{% endtab %}

{% tab title="iOS" %}
#### iOS

**Objective-C**

```objectivec
NSString *identityExtensionVersion = [ACPIdentity extensionVersion];
```

**Swift**

```swift
var identityExtensionVersion  = ACPIdentity.extensionVersion()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```jsx
ACPIdentity.extensionVersion().then(identityExtensionVersion => console.log("AdobeExperienceSDK: ACPIdentity version: " + identityExtensionVersion));
```
{% endtab %}
{% endtabs %}

## Visitor tracking between an app and the mobile web

If your app opens mobile web content, you need to ensure that visitors are not identified separately as they move between the native and mobile web.

### Visitor IDs in apps

The Mobile SDK generates a unique visitor ID when the app is installed. This ECID is stored in persistent memory on the mobile device and is sent with every hit. The ECID is removed when the user uninstalls the app or when the user sets the Mobile SDK global privacy status to Opt-out.

{% hint style="info" %}
When the Mobile SDK privacy status is set to Opt-out, and the ECID is removed, a new unique visitor ID \(ECID\) is generated when the user sets the global privacy status to Opt-In.
{% endhint %}

{% hint style="info" %}
App visitor IDs persist through upgrades.
{% endhint %}

### Visitor IDs in the mobile web

Typical mobile web implementations use the same standard analytics `s_code.js` or `AppMeasurement.js` that is used in desktop sites. The JavaScript libraries have their own methods of generating unique visitor IDs, which causes a different visitor ID to be generated when you open mobile web content from your app.

To use the same visitor ID in the app and mobile web and pass the visitor ID to the mobile web in the URL, complete the following steps:

### Implementing visitor tracking between an app and the mobile web

{% tabs %}
{% tab title="Android" %}
#### Java

To append visitor information to the URL that is being used to open the web view, call [appendVisitorInfoForUrl](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#appendToUrl-java):

```java
Identity.appendVisitorInfoForURL("http://myurl.com", new AdobeCallback<String>() {    
    @Override    
    public void call(String urlWithAdobeVisitorInfo) {        
        //handle the new URL here        
        //For example, open the URL on the device browser        
        //        
        Intent i = new Intent(Intent.ACTION_VIEW);        
        i.setData(Uri.parse(urlWithAdobeVisitorInfo));        
        startActivity(i);    
    }
});
```

Alternately, starting in SDK version 1.4.0 \(Identity version 1.1.0\), you can call [getUrlVariables](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#geturlvariables-java) and build your own URL:

```java
Identity.getUrlVariables(new AdobeCallback<String>() {    
    @Override    
    public void call(String stringWithAdobeVisitorInfo) {        
        //handle the URL query parameter string here 
        //For example, open the URL on the device browser        
        //        
        Intent i = new Intent(Intent.ACTION_VIEW);        
        i.setData(Uri.parse("http://myUrl.com?" + urlWithAdobeVisitorInfo));        
        startActivity(i);    
    }
});
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

To append visitor information to the URL that is being used to open the web view, call [appendToUrl](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#appendToUrl-ios):

```objectivec
NSURL* url = [[NSURL alloc] initWithString:@"www.myUrl.com"];
[ACPIdentity appendToUrl:url withCallback:^(NSURL * _Nullable urlWithVisitorData) {    
// handle the appended url here
}];
```

Alternately, starting with SDK version 2.3.0 \(ACPIdentity version 2.1.0\), you can call [getUrlVariables](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#geturlvariables-ios) and build your own URL:

```objectivec
[ACPIdentity getUrlVariables:^(NSString * _Nullable urlVariables) {    
  // handle the URL query parameter string here
  NSString* urlString = @"http://myUrl.com";
  NSString* urlStringWithVisitorData = [NSString stringWithFormat:@"%@?%@", urlString, urlVariables];
  NSURL* urlWithVisitorData = [NSURL URLWithString:urlStringWithVisitorData];
  [[UIApplication sharedApplication] openURL:urlWithVisitorData options:@{} completionHandler:^(BOOL success) {
    // handle openURL success
  }];
}];
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

To append visitor information to the URL that is being used to open the web view, call [appendVisitorInfoForUrl](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#appendToUrl-js):

```java
ACPIdentity.appendVisitorInfoForURL("www.myUrl.com").then(urlWithVistorData => console.log("AdobeExperenceSDK: Url with Visitor Data = " + urlWithVisitorData));
```

Alternately, starting with SDK version 1.0.5, you can call [getUrlVariables](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#geturlvariables-js) and build your own URL:

```java
ACPIdentity.getUrlVariables().then(urlVariables => console.log("AdobeExperenceSDK: query params = " + urlVariables));
```
{% endtab %}
{% endtabs %}

The ID service code on the destination domain extracts the ECID from the URL instead of sending a request to Adobe for a new ID. The ID service code on the destination page uses this ECID to track the visitor. On hits from the mobile web content, verify that the `mid` parameter exists on each hit, and that this value matches the `mid`value that is being sent by the app code.

