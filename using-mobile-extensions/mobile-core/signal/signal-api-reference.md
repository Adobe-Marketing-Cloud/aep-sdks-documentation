# Signal API reference

## Version of the Signal extension

The `extensionVersion()` API returns the version of the Signal extension that is registered with the MobileCore extension.

To get the version of the Identity extension, use the following code sample:

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

The Signal extension listens for the information provided through [collectPII API](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#collect-pii)

