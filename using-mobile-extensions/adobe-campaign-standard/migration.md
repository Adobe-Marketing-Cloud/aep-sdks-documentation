# Migrating to AEPCampaign reference

This document is a reference comparison of ACPCampaign \(1.x\) APIs against their equivalent APIs in AEPCampaign \(3.x\) for an iOS mobile application implementation.

The AEPCampaign extension is implemented purely in Swift and is compatible with the AEPCore swift SDK. To ensure a smooth transition from the ACPCampaign SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application. If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## AEPCampaign classes

| Type | AEP \(3.x\) | AEP 3.x \(Objective-C\) | ACP \(1.x\) |
| :--- | :--- | :--- | :--- |
| Primary Class \(Module\) | Campaign | AEPMobileCampaign | ACPCampaign |

## AEPCampaign APIs

### extensionVersion

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static var extensionVersion: String
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}

{% tab title="ACP 1.x \(Objective-C\)" %}
```objective-c
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}
{% endtabs %}

### registerExtension

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
{% hint style="info" %}
Registration occurs by passing `Campaign` to the `MobileCore.registerExtensions` API.
{% endhint %}

```swift
MobileCore.registerExtensions([Campaign.self])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
{% hint style="info" %}
Registration occurs by passing `AEPMobileCampaign` to the `[AEPMobileCore registerExtensions:completion:]` API.
{% endhint %}

```objective-c
[AEPMobileCore registerExtensions:@[AEPMobileCampaign.class] completion:nil];
```
{% endtab %}

{% tab title="ACP 1.x \(Objective-C\)" %}
```objective-c
+ (void) registerExtension;
```
{% endtab %}
{% endtabs %}

### resetLinkageFields

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func resetLinkageFields()
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
+ (void) resetLinkageFields;
```
{% endtab %}

{% tab title="ACP 1.x \(Objective-C\)" %}
```objective-c
+ (void) resetLinkageFields;
```
{% endtab %}
{% endtabs %}

### setLinkageFields

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func setLinkageFields(_ linkageFields: [String: String])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*)
```
{% endtab %}

{% tab title="ACP 1.x \(Objective-C\)" %}
```objective-c
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```
{% endtab %}
{% endtabs %}

