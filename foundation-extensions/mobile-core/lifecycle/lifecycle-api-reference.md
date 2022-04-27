# Lifecycle API reference

## Version of the Lifecycle extension

The `extensionVersion()` API returns the version of the Lifecycle extension that is registered with the Mobile Core extension.

To get the version of the Lifecycle extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
#### Java

```java
String lifecycleExtensionVersion = Lifecycle.extensionVersion();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
**Swift**

```swift
let version = Lifecycle.extensionVersion
```

**Objective C**

```objectivec
NSString *version = [AEPMobileLifecycle extensionVersion];
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
**Objective C**

```objectivec
NSString *lifecycleExtensionVersion = [ACPLifecycle extensionVersion];
```

**Swift**

```swift
let lifecycleExtensionVersion  = ACPLifecycle.extensionVersion()
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPLifecycle.extensionVersion().then(lifecycleExtensionVersion => console.log("AdobeExperienceSDK: ACPLifecycle version: " + lifecycleExtensionVersion));
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

```dart
String lifeycycleExtensionVersion = await FlutterACPLifecycle.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

```jsx
ACPLifecycle.extensionVersion(function(version) {  
   console.log("ACPLifecycle version: " + version);
}, function(error) {  
   console.log(error);  
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

```csharp
string lifecycleVersion = ACPLifecycle.ExtensionVersion();
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

```csharp
string lifecycleVersion = ACPLifecycle.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## Lifecycle Start

Starts the collection of lifecycle data.

**For Analytics use case:** Use this API to start a new lifecycle session or resume a previously paused lifecycle session. If a previously paused session timed out, then a new session is created. If a current session is running, then calling this method does nothing.

**For Platform use case:** Use this API to dispatch a [Lifecycle Application Foreground](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle/lifecycle-event-reference#lifecycle-application-foreground) event when the application is launched.

### lifecycleStart <a id="lifecycleStart"></a>

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void lifecycleStart(final Map<String, String> additionalContextData);
```

**Example**

```java
MobileCore.lifecycleStart(null);
```

If you need to collect additional lifecycle data:

```text
contextData.put("myapp.category", "Game");
MobileCore.lifecycleStart(additionalContextData);
```

{% hint style="warning" %}
This method should be called from the Activity onResume method.
{% endhint %}
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
#### Swift

```swift
 MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
```

#### Objective-C

**Syntax**

```swift
 @objc(lifecycleStart:)
 static func lifecycleStart(additionalContextData: [String: Any]?)
```

**Example**

```text
 [AEPMobileCore lifecycleStart:nil];
```

If you need to collect additional lifecycle data:

```text
 [AEPMobileCore lifecycleStart:@{@"contextDataKey": @"contextDataVal"}];
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
#### Objective-C

**Syntax**

```text
+ (void) lifecycleStart: (nullable NSDictionary<NSString*, NSString*>*) additionalContextData;
```

**Example**

```text
[ACPCore lifecycleStart:nil];
```

If you need to collect additional lifecycle data:

```text
[ACPCore lifecycleStart:@{@"state": @"appResume"}];
```

#### Swift

```swift
ACPCore.lifecycleStart(["state": "appResume"])
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

When using React Native, starting to collect lifecycle data should be done in native code which is shown under the Android and iOS (ACP 2.x) tabs.

{% endtab %}

{% tab title="Cordova" %}
#### Cordova

When using Cordova, the `lifecycleStart` method call must be made in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Unity" %}
#### C\#

When using Unity, the `LifecycleStart` method call must be made from the `OnApplicationPause` method.

```csharp
private void OnApplicationPause(bool pauseStatus)
{
  if (!pauseStatus)
  {
    ACPCore.LifecyclePause();
  }
  else
  {
    var cdata = new Dictionary<string, string>();
    cdata.Add("launch.data", "added");
    ACPCore.LifecycleStart(cdata);
  }
}
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

**iOS**

When using iOS, the `LifecycleStart` method call must be made from the `OnActivated` method.

```csharp
public override void OnActivated(UIApplication uiApplication)
{
  base.OnActivated(uiApplication);
  ACPCore.LifecycleStart(null);
}
```

**Android**

When using Android, the `LifecycleStart` method call must be made from the `OnResume` method.

```csharp
protected override void OnResume()
{
  base.OnResume();
  ACPCore.LifecycleStart(null);
}
```
{% endtab %}
{% endtabs %}

### Lifecycle Pause

Pauses the collection of lifecycle data.

**For Analytics use case:** Use this API to pause the collection of lifecycle data.

**For Platform use case:** Use this API to dispatch a [Lifecycle Application Background](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle/lifecycle-event-reference#lifecycle-application-background) event when the application closes.

### lifecyclePause <a id="lifecyclePause"></a>

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void lifecyclePause()
```

**Example**

```java
MobileCore.lifecyclePause();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
#### Swift

```swift
 MobileCore.lifecyclePause()
```

#### Objective-C

**Syntax**

```swift
 @objc(lifecyclePause)
 static func lifecyclePause()
```

**Example**

```text
 [AEPMobileCore lifecyclePause];
```
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
#### Objective-C

**Syntax**

```text
+ (void) lifecyclePause;
```

**Example**

```text
[ACPCore lifecyclePause];
```

#### Swift

```swift
ACPCore.lifecyclePause()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

When using React Native, pausing the collection of lifecycle data should be done in native code which is shown under the Android and iOS (ACP 2.x) tabs.

{% endtab %}

{% tab title="Cordova" %}
#### Cordova

When using Cordova, the `lifecyclePause` method call must be made in native code which is shown under the Android and iOS tabs.
{% endtab %}

{% tab title="Unity" %}
#### C\#

When using Unity, the `LifecyclePause` method call must be made from the `OnApplicationPause` method.

```csharp
private void OnApplicationPause(bool pauseStatus)
{
  if (!pauseStatus)
  {
    ACPCore.LifecyclePause();
  }
  else
  {
    var cdata = new Dictionary<string, string>();
    cdata.Add("launch.data", "added");
    ACPCore.LifecycleStart(cdata);
  }
}
```
{% endtab %}

{% tab title="Xamarin" %}
#### C\#

**iOS**

When using iOS, the `LifecyclePause` method call must be made from the `OnResignActivation` method.

```csharp
public override void OnResignActivation(UIApplication uiApplication)
{
  base.OnResignActivation(uiApplication);
  ACPCore.LifecyclePause();
}
```

**Android**

When using Android, the `LifecyclePause` method call must be made from the `OnPause` method.

```csharp
protected override void OnPause()
{
  base.OnPause();
  ACPCore.LifecyclePause();
}
```
{% endtab %}
{% endtabs %}

