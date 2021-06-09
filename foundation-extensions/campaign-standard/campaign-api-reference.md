# Campaign API Reference

This document contains usage information for the public functions and classes in `AEPCampaign`.

## Static functions

- [extensionVersion](#extensionVersion)
- [registerExtension](#registerExtension)
- [resetLinkageFields](#resetLinkageFields)
- [setLinkageFields](#setLinkageFields)

<hr />

### extensionVersion

Returns the running version of the AEPCampaign extension.

**Signature**

{% tabs %}
{% tab title="Swift" %}

```swift
static var extensionVersion: String
```

**Example usage**

```swift
let campaignVersion = Campaign.extensionVersion
```

{% endtab %}

{% tab title="Objective-C" %}

**Signature**

```objc
+ (nonnull NSString*) extensionVersion;
```

**Example usage**

```objc
NSString *campaignVersion = [AEPMobileCampaign extensionVersion];
```

{% endtab %}

{% endtabs %}

<hr />

### registerExtension

This API no longer exists in `AEPCampaign`. Instead, the extension should be registered by calling the `registerExtensions` API in the MobileCore. Please see the updated SDK initialization steps at the [migrate to Swift tutorial.](../../resources/migrate-to-swift.md#update-sdk-initialization)

{% tabs %}
{% tab title="Swift" %}

**Example:**

```swift
MobileCore.registerExtensions([Campaign.self, ...], {
  // processing after registration
})
```

{% endtab %}

{% tab title="Objective-C" %}

**Example:**

```objc
[AEPMobileCore registerExtensions:@[AEPMobileCampaign.class, ...] completion:^{
  // processing after registration
}];
```

{% endtab %}

{% endtabs %}

<hr />

### resetLinkageFields

Clears previously stored linkage fields in the mobile SDK and triggers a Campaign rules download request to the configured Campaign server.

This method unregisters any previously registered rules with the Rules Engine and clears cached rules from the most recent rules download.

{% tabs %}
{% tab title="Swift" %}

**Signature**

```swift
static func resetLinkageFields()
```

**Example usage**

```swift
Campaign.resetLinkageFields()
```

{% endtab %}

{% tab title="Objective-C" %}

**Signature**

```objc
+ (void) resetLinkageFields;
```

**Example usage**

```objc
[AEPMobileCampaign resetLinkageFields];
```

{% endtab %}

{% endtabs %}

<hr />

### setLinkageFields

Sets the Campaign linkage fields (CRM IDs) in the mobile SDK to be used for downloading personalized messages from Campaign.

The set linkage fields are stored as a base64 encoded JSON string in memory and they are sent in a custom HTTP header `X-InApp-Auth`.

{% tabs %}
{% tab title="Swift" %}

**Signature**

```swift
static func setLinkageFields(linkageFields: [String: String])
```

**Example usage**

```swift
Campaign.setLinkageFields(linkageFields: ["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

{% endtab %}

{% tab title="Objective-C" %}

**Signature**

```objc
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

**Example usage**

```objc
[AEPMobileCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

{% endtab %}

{% endtabs %}

<hr />

