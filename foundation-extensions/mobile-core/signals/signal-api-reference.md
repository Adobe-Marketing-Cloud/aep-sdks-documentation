# Signal API reference

## extensionVersion

The `extensionVersion()` API returns the version of the Signal extension that is registered with the Mobile Core extension.

To get the version of the Signal extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static String extensionVersion();
```

**Example**

```java
String signalExtensionVersion = Signal.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
**Syntax**

```swift
public static let extensionVersion
```

**Examples**

**Swift**

```swift
let version = Signal.extensionVersion
```

**Objective-C**

```objectivec
NSString *version = [AEPMobileSignal extensionVersion];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
**Syntax**

```objectivec
(nonnull NSString*) extensionVersion;
```

**Examples**

**Swift**

```swift
var signalExtensionVersion  = ACPSignal.extensionVersion()
```

**Objective-C**

```objectivec
NSString *signalExtensionVersion = [ACPSignal extensionVersion];
```

{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
ACPSignal.extensionVersion().then(signalExtensionVersion => console.log("AdobeExperienceSDK: ACPSignal version: " + signalExtensionVersion));
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

```dart
String signalExtensionVersion = await FlutterACPSignal.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}
### Cordova

```jsx
ACPSignal.extensionVersion(function(version) {  
    console.log("ACPSignal version: " + version);
}, function(error) {  
    console.log(error);  
});
```
{% endtab %}

{% tab title="Unity" %}
### C\#

```csharp
string signalVersion = ACPSignal.ExtensionVersion();
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

```csharp
string signalVersion = ACPSignal.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## registerExtension

Registers the Signal extension with the Mobile Core.

{% tabs %}
{% tab title="Android" %}
**Syntax**

```java
public static void registerExtension()
```

**Example**

```java
Signal.registerExtension();
```
{% endtab %}

{% tab title="iOS \(AEP 3.x\)" %}
This API no longer exists in `Signal`. Instead, the extension should be registered by calling the `registerExtensions` API in the MobileCore. Please see the updated SDK initialization steps at the [migrate to Swift tutorial.](../../resources/migrate-to-swift.md#update-sdk-initialization)
{% endtab %}

{% tab title="iOS \(ACP 2.x\)" %}
**Syntax**

```text
+ (void) registerExtension;
```

**Example**

**Swift**

```swift
ACPSignal.registerExtension()
```

**Objective-C**

```text
[ACPSignal registerExtension];
```
{% endtab %}

{% tab title="React Native" %}
When using React Native, register the Signal extension with Mobile Core in native code as shown on the Android and iOS tabs.
{% endtab %}
{% endtabs %}

## CollectPII API

The Signal extension can be used to handle `collectPII` rules. For more information, see the [collectPII](../mobile-core-api-reference#collect-pii) API.

