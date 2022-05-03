# Adobe Campaign Standard API reference

## extensionVersion

Returns the running version of the Campaign Standard extension.

{% tabs %}
{% tab title="Android" %}
### Java

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
### Swift

**Syntax**

```swift
static var extensionVersion: String
```

**Example**

```swift
let campaignVersion = Campaign.extensionVersion
```

### Objective-C

**Syntax**

```objective-c
+ (NSString * _Nonnull)extensionVersion
```

**Example**

```objective-c
NSString *campaignVersion = [AEPMobileCampaign extensionVersion];
```
{% endtab %}

{% tab title="iOS (ACP 1.x)" %}
### Swift

**Syntax**

```swift
+ (nonnull NSString*) extensionVersion;
```

**Example**

```swift
let campaignVersion = ACPCampaign.extensionVersion()
```

### Objective-C

**Syntax**

```objective-c
+ (NSString * _Nonnull)extensionVersion
```

**Example**

```objective-c
NSString *campaignVersion = [ACPCampaign extensionVersion];
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

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

## registerExtension

Registers the Campaign Standard extension with the Mobile Core.

{% tabs %}
{% tab title="Android" %}
### Java

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

This API no longer exists in the AEP 3.x Adobe Campaign Standard extension. Instead, the extension should be registered by calling the `registerExtensions` API in the MobileCore. Please see the updated SDK initialization steps at the [migrate to Swift tutorial](https://aep-sdks.gitbook.io/docs/resources/migrate-to-swift).

{% endtab %}

{% tab title="iOS (ACP 1.x)" %}

### Swift

**Syntax**

```swift
+ (void) registerExtension
```

**Example**

```swift
ACPCampaign.registerExtension()
```

### Objective-C

**Syntax**

```objective-c
+ (void) registerExtension
```

**Example**

```objective-c
[ACPCampaign registerExtension];
```
{% endtab %}

{% tab title="React Native" %}
When using React Native, register the Adobe Campaign Standard extension with Mobile Core in native code as shown on the Android and iOS tabs.
{% endtab %}
{% endtabs %}

## resetLinkageFields

Clears previously stored linkage fields in the mobile SDK and triggers a Campaign rules download request to the configured Campaign server.

This method unregisters any previously registered rules with the Rules Engine and clears cached rules from the most recent rules download.

{% tabs %}
{% tab title="Android" %}
### Java

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
### Swift

**Syntax**

```swift
static func resetLinkageFields()
```

**Example**

```swift
Campaign.resetLinkageFields()
```

### Objective-C

**Syntax**

```objective-c
+ (void) resetLinkageFields
```

**Example**

```objective-c
[AEPMobileCampaign resetLinkageFields];
```
{% endtab %}

{% tab title="iOS (ACP 1.x)" %}
### Swift

**Syntax**

```swift
+ (void) resetLinkageFields
```

**Example**

```swift
ACPCampaign.resetLinkageFields()
```

### Objective-C

**Syntax**

```objective-c
+ (void) resetLinkageFields
```

**Example**

```objective-c
[ACPCampaign resetLinkageFields];
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

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

## setLinkageFields

Sets the Campaign linkage fields (CRM IDs) in the mobile SDK to be used for downloading personalized messages from Campaign.

The set linkage fields are stored as a base64 encoded JSON string in memory and they are sent in a custom HTTP header `X-InApp-Auth`.

{% tabs %}
{% tab title="Android" %}
### Java

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
### Swift

**Syntax**

```swift
static func setLinkageFields(_ linkageFields: [String: String])
```

**Example**

```swift
Campaign.setLinkageFields(linkageFields: ["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

### Objective-C

**Syntax**

```objective-c
+ (void) setLinkageFields:(NSDictionary<NSString *,NSString *> * _Nonnull)
```

**Example**

```objective-c
[AEPMobileCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```
{% endtab %}

{% tab title="iOS (ACP 1.x)" %}
### Swift

**Syntax**

```swift
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields
```

**Example**

```swift
ACPCampaign.setLinkageFields(["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

### Objective-C

**Syntax**

```objective-c
+ (void) setLinkageFields: (NSDictionary<NSString*, NSString*>*) linkageFields
```

**Example**

```objective-c
[ACPCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

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

