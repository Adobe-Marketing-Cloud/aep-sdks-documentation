# Migration to AEPTarget

This document is a reference comparison of ACPTarget (2.x) APIs against their equivalent APIs in AEPTarget (3.x) for an iOS mobile application implementation.

If an explanation beyond showing API differences is necessary, it will be captured as a "hint" within that API's section.

For example:

{% hint style="info" %}
This is information that is important to help clarify the API.
{% endhint %}

## Pod installation

| AEP (3.x)                    | ACP (2.x) |
| :----------------------------- | :-------------------------------------- |
| pod 'AEPTarget', '~&gt; 3.0' | pod 'ACPTarget', '~&gt; 2.0'    |
| pod 'AEPCore', '~&gt; 3.0'   | pod 'ACPCore', '~&gt; 2.0'              |

## Primary classes

{% tabs %}
{% tab title="Swift" %}

| AEP (3.x) | ACP (2.x) |
| :---------- | :-------------------------------------- |
| Target | ACPTarget                        |
| MobileCore  | ACPCore                                 |

{% endtab %}

{% tab title="Objective-C" %}

| AEP (3.x)       | ACP (2.x) |
| :---------------- | :-------------------------------------- |
| AEPMobileTarget | ACPTarget                        |
| AEPMobileCore     | ACPCore                                 |

{% endtab %}
{% endtabs %}

## Primary class

The class name containing public APIs is different depending on which SDK and language combination being used.

| SDK Version | Language    | Class Name        | Example                                 |
| ----------- | ----------- | ----------------- | --------------------------------------- |
| ACPTarget   | Objective-C | `ACPCTarget`      | `[ACPTarget clearPrefetchCache];`       |
| AEPTarget   | Objective-C | `AEPMobileTarget` | `[AEPMobileTarget clearPrefetchCache];` |
| AEPTarget   | Swift       | `Target`          | `Target.clearPrefetchCache()`           |

## Public APIs (alphabetical)

- [clearPrefetchCache](#clearPrefetchCache)
- [clickedLocation](#clickedLocation)
- [collectLaunchInfo (For enabling visual preview mode)](#Visual preview)
- [displayedLocations](#displayedLocations)
- [extensionVersion](#extensionVersion)
- [getThirdPartyId](#getThirdPartyId)
- [getTntId](#getTntId)
- [prefetchContent](#prefetchContent)
- [registerExtension](#registerExtension)
- [resetExperience](#resetExperience)
- [retrieveLocationContent](#retrieveLocationContent)
- [setPreviewRestartDeepLink](#setPreviewRestartDeepLink)
- [setThirdPartyId](#setThirdPartyId)

---

### clearPrefetchCache

{% tabs %}
{% tab title="ACPTarget (Objective-C)" %}

```objc
+ (void) clearPrefetchCache;
```

{% endtab %}

{% tab title="AEPTarget (Objective-C)" %}

```objc
+ (void) clearPrefetchCache;
```

{% endtab %}

{% tab title="AEPTarget (Swift)" %}

```swift
static func clearPrefetchCache
```

{% endtab %}

{% endtabs %}

---

### clickedLocation

{% tabs %}
{% tab title="ACPTarget (Objective-C)" %}

{% hint style="info" %}

The API was named `locationClicked` in the ACPTarget SDK.

{% endhint %}

```objc
+ (void) locationClickedWithName: (nonnull NSString*) name
                targetParameters: (nullable ACPTargetParameters*) parameters;
```

{% endtab %}

{% tab title="AEPTarget (Objective-C)" %}

```objc
+ (void) clickedLocation: (nonnull NSString*) name
                withTargetParameters: (nullable AEPTargetParameters*);
```

{% endtab %}

{% tab title="AEPTarget (Swift)" %}

```swift
static func clickedLocation(_ name: String, targetParameters: TargetParameters? = nil) 
```

{% endtab %}

{% endtabs %}

---

### 

### extensionVersion

{% tabs %}
{% tab title="ACPTarget (Objective-C)" %}

```objc
+ (nonnull NSString*) extensionVersion;
```

{% endtab %}

{% tab title="AEPTarget (Objective-C)" %}

```objc
+ (nonnull NSString*) extensionVersion;
```

{% endtab %}

{% tab title="AEPTarget (Swift)" %}

```swift
static var extensionVersion: String
```

{% endtab %}

{% endtabs %}

---

### registerExtension

{% tabs %}
{% tab title="ACPTarget (Objective-C)" %}

```objc
+ (void) registerExtension;
```

{% endtab %}

{% tab title="AEPTarget (Objective-C)" %}

{% hint style="info" %}

Registration occurs by passing `AEPMobileTarget` to the `[AEPMobileCore registerExtensions:completion:]` API.

```objc
[AEPMobileCore registerExtensions:@[AEPMobileTarget.class] completion:nil];
```

{% endtab %}

{% tab title="AEPTarget (Swift)" %}

{% hint style="info" %}

Registration occurs by passing `Target` to the `MobileCore.registerExtensions` API.

{% endhint %}

```swift
MobileCore.registerExtensions([Target.self])
```

{% endtab %}

{% endtabs %}

---



