# Migrating to AEPTarget reference

This document is a reference comparison of AEPTarget\(3.x\) APIs against their equivalent ACPTarget \(2.x\) APIs for an iOS mobile application implementation.

The AEPTarget extension is implemented purely in Swift and is compatible with the AEPCore swift SDK. To ensure a smooth transition from the ACPTarget SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application. If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## Public classes

| Type | AEP 3.x \(Swift\) | AEP 3.x \(Objective-C\) | ACP 2.x \(Objective-C\) |
| :--- | :--- | :--- | :--- |
| Primary Class \(Module\) | Target | AEPMobileTarget | ACPTarget |
| Class | TargetRequest | AEPTargetRequestObject | ACPTargetRequestObject |
| Class | TargetPrefetch | AEPTargetPrefetchObject | ACPTargetPrefetchObject |
| Class | TargetOrder | AEPTargetOrder | ACPTargetOrder |
| Class | TargetParameters | AEPTargetParameters | ACPTargetParameters |
| Class | TargetProduct | AEPTargetProduct | ACPTargetProduct |

## Public APIs

### clearPrefetchCache

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func clearPrefetchCache()
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) clearPrefetchCache;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) clearPrefetchCache;
```
{% endtab %}
{% endtabs %}

### clickedLocation

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func clickedLocation(_ name: String, targetParameters: TargetParameters? = nil)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) clickedLocation: (NSString* _NonNull) name
    withTargetParameters: (AEPTargetParameters* _Nullable) targetParameters;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) locationClickedWithName: (nonnull NSString*) name
                targetParameters: (nullable ACPTargetParameters*) parameters;
```
{% endtab %}
{% endtabs %}

### extensionVersion

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static var extensionVersion: String
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

### getThirdPartyId

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func getThirdPartyId(_ completion: @escaping (String?, Error?) -> Void)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) getThirdPartyId: (nonnull void (^) (NSString* _Nullable thirdPartyId,  NSError* _Nullable error)) completion;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) getThirdPartyId: (nonnull void (^) (NSString* __nullable thirdPartyId)) callback;
```
{% endtab %}
{% endtabs %}

### getTntId

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func getTntId(_ completion: @escaping (String?, Error?) -> Void)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) getTntId: (nonnull void (^) (NSString* _Nullable tntId,  NSError* _Nullable error)) completion;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) getTntId: (nonnull void (^) (NSString* __nullable tntId)) callback;
```
{% endtab %}
{% endtabs %}

### prefetchContent

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func prefetchContent(_ prefetchArray: [TargetPrefetch], with targetParameters: TargetParameters? = nil, _ completion: ((Error?) -> Void)?)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) prefetchContent: (NSArray<AEPTargetPrefetchObject*>* _NonNull) prefetchArray
          withParameters: (AEPTargetParameters* _Nullable) targetParameters
                callback: (nullable void (^) (NSError* _Nullable error)) completion;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) prefetchContent: (nonnull NSArray<ACPTargetPrefetchObject*>*) prefetchObjectArray
          withParameters: (nullable ACPTargetParameters*) parameters
                callback: (nullable void (^) (NSError* _Nullable error)) callback;
```
{% endtab %}
{% endtabs %}

### registerExtension

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
{% hint style="info" %}
Registration occurs by passing `Target` to the `MobileCore.registerExtensions` API.
{% endhint %}

```swift
MobileCore.registerExtensions([Target.self])
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
{% hint style="info" %}
Registration occurs by passing `AEPMobileTarget` to the `[AEPMobileCore registerExtensions:completion:]` API.
{% endhint %}

```text
[AEPMobileCore registerExtensions:@[AEPMobileTarget.class] completion:nil];
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
[ACPTarget registerExtension];
```
{% endtab %}
{% endtabs %}

### retrieveLocationContent

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func retrieveLocationContent(_ requestArray: [TargetRequest], with targetParameters: TargetParameters? = nil)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
(void) retrieveLocationContent: (NSArray<AEPTargetRequestObject*>* _NonNull) requestsArray
                withParameters: (AEPTargetParameters* _Nullable) targetParameters;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) retrieveLocationContent: (nonnull NSArray<ACPTargetRequestObject*>*) requests
                  withParameters: (nullable ACPTargetParameters*) parameters;
```
{% endtab %}
{% endtabs %}

### setPreviewRestartDeepLink

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func setPreviewRestartDeepLink(_ deeplink: URL)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) setPreviewRestartDeeplink: (NSURL* _NonNull) deeplink;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) setPreviewRestartDeeplink: (nonnull NSURL*) deeplink;
```
{% endtab %}
{% endtabs %}

### setThirdPartyId

{% tabs %}
{% tab title="AEP 3.x \(Swift\)" %}
```swift
static func setThirdPartyId(_ id: String?)
```
{% endtab %}

{% tab title="AEP 3.x \(Objective-C\)" %}
```text
+ (void) setThirdPartyId: (NSString* _Nullable) thirdPartyId;
```
{% endtab %}

{% tab title="ACP 2.x \(Objective-C\)" %}
```text
+ (void) setThirdPartyId: (nullable NSString*) thirdPartyId;
```
{% endtab %}
{% endtabs %}

