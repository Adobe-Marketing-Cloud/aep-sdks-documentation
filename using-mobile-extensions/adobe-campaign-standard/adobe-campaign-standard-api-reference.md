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

{% tab title="iOS \(AEP 3.x\)" %}
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

**Example**

```text
NSString *campaignVersion = [AEPMobileCampaign extensionVersion];
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

{% tab title="iOS \(AEP 3.x\)" %}
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

**Example**

```text
[AEPMobileCampaign resetLinkageFields];
```
{% endtab %}
{% endtabs %}

## setLinkageFields

Sets the Campaign linkage fields \(CRM IDs\) in the mobile SDK to be used for downloading personalized messages from Campaign.

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

{% tab title="iOS \(AEP 3.x\)" %}
### Swift

**Syntax**

```swift
static func setLinkageFields(linkageFields: [String: String])
```

**Example**

```swift
Campaign.setLinkageFields(linkageFields: ["cusFirstName": "John", "cusLastName": "Doe", "cusEmail": "john.doe@email.com"])
```

### Objective-C

**Example**

```text
[AEPMobileCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```
{% endtab %}
{% endtabs %}

