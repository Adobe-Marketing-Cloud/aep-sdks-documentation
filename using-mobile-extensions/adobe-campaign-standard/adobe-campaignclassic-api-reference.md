# Campaign API reference

## Set linkage fields

Allows Campaign to connect fields from separate databases and create a more developed and personalized messaging experience. Profile template-based messages that contain PII-based personalization are downloaded. 

{% tabs %}

{% tab title="iOS" %}
### setLinkageFields


#### Syntax

```objectivec
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

#### Objective-C

The **linkage fields** are stored as a base64-encoded JSON string in memory and sent in a custom HTTP header 'X-InApp-Auth' in all future Campaign rules download requests until ACPCampaign::resetLinkageFields is invoked.

#### Example

```objectivec
[ACPCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

#### Swift

```swift
ACPCampaign.setLinkageFields(linkageFields[String:String]);
```
{% endtab %}
{% endtabs %}

## Reset Linkage fields

Removes the previously stored linkage fields in the SDK and triggers the Campaign rules download again.

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


