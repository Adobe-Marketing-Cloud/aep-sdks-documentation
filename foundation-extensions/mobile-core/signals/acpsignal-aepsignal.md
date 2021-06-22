# Migrating to AEPSignal Reference

This document is a reference comparison of ACPSignal \(2.x\) APIs against their equivalent APIs in AEPSignal \(3.x\).

## Primary `Classes`

| Type | AEP 3.x \(Swift\) | AEP 3.x \(Objective-C\) | ACP 2.x \(Objective-C\) |
| :--- | :--- | :--- | :--- |
| Primary Class | Signal | AEPMobileSignal | ACPSignal |

## Signal extension APIs

For more information, please read the [Signal API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/signals/signal-api-reference).

### extensionVersion

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
public static var extensionVersion: String
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}
{% endtabs %}

