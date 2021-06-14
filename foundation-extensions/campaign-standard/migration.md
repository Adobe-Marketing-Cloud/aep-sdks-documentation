# Migration to AEPCampaign

This document is a reference comparison of ACPCampaign (1.x) APIs against their equivalent APIs in AEPCampaign (3.x) for an iOS mobile application implementation.

The AEPCampaign extension is implemented purely in Swift and is compatible with the AEPCore swift SDK. To ensure a smooth transition from the ACPCampaign SDK, there are no major changes on the API names or definition. For more details, follow the migration guide below for your Swift or Objective-C mobile application. If explanation beyond showing API differences is necessary, it will be captured as an info hint within that API's section.

## Swift

### Public classes

| Type                   | AEP (3.x) | ACP (1.x)   |
| ---------------------- | :-------- | :---------- |
| Primary Class (Module) | Campaign  | ACPCampaign |

### API usages

{% tabs %}
{% tab title="AEP (3.x)" %}

**extensionVersion**

```swift
Campaign.extensionVersion
```

**registerExtension**

{% hint style="info" %}

Registration occurs by passing `AEPMobileCampaign` to the `[AEPMobileCore registerExtensions:completion:]` API.

{% endhint %}

```swift
MobileCore.registerExtensions([Campaign.self])
```

**resetLinkageFields**

```swift
Campaign.resetLinkageFields()
```

**setLinkageFields**

```swift
Campaign.setLinkageFields(linkageFields: ["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

{% endtab %}

{% tab title="ACP (1.x)" %}

**extensionVersion**

```swift
ACPCampaign.extensionVersion
```

**registerExtension**

```swift
ACPCampaign.registerExtension
```

**resetLinkageFields**

```swift
ACPCampaign.resetLinkageFields()
```

**setLinkageFields**

```swift
ACPCampaign.setLinkageFields(["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

{% endtab %}
{% endtabs %}

## Objective-C

### Public classes

| Type          | AEP (3.x)         | ACP (1.x)   |
| ------------- | :---------------- | :---------- |
| Primary Class | AEPMobileCampaign | ACPCampaign |

### API usages

{% tabs %}

{% tab title="AEP (3.x)" %}

**extensionVersion**

```objc
[AEPMobileCampaign extensionVersion];
```

**registerExtension**
{% hint style="info" %}
Registration occurs by passing `AEPMobileCampaign.class` to the `AEPMobileCore registerExtensions` API in addition to the other extensions registered.
{% endhint %}

```objc
[AEPMobileCore registerExtensions:@[..., AEPMobileCampaign.class] completion:^{
	// registration complete
}];
```

**resetLinkageFields**

```objc
[AEPMobileCampaign resetLinkageFields];
```

**setLinkageFields**

```swift
[AEPMobileCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

{% endtab %}

{% tab title="ACP (1.x)" %}

**extensionVersion**

```objc
[ACPCampaign extensionVersion];
```

**registerExtension**

```objc
[ACPCampaign registerExtension];
```

**resetLinkageFields**

```objc
[ACPCampaign resetLinkageFields];
```

**setLinkageFields**

```swift
[ACPCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

{% endtab %}
{% endtabs %}