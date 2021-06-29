# Adobe Campaign Standard API reference

---

### extensionVersion

Returns the running version of the Campaign extension.

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

**Swift**

```swift
let campaignVersion = Campaign.extensionVersion
```

**Objective-C**

```objc
NSString *campaignVersion = [AEPMobileCampaign extensionVersion];
```

{% endtab %}

{% tab title="iOS (ACP 1.x)" %}

**Syntax**

```objc
+ (nonnull NSString*) extensionVersion;
```

**Example**

**Swift**

```swift
let campaignVersion = ACPCampaign.extensionVersion()
```

**Objective-C**

```objc
NSString *campaignVersion = [ACPCampaign extensionVersion];
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

This API no longer exists in `Campaign`. Instead, the extension should be registered by calling the `registerExtensions` API in the MobileCore. Please see the updated SDK initialization steps at the [migrate to Swift tutorial](https://aep-sdks.gitbook.io/docs/resources/migrate-to-swift).

{% endtab %}

{% tab title="iOS (ACP 1.x)" %}

**Syntax**

```objc
+ (void) registerExtension;
```

**Example**

**Swift**

```swift
ACPCampaign.registerExtension()
```

**Objective-C**

```objc
[ACPCampaign registerExtension];
```

{% endtab %}

{% tab title="React Native" %}

When using React Native, register the Campaign extension with Mobile Core in native code as shown on the Android and iOS tabs.

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

**Swift**

```swift
Campaign.resetLinkageFields()
```

**Objective-C**

```objc
[AEPMobileCampaign resetLinkageFields];
```

{% endtab %}

{% tab title="iOS (ACP 1.x)" %}

**Syntax**

```objc
+ (void) resetLinkageFields;
```

**Example**

**Swift**

```swift
ACPCampaign.resetLinkageFields()
```

**Objective-C**

```objc
[ACPCampaign resetLinkageFields];
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

**Swift**

```swift
Campaign.setLinkageFields(linkageFields: ["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

**Objective-C**

```objc
[AEPMobileCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

{% endtab %}

{% tab title="iOS (ACP 1.x)" %}

**Syntax**

```objc
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

**Example**

**Swift**

```swift
ACPCampaign.setLinkageFields(["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

**Objective-C**

```objc
[ACPCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
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

