# Identity

The Identity extension is bundled with [Mobile Core](../README.md) and enables your app with the Experience Cloud ID (ECID). This service helps with the synchronization of Adobe and other customer identifiers.

{% hint style="danger" %}
On web or other platforms, there might situations where this extension might not be required, and the implementation of this SDK extension on mobile apps is required.
{% endhint %}

To get started with Identity, complete the following steps:

1. Add the **Identity** extension to your app.
2. Implement the SDK APIs to complete the following tasks:
   * Update customer IDs.
   * Append Adobe visitor data to a URL string.
   * Return customer IDs.
   * Retrieve Experience Cloud IDs.
   * Set advertising IDs.
   * Set the device notification for push notifications.

## Add the Identity extension to your app

{% tabs %}
{% tab title="Android" %}

#### Java

Import the library:

```java
import com.adobe.marketing.mobile.*;
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### iOS

Import the Identity extension:

**Swift**

```swift
import AEPCore
import AEPIdentity
```

**Objective-C**

```objectivec
@import AEPCore;
@import AEPIdentity;
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### iOS

Import the Identity extension:

**Swift**

In Swift, the ACPCore includes ACPIdentity :

```swift
import ACPCore
```

**Objective-C**

```objectivec
#import  "ACPIdentity.h"
```

{% endtab %}

{% tab title="React Native" %}
Import the Identity extension:

#### JavaScript

```jsx
import {ACPIdentity} from '@adobe/react-native-acpcore';
```
{% endtab %}

{% tab title="Flutter" %}
Import the Identity extension:

#### Dart

```dart
import 'package:flutter_acpcore/flutter_acpidentity.dart';
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

After creating your Cordova app and adding the Android and iOS platforms, the Identity extension for Cordova can be added with this command:

```text
cordova plugin add https://github.com/adobe/cordova-acpcore.git
```
{% endtab %}

{% tab title="Unity" %}
### C\#

After importing the [ACPCore.unitypackage](https://github.com/adobe/unity-acpcore/blob/master/bin/ACPCore-0.0.1-Unity.zip), the Identity extension for Unity can be added with following code in the MainScript

```csharp
using com.adobe.marketing.mobile;
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

After adding the iOS ACPCore NuGet package or the Android ACPIdentity NuGet package, the Identity extension can be added by this import statement

```csharp
using Com.Adobe.Marketing.Mobile;
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
public class MobileApp extends Application {
@Override
public void onCreate() {
super.onCreate();
     MobileCore.setApplication(this);
     try {         
         Identity.registerExtension();
         // register other extensions
         MobileCore.start(new AdobeCallback () {
             @Override
             public void call(Object o) {
                 MobileCore.configureWithAppID("yourAppId");
             }
         });    
     } catch (Exception e) {
         //Log the exception
     }
  }
}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
#### iOS

Register the Identity extension in your app's `didFinishLaunchingWithOptions` function:

**Swift**

{% hint style="warning" %}
When including both Identity and Identity for Edge Network extensions, register the extensions using their full Swift module names.

```swift
MobileCore.registerExtensions([AEPIdentity.Identity.self, AEPEdgeIdentity.Identity.self, ...], { ... })
```
{% endhint %}

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
     MobileCore.registerExtensions([Identity.self, ...], {
       ...
     })
}
```

**Objective-C**

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
 [AEPMobileCore registerExtensions:@[AEPMobileIdentity.class, ...] completion:^{
   ...
 }];
 return YES;
}
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### iOS

Register the Identity extension in your app's `didFinishLaunchingWithOptions` function:

**Swift**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPIdentity.registerExtension();
  // Override point for customization after application launch.
  return true;
}
```

**Objective-C**

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPIdentity registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

When using React Native, registering Identity with Mobile Core should be done in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Flutter" %}
#### Dart

When using Flutter, registering Identity with Mobile Core should be done in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

When using Cordova, registering Identity with Mobile Core must be done in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Unity" %}
#### C\#

Register the Identity extension in your app's `Start()` function:

```csharp
void Start() {
  ACPIdentity.RegisterExtension();
}
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

