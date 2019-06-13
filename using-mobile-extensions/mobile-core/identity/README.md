# Identity

The Identity framework is bundled with [Mobile Core](../) and enables your app with Adobe's Experience Cloud ID service. This service helps with the synchronization of Adobe and other customer identifiers.

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

## Add Identity to your app

{% tabs %}
{% tab title="Android" %}
Import the library**:**

**Java**

```java
import com.adobe.marketing.mobile.*;
```
{% endtab %}

{% tab title="iOS" %}
Import the library:

**Objective-C**

```objectivec
#import  "ACPIdentity.h"
```

### Swift

In swift, the ACPCore includes ACPIdentity :

```swift
import ACPCore
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

Import the Identity extension

```jsx
import {ACPIdentity} from '@adobe/react-native-acpcore';
```

Get the extension version

```jsx
ACPIdentity.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPIdentity version: " + version));
```
{% endtab %}
{% endtabs %}

## **Register the extension**

Here is the code sample to register the Identity extension:

{% tabs %}
{% tab title="Android" %}

### Java

After calling the `setApplication()` method in the `onCreate()` method, register the extension.

Here is a code sample that calls these set up methods:

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
Register Identity extension in your app's `didFinishLaunchingWithOptions` function:

**Objective-C**

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```

### Swift

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
Previously known as MCID, the Experience Cloud ID or ECID uniquely identifies each visitor in the Adobe Experience Cloud and is similar to the following value:`65002602839283012066007008864929833047`.
{% endhint %}

After the configuration is complete, an Experience Cloud ID is generated and, where applicable, is included on all Analytics and Audience Manager hits. Other IDs, such as custom and automatically-generated IDs, continue to be sent with each hit.

## Visitor Tracking between an App and Mobile Web

If you app opens mobile web content, you need to ensure that visitors are not identified separately as they move between the native and mobile web.

#### Visitor IDs in Apps

The Mobile SDK generates a unique visitor ID when the app is installed. This Experience Cloud ID (ECID, previously known as MCID) is stored in persistent memory on the mobile device and is sent with every hit. The ECID is removed when the user uninstalles the app or if the user sets the Mobile SDK global privacy status to Opt-Out.

{% hint style="info" %}

When the Mobile SDK privacy status is set to Opt-Out and the ECID is removed, a new unique visitor ID (ECID) is generated when the user sets the global privacy status to Opt-In.

{% endhint %}

{% hint style="info" %}

App visitor IDs persist through upgrades.

{% endhint %}

#### Visitor IDs in the Mobile Web

Typical mobile web implementations use the same standard Analytics `s_code.js` or `AppMeasurement.js` that is used within desktop sites. The JavaScript libraries have their own methods of generating unique visitor IDs, which causes a different vistior ID to be generated when you open mobile web content from your app.

To use the same visitor ID in the app and mobile web, complete the following instructions to pass the visitor ID to the mobile web in the URL.

##### Implementing Visitor Tracking between an App and Mobile Web

{% tabs %}
{% tab title="Android" %}

### Java

To append visitor information to the URL that is being used to open the web view, call [appendVisitorInfoForUrl](./identity-api-reference#appendtourl-java):

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

Alternately, starting with SDK version 1.4.0, you can call [getUrlVariables](./identity-api-reference#geturlvariables-java) and build your own URL:

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

### Objective-C

To append visitor information to the URL that is being used to open the web view, call [appendToUrl](./identity-api-reference#appendtourl-ios):

```objective-c
NSURL* url = [[NSURL alloc] initWithString:@"www.myUrl.com"];
[ACPIdentity appendToUrl:url withCallback:^(NSURL * _Nullable urlWithVisitorData) {    
// handle the appended url here}
}];
```

Alternately, starting with SDK version 2.3.0, you can call [getUrlVariables](./identity-api-reference#geturlvariables-ios) and build your own URL:

```objective-c
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

### JavaScript

To append visitor information to the URL that is being used to open the web view, call [appendVisitorInfoForUrl](./identity-api-reference#appendtourl-js):

```java
ACPIdentity.appendVisitorInfoForURL("www.myUrl.com").then(urlWithVistorData => console.log("AdobeExperenceSDK: Url with Visitor Data = " + urlWithVisitorData));
```

Alternately, starting with SDK version 1.0.5, you can call [getUrlVariables](./identity-api-reference#geturlvariables-js) and build your own URL:

```java
ACPIdentity.getUrlVariables().then(urlVariables => console.log("AdobeExperenceSDK: query params = " + urlVariables));
```

{% endtab %}

{% endtabs %}

The ID service code on the destination domain extracts the ECID from the URL instead of sending a request to Adobe for a new ID. The ID service code on the destination page used the passed-in ECID to track the visitor.

On hits from the mobile web content, verify that the `mid` parameter is present on each hit, and that this value matches the `mid` that is being sent by the app code.

