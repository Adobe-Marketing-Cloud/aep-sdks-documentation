# Campaign API reference

This document contains usage information for the public functions and classes in `AEPCampaign`.

---

### extensionVersion

Returns the running version of the AEPCampaign extension.

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public String extensionVersion()
```

**Example**

```java
Campaign.extensionVersion();
```

{% endtab %}
{% tab title="iOS (AEP 3.x)" %}

**Syntax**

```swift
static var extensionVersion: String
```

**Example**

**Objective-C**

```objc
NSString *campaignVersion = [AEPMobileCampaign extensionVersion];
```

**Swift**

```swift
let campaignVersion = Campaign.extensionVersion
```

{% endtab %}

{% tab title="iOS (ACP 1.x)" %}

**Syntax**

```objc
+ (nonnull NSString*) extensionVersion;
```

**Example**

**Objective-C**

```objc
NSString *campaignVersion = [ACPCampaign extensionVersion];
```

**Swift**

```swift
let campaignVersion = ACPCampaign.extensionVersion()
```

{% endtab %}

{% tab title="React Native" %}

**Syntax**

```javascript
extensionVersion(): Promise<string>
```

**Example**

```javascript
ACPCampaign.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPCampaign version: " + version));
```

{% endtab %}

{% endtabs %}

---

### registerExtension

Registers the Campaign extension with the Mobile Core.

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public static void registerExtension()
```

**Example**

```java
Campaign.registerExtension();
```

{% endtab %}
{% tab title="iOS (AEP 3.x)" %}

This API no longer exists in `AEPCampaign`. Instead, the extension should be registered by calling the `registerExtensions` API in the MobileCore. Please see the updated SDK initialization steps at the [migrate to Swift tutorial.]({% endtab %}

{% endtab %}

{% tab title="iOS (ACP 1.x)" %}

**Syntax**

```objc
+ (void) registerExtension;
```

**Example**

**Objective-C**

```objc
[ACPCampaign registerExtension];
```

**Swift**

```swift
ACPCampaign.registerExtension()
```

{% endtab %}

{% tab title="React Native" %}

**Syntax**

```javascript
registerExtension()
```

**Example**

```javascript
ACPCampaign.registerExtension();
```

{% endtab %}

{% endtabs %}

---

### resetLinkageFields

Clears previously stored linkage fields in the mobile SDK and triggers a Campaign rules download request to the configured Campaign server.

This method unregisters any previously registered rules with the Rules Engine and clears cached rules from the most recent rules download.

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public static void resetLinkageFields()
```

**Example**

```java
Campaign.resetLinkageFields()
```

{% endtab %}
{% tab title="iOS (AEP 3.x)" %}

**Syntax**

```swift
static func resetLinkageFields()
```

**Example**

**Objective-C**

```objc
[AEPMobileCampaign resetLinkageFields];
```

**Swift**

```swift
Campaign.resetLinkageFields()
```

{% endtab %}

{% tab title="iOS (ACP 1.x)" %}

**Syntax**

```objc
+ (void) resetLinkageFields;
```

**Example**

**Objective-C**

```objc
[ACPCampaign resetLinkageFields];
```

**Swift**

```swift
ACPCampaign.resetLinkageFields()
```

{% endtab %}

{% tab title="React Native" %}

**Syntax**

```javascript
resetLinkageFields()
```

**Example**

```javascript
ACPCampaign.resetLinkageFields();
```

{% endtab %}

{% endtabs %}

---

### setLinkageFields

Sets the Campaign linkage fields (CRM IDs) in the mobile SDK to be used for downloading personalized messages from Campaign.

The set linkage fields are stored as a base64 encoded JSON string in memory and they are sent in a custom HTTP header `X-InApp-Auth`.

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public static void setLinkageFields(final Map<String, String> linkageFields)
```

**Example**

```java
HashMap<String, String> linkageFields = new HashMap<String, String>();
linkageFields.put("cusFirstName", "John");
linkageFields.put("cusLastName", "Doe");
linkageFields.put("cusEmail", "john.doe@email.com");
Campaign.setLinkageFields(linkageFields);
```

{% endtab %}
{% tab title="iOS (AEP 3.x)" %}

**Syntax**

```swift
static func setLinkageFields(linkageFields: [String: String])
```

**Example**

**Objective-C**

```objc
[AEPMobileCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

**Swift**

```swift
Campaign.setLinkageFields(linkageFields: ["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

{% endtab %}

{% tab title="iOS (ACP 1.x)" %}

**Syntax**

```objc
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

**Example**

**Objective-C**

```objc
[ACPCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

**Swift**

```swift
ACPCampaign.setLinkageFields(["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

{% endtab %}

{% tab title="React Native" %}

**Syntax**

```javascript
setLinkageFields(linkageFields: { string: string })
```

**Example**

```javascript
ACPCampaign.setLinkageFields({"firstName": "John"});
```

{% endtab %}

{% endtabs %}

---

