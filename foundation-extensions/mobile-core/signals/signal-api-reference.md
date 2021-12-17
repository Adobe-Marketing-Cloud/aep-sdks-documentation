# Signal API reference

## Version of the Signal extension

The `extensionVersion()` API returns the version of the Signal extension that is registered with the Mobile Core extension.

To get the version of the Signal extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
#### Java

```java
String signalExtensionVersion = Signal.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
### Swift

```swift
let version = Signal.extensionVersion
```

### Objective-C

```objectivec
NSString *version = [AEPMobileSignal extensionVersion];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### Swift

```swift
var signalExtensionVersion  = ACPSignal.extensionVersion()
```

### Objective-C

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

## CollectPII API

The Signal extension can be used to handle `collectPII` rules. For more information, see the [collectPII](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#collect-pii) API.

