# Audience Manager API reference

## extensionVersion

The `extensionVersion()` API returns the version of the Audience extension that is registered with the Mobile Core extension.

To get the version of the Audience extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}

#### Java

```java
String audienceExtensionVersion = Audience.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

**Swift**

```swift
let audienceExtensionVersion  = Audience.extensionVersion()
```

**Objective-C**

```objective-c
NSString *audienceExtensionVersion = [AEPMobileAudience extensionVersion];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Objective-C**

```objective-c
NSString *audienceExtensionVersion = [ACPAudience extensionVersion];
```

**Swift**

```swift
let audienceExtensionVersion  = ACPAudience.extensionVersion()
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPAudience.extensionVersion().then(audienceExtensionVersion => console.log("AdobeExperienceSDK: ACPAudience version: " + audienceExtensionVersion));
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

```dart
String audienceExtensionVersion = await FlutterACPAudience.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

```jsx
ACPAudience.extensionVersion(function(version) {  
   console.log("ACPAudience version: " + version);
}, function(error) {  
   console.log(error);  
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

```csharp
string audienceExtensionVersion = ACPAudience.ExtensionVersion();
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

```csharp
string audienceExtensionVersion = ACPAudience.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## getVisitorProfile

Returns the visitor profile that was most recently updated. The visitor profile is saved in the SDK's local storage for access across multiple launches of your app. If no audience signal has been sent before, when this API is called, a null value is returned.

{% tabs %}
{% tab title="Android" %}
### getVisitorProfile

This API returns the visitor profile that was most recently obtained. For easy access across multiple launches of your app, the visitor profile is saved in `SharedPreferences`. If no signal has been submitted, null is returned.

When an AdobeCallbackWithError is provided, an AdobeError can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with the visitor profile.

#### Syntax

```java
public static void getVisitorProfile(final AdobeCallback<Map<String, String>> adobeCallback)
```

#### Example

```java
AdobeCallback<Map<String, String>> visitorProfileCallback = new AdobeCallback<Map<String, String>>() {
    @Override
    public void call(final Map<String, String> visitorProfile) {
        // your own customized code
    }
};

Audience.getVisitorProfile(visitorProfileCallback);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### getVisitorProfile

This API returns the visitor profile that was most recently obtained. 

#### Syntax

```swift
static func getVisitorProfile(completion: @escaping ([String: String]?, Error?) -> Void)
```

#### Example

**Swift**

```swift
Audience.getVisitorProfile { (visitorProfile, error) in
   if error != nil {
    // handle the error here
   } else {
    // handle the retrieved visitorProfile here
   }
  }
```

**Objective-C**

```objective-c
[AEPMobileAudience getVisitorProfile:^(NSDictionary<NSString *,NSString *> * _Nullable visitorProfile, NSError * _Nullable error) {
   if (error) {
    // handle the error here
   } else {
    // handle the returned visitorProfile dictionary here
   }
}];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### getVisitorProfile

{% hint style="info" %}
Method `getVisitorProfileWithCompletionHandler` was added in ACPAudience version 2.1.0.
{% endhint %}

This API returns the visitor profile that was most recently obtained. For easy access across multiple launches of your app, the visitor profile is saved in `NSUserDefaults`. If no signal has been submitted, nil is returned.

#### Syntax

```objective-c
+ (void) getVisitorProfile: (nonnull void (^) (NSDictionary* __nullable visitorProfile)) callback;

+ (void) getVisitorProfileWithCompletionHandler: (nonnull void (^) (NSDictionary* __nullable visitorProfile, NSError* __nullable error)) completionHandler;
```

#### Example

**Objective-C**

```objective-c
[ACPAudience getVisitorProfile:^(NSDictionary* visitorProfile){
  // handle the visitorProfile here
}];

[ACPAudience getVisitorProfileWithCompletionHandler:^(NSDictionary * _Nullable visitorProfile, NSError * _Nullable error) {
  if (error) {
    // handle error here
  } else {
    // handle the returned visitorProfile here
  }
}];
```

**Swift**

```swift
ACPAudience.getVisitorProfile { (visitorProfile) in
  // handle the visitorProfile here
}

