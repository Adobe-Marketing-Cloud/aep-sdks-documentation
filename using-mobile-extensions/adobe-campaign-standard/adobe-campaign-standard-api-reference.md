# Adobe Campaign Standard API reference

## Set linkage fields

Allows Campaign to connect fields from separate databases and create a more developed and personalized messaging experience. Profile template-based messages that contain PII-based personalization are downloaded. The **linkage fields** are stored as a base64-encoded JSON string in memory and sent in a custom HTTP header, `X-InApp-Auth`, in all future Campaign rules download requests until `ACPCampaign::resetLinkageFields` is invoked. The **linkage fields** are cleared when the app is gracefully closed, crashed, or the privacy status is changed to opt out. For more information, see [Preparing and sending an In-App message](https://helpx.adobe.com/campaign/standard/channels/using/preparing-and-sending-an-in-app-message.html).

{% tabs %}
{% tab title="iOS" %}
### setLinkageFields

#### Syntax

```objectivec
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

#### Objective-C

#### Example

```objectivec
[ACPCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

#### Swift

```swift
var linkageFields = [String: String]()
linkageFields["cusFirstName"] = "John"
linkageFields["cusLastName"] = "Doe"
linkageFields["cusEmail"] = "john.doe@email.com"
ACPCampaign.setLinkageFields(linkageFields)
```
{% endtab %}
{% endtabs %}

## Reset linkage fields

Removes the previously stored linkage fields in the SDK and triggers the Campaign rules download again. Personalized messages stored in cache before are erased.

{% tabs %}
{% tab title="iOS" %}
### resetLinkageFields

#### Syntax

```objectivec
+ (void) resetLinkageFields;
```

#### Objective-C

#### Example

```objectivec
[ACPCampaign resetLinkageFields];
```

#### Swift

```swift
ACPCampaign.resetLinkageFields();
```
{% endtab %}
{% endtabs %}