**iOS**

Register the Identity extension in your app's `FinishedLaunching()` function:

```csharp
public override bool FinishedLaunching(UIApplication app, NSDictionary options)
{
  global::Xamarin.Forms.Forms.Init();
  LoadApplication(new App());
    ACPIdentity.RegisterExtension();

  // start core
  ACPCore.Start(startCallback);

  return base.FinishedLaunching(app, options);
}

private void startCallback()
{
  // set launch config
  ACPCore.ConfigureWithAppID("yourAppId");
}
```

**Android**

Register the Identity extension in your app's `OnCreate()` function:

```csharp
protected override void OnCreate(Bundle savedInstanceState)
{
  base.OnCreate(savedInstanceState);
  global::Xamarin.Forms.Forms.Init(this, savedInstanceState);
  LoadApplication(new App());

  ACPIdentity.RegisterExtension();

  // start core
  ACPCore.Start(new CoreStartCompletionCallback());
}

class CoreStartCompletionCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object callback)
  {
    // set launch config
    ACPCore.ConfigureWithAppID("yourAppId");
  }
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Previously known as MCID, the Experience Cloud ID (ECID) uniquely identifies each visitor in the Adobe Experience Platform and is a 38-character ID.
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

{% tab title="iOS (AEP 3.x)" %}
#### iOS

**Swift**

```swift
var identityExtensionVersion  = Identity.extensionVersion
```

**Objective-C**

```objectivec
NSString *identityExtensionVersion = [AEPMobileIdentity extensionVersion];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### iOS

**Swift**

```swift
var identityExtensionVersion  = ACPIdentity.extensionVersion()
```

**Objective-C**

```objectivec
NSString *identityExtensionVersion = [ACPIdentity extensionVersion];
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```jsx
ACPIdentity.extensionVersion().then(identityExtensionVersion => console.log("Identity version: " + identityExtensionVersion));
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

```dart
String identityExtensionVersion = await FlutterACPIdentity.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

```jsx
ACPIdentity.extensionVersion(function (handleCallback) {
  console.log("AdobeExperienceSDK: ACPIdentity version: " + handleCallback)
}, function (handleError) {
  console.log("AdobeExperenceSDK: failed to get extension version : " + handleError)
});
```
{% endtab %}

{% tab title="Unity" %}
#### C\#

```csharp
string identityVersion = ACPIdentity.ExtensionVersion();
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

