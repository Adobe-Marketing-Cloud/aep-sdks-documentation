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

{% tab title="iOS" %}

#### iOS

**Objective-C**

```objectivec
NSString *signalExtensionVersion = [ACPSignal extensionVersion];
```

**Swift**

```swift
var signalExtensionVersion  = ACPSignal.extensionVersion()
```

{% endtab %}

{% tab title="React Native" %}

#### JavaScript

```jsx
ACPSignal.extensionVersion().then(signalExtensionVersion => console.log("AdobeExperienceSDK: ACPSignal version: " + signalExtensionVersion));
```

{% endtab %}
{% endtabs %}

## CollectPII API

The Signal extension can be used for handling collectPII rules, for more information check the Mobile Core  [collectPII](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#collect-pii) API.