ACPAudience.getVisitorProfile { (visitorProfile, error) in
  if let error = error {
    // handle error here
  } else {
    // handle the returned visitorProfile here
  }
}
```
{% endtab %}

{% tab title="React Native" %}
**JavaScript**

### getVisitorProfile

```jsx
ACPAudience.getVisitorProfile().then(profile => console.log("AdobeExperienceSDK: Visitor Profile: " + profile));
```
{% endtab %}
{% endtabs %}

## registerExtension

This API registers an extension class that was derived from `ACPExtension` with a unique name. This call validates the parameters to ensure that the name is not empty, the name is unique, and that the parent class is ACPExtension.

{% tabs %}
{% tab title="Android" %}
### registerExtension

#### Syntax

```java
public  static void registerExtension() throws InvalidInitException
```

#### Example

```java
Audience.registerExtension();
```
{% endtab %}

{% tab title="iOS" %}
### registerExtension

#### Syntax

```objective-c
+ (BOOL) registerExtension: (nonnull Class) extensionClass
                     error: (NSError* _Nullable* _Nullable) error;
```

#### **Examples**

**Objective-C**

```objective-c
[ACPAudience registerExtension];
```

**Swift**

```swift
ACPAudience.registerExtension()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### registerExtension

```jsx
ACPAudience.registerExtension();
```
{% endtab %}
{% endtabs %}

## reset

This API helps you reset the Audience Manager UUID and purges the current visitor profile.

