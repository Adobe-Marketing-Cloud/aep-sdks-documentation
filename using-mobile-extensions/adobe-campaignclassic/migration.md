# Migrating to AEPCampaignClassic reference

This document is a reference comparison of ACPCampaignClassic \(2.x\) APIs against their equivalent APIs in AEPCampaignClassic \(3.x\) for an iOS mobile application implementation.

The AEPCampaignClassic extension is implemented purely in Swift and is compatible with the AEPCore swift SDK. To ensure a smooth transition from the ACPCampaignClassic SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application. If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## AEPCampaignClassic classes

| Type | AEP \(3.x\) | AEP 3.x \(Objective-C\) | ACP \2.x\) |
| :--- | :--- | :--- | :--- |
| Primary Class \(Module\) | CampaignClassic | AEPMobileCampaignClassic | ACPCampaignClassic |

## AEPCampaignClassic APIs

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

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
+ (nonnull NSString*) extensionVersion;
```
{% endtab %}
{% endtabs %}

### registerExtension

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
{% hint style="info" %}
Registration occurs by passing `CampaignClassic` to the `MobileCore.registerExtensions` API.
{% endhint %}

```swift
MobileCore.registerExtensions([CampaignClassic.self])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
{% hint style="info" %}
Registration occurs by passing `AEPMobileCampaignClassic` to the `[AEPMobileCore registerExtensions:completion:]` API.
{% endhint %}

```objective-c
[AEPMobileCore registerExtensions:@[AEPMobileCampaignClassic.class] completion:nil];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
+ (void) registerExtension;
```
{% endtab %}
{% endtabs %}

### registerDevice

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func registerDevice(token: Data, userKey: String?, additionalParameters: [String: Any]?)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
+ (void) registerDeviceWithToken: (nonnull NSData*) token userKey: (nullable NSString*) userKey additionalParams: (nullable NSDictionary*) additionalParams;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
+ (void) registerDevice: (nonnull NSData*) token userKey: (nullable NSString*) userKey additionalParams: (nullable NSDictionary*) additionalParams callback: (nullable void (^) (BOOL success)) callback;
```
{% endtab %}
{% endtabs %}

### trackNotificationClick

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func trackNotificationClick(withUserInfo userInfo: [AnyHashable: Any])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
+ (void) trackNotificationClickWithUserInfo: (nonnull NSDictionary*) userInfo;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
+ (void) trackNotificationClick: (nonnull NSDictionary<NSString*, NSString*>*) trackInfo;
```
{% endtab %}

### trackNotificationClick

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func trackNotificationReceive(withUserInfo userInfo: [AnyHashable: Any])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```objective-c
+ (void) trackNotificationReceiveWithUserInfo: (nonnull NSDictionary<NSString*, NSString*>*) userInfo;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```objective-c
+ (void) trackNotificationReceive: (nonnull NSDictionary<NSString*, NSString*>*) trackInfo;
```
{% endtab %}
{% endtabs %}
