# Migrating to AEPLifecycle reference

This document is a reference comparison of AEPLifecycle (3.x) APIs against their equivalent APIs in ACPLifecycle (2.x) for an iOS mobile application implementation.

## Public `Classes`

| Type | AEP 3.x (Swift) | AEP 3.x (Objective-C) | ACP 2.x (Objective-C) |
| :--- | :--- | :--- | :--- |
| Primary Class | Lifecycle | AEPMobileLifecycle | ACPLifecycle |
| Class | MobileCore | AEPMobileCore | ACPCore |

## Lifecycle extension APIs

For more information, please read the [Lifecycle API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle/lifecycle-api-reference).

### extensionVersion

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
Lifecycle.extensionVersion
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```text
[AEPMobileLifecycle extensionVersion];
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```text
ACPLifecycle.extensionVersion()
```
{% endtab %}
{% endtabs %}

### lifecycleStart

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
MobileCore.lifecycleStart(additionalContextData: data)
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```text
[AEPMobileCore lifecycleStart: data];
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```text
[ACPCore lifecycleStart: data];
```
{% endtab %}
{% endtabs %}

### lifecyclePause

{% tabs %}
{% tab title="AEP 3.x (Swift)" %}
```swift
MobileCore.lifecyclePause()
```
{% endtab %}

{% tab title="AEP 3.x (Objective-C)" %}
```text
[AEPMobileCore lifecyclePause];
```
{% endtab %}

{% tab title="ACP 2.x (Objective-C)" %}
```text
[ACPCore lifecyclePause];
```
{% endtab %}
{% endtabs %}

