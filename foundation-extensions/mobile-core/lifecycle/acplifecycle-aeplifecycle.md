# Migrating to AEPLifecycle

This document is a reference comparison of AEPLifecycle \(3.x\) APIs against their equivalent APIs in ACPLifecycle \(2.x\) for an iOS mobile application implementation.

## Pod installation

| AEP (3.x)                    | ACP (2.x)               |
| ---------------------------- | ----------------------- |
| pod 'AEPLifecycle', '~> 3.0' | pod 'ACPCore', '~> 2.0' |
| pod 'AEPCore', '~> 3.0'      | pod 'ACPCore', '~> 2.0' |

## Primary Classes

{% tabs %}
{% tab title="Swift" %}

| AEP (3.x)  | ACP (2.x)    |
| ---------- | ------------ |
| Lifecycle  | ACPLifecycle |
| MobileCore | ACPCore      |

{% endtab %}

{% tab title="Objective-C" %}

| AEP (3.x)          | ACP (2.x)    |
| ------------------ | ------------ |
| AEPMobileLifecycle | ACPLifecycle |
| AEPMobileCore      | ACPCore      |

{% endtab %}

{% endtabs %}

## Lifecycle extension APIs

{% tabs %}
{% tab title="Swift" %}

| API              | AEP (3.x)                                              | ACP (2.x)                       |
| ---------------- | ------------------------------------------------------ | ------------------------------- |
| extensionVersion | Lifecycle.extensionVersion                             | ACPLifecycle.extensionVersion() |
| lifecycleStart   | MobileCore.lifecycleStart(additionalContextData: data) | ACPCore.lifecycleStart(data)    |
| lifecyclePause   | MobileCore.lifecyclePause()                            | ACPCore.lifecyclePause()        |

{% endtab %}

{% tab title="Objective-C" %}

| API              | AEP (3.x)                              | ACP (2.x)                        |
| ---------------- | -------------------------------------- | :------------------------------- |
| extensionVersion | [AEPMobileLifecycle extensionVersion]; | [ACPLifecycle extensionVersion]; |
| lifecycleStart   | [AEPMobileCore lifecycleStart: data];  | [ACPCore lifecycleStart: data];  |
| lifecyclePause   | [AEPMobileCore lifecyclePause];        | [ACPCore lifecyclePause];        |

{% endtab %}

{% endtabs %}

For more information, please read the [Lifecycle API reference](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/lifecycle/lifecycle-api-reference).