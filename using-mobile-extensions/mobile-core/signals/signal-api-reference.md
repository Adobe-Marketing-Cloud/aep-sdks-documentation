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
**Objective C**

```objectivec
NSString *signalExtensionVersion = [AEPMobileSignal extensionVersion];
```

**Swift**

```swift
var signalExtensionVersion  = AEPSignal.extensionVersion
```
{% endtab %}


{% endtabs %}

## CollectPII API

The Signal extension can be used to handle `collectPII` rules. For more information, see the [collectPII](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#collect-pii) API.

