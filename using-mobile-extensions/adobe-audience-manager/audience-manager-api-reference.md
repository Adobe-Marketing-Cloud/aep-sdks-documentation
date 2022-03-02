# Audience Manager API reference

## extensionVersion

The `extensionVersion()` API returns the version of the Audience extension that is registered with the Mobile Core extension.

To get the version of the Audience extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
### Java

**Example**

```java
String audienceExtensionVersion = Audience.extensionVersion();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
### Swift

**Syntax**

```swift
static var extensionVersion: String
```

**Example**

```swift
let audienceExtensionVersion  = Audience.extensionVersion()
```

### Objective-C

**Syntax**

```objectivec
+ (nonnull NSString*) extensionVersion;
```

**Example**

```objectivec
NSString *audienceExtensionVersion = [AEPMobileAudience extensionVersion];
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
### Swift

**Syntax**

```swift
+ (nonnull NSString*) extensionVersion;
```

**Example**

```swift
let audienceExtensionVersion  = ACPAudience.extensionVersion()
```

### Objective-C

**Syntax**

```objectivec
add
```

**Example**

```objectivec
NSString *audienceExtensionVersion = [ACPAudience extensionVersion];
```

{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Example**

```jsx
ACPAudience.extensionVersion().then(audienceExtensionVersion => console.log("AdobeExperienceSDK: ACPAudience version: " + audienceExtensionVersion));
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Example**

```dart
String audienceExtensionVersion = await FlutterACPAudience.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

**Example**

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

**Example**

```csharp
string audienceExtensionVersion = ACPAudience.ExtensionVersion();
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

**Example**

```csharp
string audienceExtensionVersion = ACPAudience.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## getVisitorProfile

This API returns the most recently obtained visitor profile. The visitor profile is saved in the SDK's local storage for access across multiple launches of your app. If no audience signal has been sent before, when this API is called, a null value is returned.

{% tabs %}
{% tab title="Android" %}
This API returns the most recently obtained visitor profile. For easy access across multiple launches of your app, the visitor profile is saved in `SharedPreferences`. If no signal has been submitted, null is returned.

When an AdobeCallbackWithError is provided, an AdobeError can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with the visitor profile.

### Java

**Syntax**

```java
public static void getVisitorProfile(final AdobeCallback<Map<String, String>> adobeCallback)
```

**Example**

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

{% tab title="iOS \(AEP 3.x\)" %}
This API returns the most recently obtained visitor profile.

### Swift

**Syntax**

```swift
static func getVisitorProfile(completion: @escaping ([String: String]?, Error?) -> Void)
```

**Example**

```swift
Audience.getVisitorProfile { (visitorProfile, error) in
   if error != nil {
    // handle the error here
   } else {
    // handle the retrieved visitorProfile here
   }
  }
```

### Objective-C

**Syntax**

```objectivec
+  (void) getVisitorProfile:^(NSDictionary<NSString *,NSString *> * _Nullable, NSError * _Nullable)completion
```

**Example**

```text
[AEPMobileAudience getVisitorProfile:^(NSDictionary<NSString *,NSString *> * _Nullable visitorProfile, NSError * _Nullable error) {
   if (error) {
    // handle the error here
   } else {
    // handle the returned visitorProfile dictionary here
   }
}];
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
The `getVisitorProfile` API returns the most recently obtained visitor profile. For easy access across multiple launches of your app, the visitor profile is saved in `NSUserDefaults`. If no signal has been submitted, nil is returned.

{% hint style="info" %}
The `getVisitorProfileWithCompletionHandler` method was added in ACPAudience version 2.1.0.
{% endhint %}

### Swift

**Syntax**

```swift
func getVisitorProfile(_ callback: @escaping ([AnyHashable : Any]?) -> Void)

func getVisitorProfile(completionHandler: @escaping ([AnyHashable : Any]?, Error?) -> Void)

```

**Example**

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

### Objective-C

**Syntax**

```objectivec
+ (void) getVisitorProfile: (nonnull void (^) (NSDictionary* __nullable visitorProfile)) callback;

+ (void) getVisitorProfileWithCompletionHandler: (nonnull void (^) (NSDictionary* __nullable visitorProfile, NSError* __nullable error)) completionHandler;
```

**Example**

```objectivec
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

{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Example**

```jsx
ACPAudience.getVisitorProfile().then(profile => console.log("AdobeExperienceSDK: Visitor Profile: " + profile));
```
{% endtab %}
{% endtabs %}

## registerExtension

This API registers an extension class that was derived from `ACPExtension` with a unique name. This call validates the parameters to ensure that the name is not empty, the name is unique, and that the parent class is `ACPExtension`.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public  static void registerExtension() throws InvalidInitException
```

**Example**

```java
Audience.registerExtension();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

**Syntax**

```swift
static func registerExtensions(_ extensions: [NSObject.Type], 
                               _ completion: (() -> Void)? = nil)
```

**Example**

```swift
MobileCore.registerExtension([Audience.self])
```

### Objective-C

**Syntax**

```objectivec
+ (void) registerExtensions: (NSArray<Class*>* _Nonnull) extensions 
                 completion: (void (^ _Nullable)(void)) completion;
```

**Example**

```objectivec
[AEPMobileCore registerExtensions:@[AEPMobileAudience.class] completion:nil];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### Swift

**Syntax**

```swift
func registerExtension()
```

**Example**

```swift
ACPAudience.registerExtension()
```

### Objective-C

**Syntax**

```objectivec
+ (BOOL) registerExtension: (nonnull Class) extensionClass
                     error: (NSError* _Nullable* _Nullable) error;
```

**Example**

```objectivec
[ACPAudience registerExtension];
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Example**

```jsx
ACPAudience.registerExtension();
```
{% endtab %}
{% endtabs %}

## reset

This API helps you reset the Audience Manager UUID and purges the current visitor profile.

{% hint style="info" %}
For more information about the UUID, the DPID, the DPUUID and other Audience Manager identifiers, see [Index of IDs in Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
This API resets the Audience Manager UUID and purges the current visitor profile from `android.content.SharedPreferences`. The Audience reset also clears the current in-memory DPID and DPUUID variables.

### Java

**Syntax**

```java
public static void reset()
```

**Example**

```java
Audience.reset();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
This API resets the Audience Manager UUID and purges the current visitor profile from `UserDefaults`. The Audience reset also clears the current in-memory DPID and DPUUID variables.

### Swift

**Syntax**

```swift
static func reset()
```

**Example**

```swift
Audience.reset()
```

### Objective-C

**Syntax**

```objectivec
+ (void) reset
```

**Example**

```objectivec
[AEPMobileAudience reset];
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
The `reset` API resets the Audience Manager UUID and purges the current visitor profile from `UserDefaults`. The Audience reset also clears the current in-memory DPID and DPUUID variables.

### Swift

**Syntax**

```swift
func reset()
```

**Example**

```swift
ACPAudience.reset()
```

### Objective-C

**Syntax**

```objectivec
+ (void) reset;
```

**Example**

```objectivec
[ACPAudience reset];
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Example**

```jsx
ACPAudience.reset();
```
{% endtab %}
{% endtabs %}

## signalWithData

This method is used to send a signal with traits to Audience Manager and get the matching segments returned in a block callback. Audience Manager sends the UUID in response to an initial signal call. The UUID is persisted on local SDK storage and is sent by the SDK to Audience Manager in all subsequent signal requests.

If you are using the Experience Cloud ID \(ECID\) Service \(formerly MCID\), the ECID and other custom identifiers for the same visitor are sent with each signal request. The visitor profile that is returned by Audience Manager is saved in SDK local storage and is updated with subsequent signal calls.

{% hint style="info" %}
For more information about the UUID and other Audience Manager identifiers, see the [index of IDs in Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en).
{% endhint %}

{% tabs %}
{% tab title="Android" %}
The `signalWithData` API sends Audience Manager a signal with traits and returns the matching segments for the visitor in a callback.

Audience Manager sends the AAM UUID in response in initial signal call. The AAM UUID is persisted in `SharedPreferences` and is sent by the SDK in all subsequent signal requests. If available, the ECID is also sent in each signal request with the DPID and the DPUUID. The visitor profile that Audience Manager returns is saved in `SharedPreferences` and is updated with every signal call.

When an `AdobeCallbackWithError` is provided, an `AdobeError` can be returned in the eventuality of an unexpected error or if the default timeout \(5000ms\) is met before the callback is returned with the visitor profile.

### Java

**Syntax**

```java
public static void signalWithData(final Map<String, String> data, final AdobeCallback<Map<String, String>> callback)
```

* `data` is the traits data for the current visitor.
* `callback` is the void method that is invoked with the visitor's profile as a parameter.

**Example**

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

{% tab title="iOS \(AEP 3.x\)" %}
The `signalWithData` API sends Audience Manager a signal with traits and returns the matching segments for the visitor in a closure.

Audience Manager sends the AAM UUID in response in initial signal call. The AAM UUID is persisted in `NSUserDefaults` and is sent by the SDK in all subsequent signal requests. If available, the Experience Cloud ID \(MID\) is also sent in each signal request with the DPID and the DPUUID. The visitor profile that Audience Manager returns is saved in `NSUserDefaults` and is updated with every signal call.

### Swift

**Syntax**

```swift
static func signalWithData(data: [String: String], completion: @escaping ([String: String]?, Error?) -> Void)
```

* `data` is the traits data for the current visitor.
* `callback` is the void method that is invoked with the visitor's profile as a parameter.

**Example**

```swift
Audience.signalWithData(data: ["trait": "trait value"]) { (traits, error) in
  if error != nil {
     // handle the error here
     } else {
     // handle the returned visitorProfile here
     }
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) signalWithData:(NSDictionary<NSString *,NSString *> * _Nonnull) completion:^(NSDictionary<NSString *,NSString *> * _Nullable, NSError * _Nullable)completion
```

**Example**

```objectivec
NSDictionary *traits = @{@"key1":@"value1",@"key2":@"value2"};
[AEPMobileAudience signalWithData:traits completion:^(NSDictionary<NSString *,NSString *> * _Nullable visitorProfile, NSError* _Nullable error) {
  if (error) {
     // handle the error here
     } else {
     // handle the returned visitorProfile dictionary here
     }
}];
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
The `signalWithData` API sends Audience Manager a signal with traits and returns the matching segments for the visitor in a callback.

Audience Manager sends the AAM UUID in response in initial signal call. The AAM UUID is persisted in `NSUserDefaults` and is sent by the SDK in all subsequent signal requests. If available, the Experience Cloud ID \(MID\) is also sent in each signal request with the DPID and the DPUUID. The visitor profile that Audience Manager returns is saved in `NSUserDefaults` and is updated with every signal call.

{% hint style="info" %}
The `signalWithData:withCompletionHandler` method was added in ACPAudience version 2.1.0.
{% endhint %}

### Swift

**Syntax**

```swift
func signal(withData data: [String : String]?, callback: (([AnyHashable : Any]?) -> Void)? = nil)

func signal(withData data: [String : String], withCompletionHandler completionHandler: @escaping ([AnyHashable : Any]?, Error?) -> Void)
```

**Example**

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

### Objective-C

**Syntax**

```objectivec
+ (void) signalWithData: (NSDictionary<NSString*, NSString*>* __nullable) data
                       callback: (nullable void (^) (NSDictionary* __nullable visitorProfile)) callback;

+ (void) signalWithData: (NSDictionary<NSString*, NSString*>* __nullable) data
                        withCompletionHandler:: (nullable void (^) (NSDictionary* __nullable visitorProfile, NSError* __nullable error)) completionHandler;
```

* `data` is the traits data for the current visitor.
* `callback` is the void method that is invoked with the visitor's profile as a parameter.

**Example**

```objectivec
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
{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Example**

```jsx
ACPAudience.signalWithData({"yourDataKey": "yourDataValue"}).then(profile => console.log("AdobeExperienceSDK: Visitor Profile: " + profile));
```
{% endtab %}
{% endtabs %}

