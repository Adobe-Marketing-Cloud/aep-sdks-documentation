# Migration to AEPCampaign

This document is a reference comparison of ACPCampaign (1.x) APIs against their equivalent APIs in AEPCampaign (3.x) for an iOS mobile application implementation.

If an explanation beyond showing API differences is necessary, it will be captured as a "hint" within that API's section.

For example:

{% hint style="info" %}
This is information that is important to help clarify the API.
{% endhint %}

## Pod installation

| AEP (3.x)                    | ACPCore (2.x) and ACPCampaign (1.x) |
| :----------------------------- | :-------------------------------------- |
| pod 'AEPCampaign', '~&gt; 3.0' | pod 'ACPCampaign', '~&gt; 1.0'          |
| pod 'AEPCore', '~&gt; 3.2.0'   | pod 'ACPCore', '~&gt; 2.0'              |

## Primary classes

{% tabs %}
{% tab title="Swift" %}

| AEP (3.x) | ACPCore (2.x) and ACPCampaign (1.x) |
| :---------- | :-------------------------------------- |
| Campaign    | ACPCampaign                             |
| MobileCore  | ACPCore                                 |

{% endtab %}

{% tab title="Objective-C" %}

| AEP (3.x)       | ACPCore (2.x) and ACPCampaign (1.x) |
| :---------------- | :-------------------------------------- |
| AEPMobileCampaign | ACPCampaign                             |
| AEPMobileCore     | ACPCore                                 |

{% endtab %}
{% endtabs %}

## Primary class

The class name containing public APIs is different depending on which SDK and language combination being used.

| SDK Version | Language    | Class Name          | Example                                   |
| ----------- | ----------- | ------------------- | ----------------------------------------- |
| ACPCampaign | Objective-C | `ACPCampaign`       | `[ACPCampaign resetLinkageFields];`       |
| AEPCampaign | Objective-C | `AEPMobileCampaign` | `[AEPMobileCampaign resetLinkageFields];` |
| AEPCampaign | Swift       | `Campaign`          | `Campaign.resetLinkageFields()`           |

## Public APIs (alphabetical)

- [extensionVersion](#extensionVersion)
- [registerExtension](#registerExtension)
- [resetLinkageFields](#resetLinkageFields)
- [setLinkageFields](#setLinkageFields)

---

### extensionVersion

{% tabs %}
{% tab title="ACPCampaign (Objective-C)" %}

```objc
+ (nonnull NSString*) extensionVersion;
```

{% endtab %}

{% tab title="AEPCampaign (Objective-C)" %}

```objc
+ (nonnull NSString*) extensionVersion;
```

{% endtab %}

{% tab title="AEPCampaign (Swift)" %}

```swift
static var extensionVersion: String
```

{% endtab %}

{% endtabs %}

---

### registerExtension

{% tabs %}
{% tab title="ACPCampaign (Objective-C)" %}

```objc
+ (void) registerExtension;
```

{% endtab %}

{% tab title="AEPCampaign (Objective-C)" %}

{% hint style="info" %}

Registration occurs by passing `AEPMobileCampaign` to the `[AEPMobileCore registerExtensions:completion:]` API.

{% endhint %}

```objc
[AEPMobileCore registerExtensions:@[AEPMobileCampaign.class] completion:nil];
```

{% endtab %}

{% tab title="AEPCampaign (Swift)" %}

{% hint style="info" %}

Registration occurs by passing `Campaign` to the `MobileCore.registerExtensions` API.

{% endhint %}

```swift
MobileCore.registerExtensions([Campaign.self])
```

{% endtab %}

{% endtabs %}

---

### resetLinkageFields

{% tabs %}
{% tab title="ACPCampaign (Objective-C)" %}

```objc
+ (void) resetLinkageFields;
```

{% endtab %}

{% tab title="AEPCampaign (Objective-C)" %}

```objc
+ (void) resetLinkageFields;
```

{% endtab %}

{% tab title="AEPCampaign (Swift)" %}

```swift
static func resetLinkageFields()
```

{% endtab %}

{% endtabs %}

---

### setLinkageFields

{% tabs %}
{% tab title="ACPCampaign (Objective-C)" %}

```objc
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

{% endtab %}

{% tab title="AEPCampaign (Objective-C)" %}

```objc
+ (void) setLinkageFields: (NSDictionary<NSString*, NSString*>* _NonNull);
```

{% endtab %}

{% tab title="AEPCampaign (Swift)" %}

```swift
static func setLinkageFields(linkageFields: [String: String])
```

{% endtab %}

{% endtabs %}

---

For more information, please see the [Campaign API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard/adobe-campaign-standard-api-reference).