```csharp
string identityVersion = ACPIdentity.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## Visitor tracking between an app and the mobile web

If your app opens mobile web content, you need to ensure that visitors are not identified separately as they move between the native and mobile web.

### Visitor IDs in apps

The Mobile SDK generates a unique visitor ID when the app is installed. This ECID is stored in persistent memory on the mobile device and is sent with every hit. The ECID is removed when the user uninstalls the app or when the user sets the Mobile SDK global privacy status to `optedout`.

{% hint style="info" %}
When the Mobile SDK privacy status is set to `optedout`, and the ECID is removed, a new unique visitor ID (ECID) is generated when the user sets the global privacy status to `optedin`.
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

To append visitor information to the URL that is being used to open the web view, call [appendVisitorInfoForUrl](identity-api-reference.md#appendtourl-appendvisitorinfoforurl):

```java
Identity.appendVisitorInfoForURL("https://example.com", new AdobeCallback<String>() {    
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

Alternately, starting in SDK version 1.4.0 (Identity version 1.1.0), you can call [getUrlVariables](identity-api-reference.md#geturlvariables) and build your own URL:

```java
Identity.getUrlVariables(new AdobeCallback<String>() {    
    @Override    
    public void call(String stringWithAdobeVisitorInfo) {        
        //handle the URL query parameter string here 
        //For example, open the URL on the device browser        
        //        
        Intent i = new Intent(Intent.ACTION_VIEW);        
        i.setData(Uri.parse("https://example.com?" + urlWithAdobeVisitorInfo));        
        startActivity(i);    
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

To append visitor information to the URL that is being used to open the web view, call [appendToUrl](identity-api-reference.md#appendtourl-appendvisitorinfoforurl):

#### Swift

```swift
let url = URL(string: "https://example.com")
Identity.appendTo(url: url) { appendedUrl, error in
    if error != nil {
        // handle error here
    } else {
        // handle appended url here
    }
}
```
#### Objective-C

```objectivec
NSURL *sampleUrl = [NSURL URLWithString:@"https://example.com"];
[AEPMobileIdentity appendToUrl:sampleUrl completion:^(NSURL * _Nullable appendedUrl, NSError *error) {
    if (error != nil) {
        // Handle error here
    } else {
        // Handle appended url here
    }
}];
```

Alternately, you can call [getUrlVariables](identity-api-reference.md#geturlvariables) and build your own URL:

#### Swift

```swift
Identity.getUrlVariables { urlVariables, error in
    if error != nil {
        // handle error here
    } else {
        if let url = URL(string: "https://example.com?\(urlVariables ?? "")") {
            DispatchQueue.main.async {
                UIApplication.shared.open(url)
            }
        }
    }
}
```

#### Objective-C

```objectivec
[AEPMobileIdentity getUrlVariables:^(NSString * _Nullable urlVariables, NSError *error) {
    NSString *sampleURLString = @"https://example.com";
    if (error != nil) {
        // Handle variables being nil
    } else {
        NSString *stringWithData = [NSString stringWithFormat:@"%@?%@", sampleURLString, urlVariables];
        NSURL *appendedUrl = [NSURL URLWithString:stringWithData];
        dispatch_async(dispatch_get_main_queue(), ^{
            [[UIApplication sharedApplication] openURL:appendedUrl options:@{} completionHandler:nil];
        });
    }
}];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
#### Objective-C

To append visitor information to the URL that is being used to open the web view, call [appendToUrl](identity-api-reference.md#appendtourl-appendvisitorinfoforurl):

```objectivec
NSURL* url = [[NSURL alloc] initWithString:@"www.example.com"];
[ACPIdentity appendToUrl:url withCallback:^(NSURL * _Nullable urlWithVisitorData) {    
// handle the appended url here
}];
```

Alternately, starting with SDK version 2.3.0 (ACPIdentity version 2.1.0), you can call [getUrlVariables](identity-api-reference.md#geturlvariables) and build your own URL:

```objectivec
[ACPIdentity getUrlVariables:^(NSString * _Nullable urlVariables) {    
  // handle the URL query parameter string here
  NSString* urlString = @"https://example.com";
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

To append visitor information to the URL that is being used to open the web view, call [appendVisitorInfoForUrl](identity-api-reference.md#appendtourl-appendvisitorinfoforurl):

```jsx
ACPIdentity.appendVisitorInfoForURL("www.example.com").then(urlWithVistorData => console.log("Url with Visitor Data = " + urlWithVisitorData));
```

Alternately, starting with SDK version 1.0.5, you can call [getUrlVariables](identity-api-reference.md#geturlvariables) and build your own URL:

```jsx
ACPIdentity.getUrlVariables().then(urlVariables => console.log("query params = " + urlVariables));
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

To append visitor information to the URL that is being used to open the web view, call [appendVisitorInfoForUrl](identity-api-reference.md#appendtourl-appendvisitorinfoforurl):

```dart
String result = "";

try {
  result = await FlutterACPIdentity.appendToUrl("www.example.com");
} on PlatformException {
  log("Failed to append URL");
}
```

Alternately, starting with SDK version 1.0.0-beta.1, you can call [getUrlVariables](identity-api-reference.md#geturlvariables) and build your own URL:

```dart
String result = "";

try {
  result = await FlutterACPIdentity.urlVariables;
} on PlatformException {
  log("Failed to get url variables");
}
```
{% endtab %}

{% tab title="Cordova" %}
#### Cordova

To append visitor information to the URL that is being used to open the web view, call [appendVisitorInfoForUrl](identity-api-reference.md#appendtourl-appendvisitorinfoforurl):

```jsx
ACPIdentity.appendVisitorInfoForUrl("https://example.com", function(handleCallback) {
  console.log("AdobeExperenceSDK: Url with Visitor Data = " + handleCallback);
}, function(handleError) {
  console.log("AdobeExperenceSDK: Failed to append URL : " + handleError);
});
```

Alternately, you can call [getUrlVariables](identity-api-reference.md#geturlvariables) and build your own URL:

```jsx
ACPIdentity.getUrlVariables(function (handleCallback) {
  console.log("AdobeExperienceSDK: Url variables: " + handleCallback);
}, function (handleError) {
  console.log("AdobeExperenceSDK: Failed to retrieve url variables : " + handleError);
});
```
{% endtab %}

{% tab title="Unity" %}
#### C\#

To append visitor information to the URL that is being used to open the web view, call [AppendToUrl](identity-api-reference.md#appendtourl-appendvisitorinfoforurl):

```csharp
[MonoPInvokeCallback(typeof(AdobeIdentityAppendToUrlCallback))]
public static void HandleAdobeIdentityAppendToUrlCallback(string url)
{
    print("Url is : " + url);
}
ACPIdentity.AppendToUrl("https://www.adobe.com", HandleAdobeIdentityAppendToUrlCallback);
```

Alternately, you can call [GetUrlVariables](identity-api-reference.md#geturlvariables) and build your own URL:

```csharp
[MonoPInvokeCallback(typeof(AdobeGetUrlVariables))]
public static void HandleAdobeGetUrlVariables(string urlVariables)
{
    print("Url variables are : " + urlVariables);
}
ACPIdentity.GetUrlVariables(HandleAdobeGetUrlVariables);
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

To append visitor information to the URL that is being used to open the web view, call [AppendToUrl](identity-api-reference.md#appendtourl-appendvisitorinfoforurl):

**iOS**

```csharp
ACPIdentity.AppendToUrl(url, callback => {
  Console.WriteLine("Appended url: " + callback);
});
```

To append visitor information to the URL that is being used to open the web view, call [AppendVisitorInfoForUrl](identity-api-reference.md#appendtourl-appendvisitorinfoforurl):

**Android**

```csharp
ACPIdentity.AppendVisitorInfoForURL("https://example.com", new StringCallback());

class StringCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("Appended url: " + stringContent);
    } 
    else 
    {
      Console.WriteLine("null content in string callback");
    }
  }
}
```

Alternately, you can call [GetUrlVariables](identity-api-reference.md#geturlvariables) and build your own URL:

**iOS**

```csharp
ACPIdentity.GetUrlVariables(callback => {
  Console.WriteLine("Url variables: " + callback);
});
```

**Android**

```csharp
ACPIdentity.GetUrlVariables(new StringCallback());

class StringCallback : Java.Lang.Object, IAdobeCallback
{
  public void Call(Java.Lang.Object stringContent)
  {
    if (stringContent != null)
    {
      Console.WriteLine("Url variables: " + stringContent);
    } 
    else 
    {
      Console.WriteLine("null content in string callback");
    }
  }
}
```
{% endtab %}
{% endtabs %}

The ID service code on the destination domain extracts the ECID from the URL instead of sending a request to Adobe for a new ID. The ID service code on the destination page uses this ECID to track the visitor. On hits from the mobile web content, verify that the `mid` parameter exists on each hit, and that this value matches the `mid`value that is being sent by the app code.

