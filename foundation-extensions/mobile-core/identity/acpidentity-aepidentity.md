# Migrating to AEPIdentity reference

This document is a reference comparison of AEPIdentity \(3.x\) APIs against their equivalent APIs in ACPIdentity \(2.x\) for an iOS mobile application implementation.

## Public Classes

| Type | AEP 3.x \(Swift\) | AEP 3.x \(Objective-C\) | ACP 2.x \(Objective-C\) |
| :--- | :--- | :--- | :--- |
| Primary Class | Identity | AEPMobileIdentity | ACPIdentity |
| Class | MobileCore | AEPMobileCore | ACPCore |

## Identity extension APIs

For more information, please read the [Identity API reference](identity-api-reference.md).

### appendVisitorInfoForURL

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}

```swift
Identity.appendTo(url:completion:)
```

{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}

```objective-c
[AEPMobileIdentity appendToUrl:completion:];
```

{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}

```objective-c
[ACPMobileIdentity appendToUrl:withCallback:];
[ACPMobileIdentity appendToUrl:withCompletionHandler:];
```

{% endtab %}
{% endtabs %}

### extensionVersion

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
Identity.extensionVersion
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
[AEPMobileIdentity extensionVersion];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
[ACPIdentity extensionVersion];
```
{% endtab %}
{% endtabs %}

### getExperienceCloudId

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
Identity.getExperienceCloudId(completion:)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
[AEPMobileIdentity getExperienceCloudId:];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
[ACPIdentity getExperienceCloudId:];
[ACPIdentity getExperienceCloudIdWithCompletionHandler:];
```
{% endtab %}
{% endtabs %}

### getIdentifiers

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
Identity.getIdentifiers(completion:)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
[AEPMobileIdentity getIdentifiers:];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
[ACPIdentity getIdentifiers:];
[ACPIdentity getIdentifiersWithCompletionHandler:];
```
{% endtab %}
{% endtabs %}

### getUrlVariables

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
Identity.getUrlVariables(completion:)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
[AEPMobileIdentity getUrlVariables:];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
[ACPIdentity getUrlVariables:];
[ACPIdentity getUrlVariablesWithCompletionHandler:];
```
{% endtab %}
{% endtabs %}

### setAdvertisingIdentifier

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
MobileCore.setAdvertisingIdentifier(_ identifier:)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
[AEPMobileCore setAdvertisingIdentifier:];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
[ACPCore setAdvertisingIdentifier:];
```
{% endtab %}
{% endtabs %}

### setPushIdentifier

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
MobileCore.setPushIdentifier(_ deviceToken:)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
[AEPMobileCore setPushIdentifier:];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
[ACPCore setPushIdentifier:];
```
{% endtab %}
{% endtabs %}

### syncIdentifier

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
Identity.syncIdentifier(identifierType:identifier:authenticationState:)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
[AEPMobileIdentity syncIdentifierWithType:identifier:authenticationState:];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
[ACPIdentity syncIdentifier:identifier:authentication:];
```
{% endtab %}
{% endtabs %}

### syncIdentifiers

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
Identity.syncIdentifiers(identifierType:identifier:authenticationState:)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
[AEPMobileIdentity syncIdentifiers:];
[AEPMobileIdentity syncIdentifiers:authenticationState:];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
[ACPIdentity syncIdentifiers:];
[ACPIdentity syncIdentifiers:authentication:];
```
{% endtab %}
{% endtabs %}
