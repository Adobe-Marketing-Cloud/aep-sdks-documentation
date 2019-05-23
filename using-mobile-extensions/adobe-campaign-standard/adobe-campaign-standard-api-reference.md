# Adobe Campaign Standard API reference

## Get extension version

Get the extension version

{% tabs %}
{% tab title="Android" %}

{% endtab %}

{% tab title="iOS" %}

{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```javascript
ACPCampaign.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPCampaign version: " + version));
```
{% endtab %}
{% endtabs %}

## Set linkage fields

Allows Campaign to connect fields from separate databases and create a more developed and personalized messaging experience. Profile template-based messages that contain PII-based personalization are downloaded. The linkage fields are stored as a base64-encoded JSON string in memory and sent in a custom HTTP header, `X-InApp-Auth`, in all future Campaign rules download requests until `ACPCampaign::resetLinkageFields` is invoked. The linkage fields are cleared when the app is gracefully closed, crashed, or the privacy status is changed to opt out. For more information, see [Preparing and sending an In-App message](https://helpx.adobe.com/campaign/standard/channels/using/preparing-and-sending-an-in-app-message.html).

{% tabs %}
{% tab title="Android" %}
### Syntax

```java
public void setLinkageFields(final Map<String, String> linkageFields)
```

### Example

```java
HashMap<String, String> linkageFields = new HashMap<String, String>();
linkageFields.put("cusFirstName", "John");
linkageFields.put("cusLastName", "Doe");
linkageFields.put("cusEmail", "john.doe@email.com");
Campaign.setLinkageFields(linkageFields);
```
{% endtab %}

{% tab title="iOS" %}
### Syntax

```objectivec
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

### Objective-C

### Example

```objectivec
[ACPCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

### Swift

```swift
var linkageFields = [String: String]()
linkageFields["cusFirstName"] = "John"
linkageFields["cusLastName"] = "Doe"
linkageFields["cusEmail"] = "john.doe@email.com"
ACPCampaign.setLinkageFields(linkageFields)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```javascript
ACPCampaign.setLinkageFields({"linkageKey": "linkageValue"});
```
{% endtab %}
{% endtabs %}

## Reset linkage fields

Removes the previously stored linkage fields in the SDK and triggers the Campaign rules download again. Personalized messages stored in cache before are erased.

{% tabs %}
{% tab title="Android" %}
### Syntax

```java
public void resetLinkageFields()
```

### Example

```java
Campaign.resetLinkageFields()
```
{% endtab %}

{% tab title="iOS" %}
### Syntax

```objectivec
+ (void) resetLinkageFields;
```

### Objective-C

### Example

```objectivec
[ACPCampaign resetLinkageFields];
```

### Swift

```swift
ACPCampaign.resetLinkageFields();
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```javascript
ACPCampaign.resetLinkageFields();
```
{% endtab %}
{% endtabs %}