{% hint style="info" %}
For more information about the UUID, the DPID, the DPUUID and other Audience Manager identifiers, see [Index of IDs in Audience Manager](https://marketing.adobe.com/resources/help/en_US/aam/ids-in-aam.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### reset

This API resets the Audience Manager UUID and purges the current visitor profile from `android.content.SharedPreferences`. The Audience reset also clears the current in-memory DPID and DPUUID variables.

#### Syntax

```java
public static void reset()
```

#### Example

```java
Audience.reset();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### reset

This API resets the Audience Manager UUID and purges the current visitor profile from `UserDefaults`. The Audience reset also clears the current in-memory DPID and DPUUID variables.

#### Syntax

```swift
static func reset()
```

#### Examples

**Swift**

```swift
Audience.reset()
```

**Objective-C**

```objective-c
[AEPMobileAudience reset];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### reset

This API resets the Audience Manager UUID and purges the current visitor profile from `UserDefaults`. The Audience reset also clears the current in-memory DPID and DPUUID variables.

#### Syntax

```objective-c
+ (void) reset;
```

#### Examples

**Objective-C**

```objective-c
[ACPAudience reset];
```

**Swift**

```swift
ACPAudience.reset()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### reset

```jsx
ACPAudience.reset();
```
{% endtab %}
{% endtabs %}

## signalWithData

Use this method to send a signal with traits to Audience Manager and get the matching segments returned in a block callback. Audience manager sends the UUID in response to an initial signal call. The UUID is persisted on local SDK storage and is sent by the SDK to Audience Manager in all subsequent signal requests.

If you are using the Experience Cloud ID \(ECID\) Service (formerly MCID), the ECID and other custom identifiers for the same visitor are sent with each signal request. The visitor profile that is returned by Audience Manager is saved in SDK local storage and is updated with subsequent signal calls.

{% hint style="info" %}
For more information about the UUID and other Audience Manager identifiers, see [Index of IDs in Audience Manager](https://marketing.adobe.com/resources/help/en_US/aam/ids-in-aam.html).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### signalWithData

This API sends Audience Manager a signal with traits and returns the matching segments for the visitor in a callback.

Audience Manager sends the AAM UUID in response in initial signal call. The AAM UUID is persisted in `SharedPreferences` and is sent by the SDK in all subsequent signal requests. If available, the ECID is also sent in each signal request with the DPID and the DPUUID. The visitor profile that Audience Manager returns is saved in `SharedPreferences` and is updated with every signal call.

When an AdobeCallbackWithError is provided, an AdobeError can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with the visitor profile.

#### Syntax

```java
public static void signalWithData(final Map<String, String> data, final AdobeCallback<Map<String, String>> callback)
```

* `data` is the traits data for the current visitor.
* `callback` is the void method that is invoked with the visitor's profile as a parameter.

#### Example

```java
AdobeCallback<Map<String, String>> visitorProfileCallback = new AdobeCallback<Map<String, String>>() {
    @Override
    public void call(final Map<String, String> visitorProfile) {
        // handle the returned visitorProfile here
    }
};
​
Map<String, String> traits = new HashMap<String, String>();
traits.put("trait", "xyz");
Audience.signalWithData(traits, visitorProfileCallback);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### signalWithData

This API sends Audience Manager a signal with traits and returns the matching segments for the visitor in a closure.

Audience Manager sends the AAM UUID in response in initial signal call. The AAM UUID is persisted in `NSUserDefaults` and is sent by the SDK in all subsequent signal requests. If available, the Experience Cloud ID (MID) is also sent in each signal request with the DPID and the DPUUID. The visitor profile that Audience Manager returns is saved in `NSUserDefaults` and is updated with every signal call.

#### Syntax

```swift
static func signalWithData(data: [String: String], completion: @escaping ([String: String]?, Error?) -> Void) 
```

* `data` is the traits data for the current visitor.
* `callback` is the void method that is invoked with the visitor's profile as a parameter.

#### Example

**Swift**

```swift
Audience.signalWithData(data: ["trait": "trait value"]) { (traits, error) in
  if error != nil {
     // handle the error here
     } else {
     // handle the returned visitorProfile here
     }
}
```

{% endtab %}

**Objective-C**

```objective-c
NSDictionary *traits = @{@"key1":@"value1",@"key2":@"value2"};
[AEPMobileAudience signalWithData:traits completion:^(NSDictionary<NSString *,NSString *> * _Nullable visitorProfile, NSError* _Nullable error) {
  if (error) {
     // handle the error here
     } else {
     // handle the returned visitorProfile dictionary here
     }
}];
```

{% tab title="iOS (ACP 2.x)" %}
### signalWithData

{% hint style="info" %}
Method `signalWithData:withCompletionHandler` was added in ACPAudience version 2.1.0.
{% endhint %}

This API sends Audience Manager a signal with traits and returns the matching segments for the visitor in a callback.

Audience Manager sends the AAM UUID in response in initial signal call. The AAM UUID is persisted in `NSUserDefaults` and is sent by the SDK in all subsequent signal requests. If available, the Experience Cloud ID (MID) is also sent in each signal request with the DPID and the DPUUID. The visitor profile that Audience Manager returns is saved in `NSUserDefaults` and is updated with every signal call.

#### Syntax

```objective-c
+ (void) signalWithData: (NSDictionary<NSString*, NSString*>* __nullable) data
                       callback: (nullable void (^) (NSDictionary* __nullable visitorProfile)) callback;

+ (void) signalWithData: (NSDictionary<NSString*, NSString*>* __nullable) data
                        withCompletionHandler:: (nullable void (^) (NSDictionary* __nullable visitorProfile, NSError* __nullable error)) completionHandler;
```

* `data` is the traits data for the current visitor.
* `callback` is the void method that is invoked with the visitor's profile as a parameter.

#### Example

**Objective-C**

```objective-c
NSDictionary *traits = @{@"key1":@"value1",@"key2":@"value2"};
[ACPAudience signalWithData:traits callback:^(NSDictionary* _Nullable visitorProfile){
  // handle the returned visitorProfile dictionary here
}];

[ACPAudience signalWithData:traits withCompletionHandler:^(NSDictionary * _Nullable visitorProfile, NSError * _Nullable error) {
  if (error) {
    // handle the error here
  } else {
    // handle the returned visitorProfile dictionary here
  }
}];
```

**Swift**

```swift
ACPAudience.signal(withData: ["key1": "value1", "key2": "value2"], callback: { (visitorProfile) in
  // handle the visitorProfile here  
})

ACPAudience.signal(withData: ["key1": "value1", "key2": "value2"], withCompletionHandler: { (visitorProfile, error) in
  if let error = error {
    // handle error
  } else {
    // handle the returned visitorProfile here
  }    
})
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

### signalWithData

```jsx
ACPAudience.signalWithData({"yourDataKey": "yourDataValue"}).then(profile => console.log("AdobeExperienceSDK: Visitor Profile: " + profile));
```
{% endtab %}
{% endtabs %}

