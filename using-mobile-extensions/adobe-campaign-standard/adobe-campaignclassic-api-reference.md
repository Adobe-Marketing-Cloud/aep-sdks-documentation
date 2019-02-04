# Campaign API reference

## Set linkage fields

Allows the Campaign to connect fields from separate databases to create a more developed and personalized messaging experience for their end user. Profile template based messages that can contain PII based personalization will be downloaded. 

{% tabs %}

{% tab title="iOS" %}
### setLinkageFields


#### Syntax

```objectivec
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

#### Objective-C

The set linkage fields are stored as base64 encoded JSON string in memory and sent in a custom HTTP header 'X-InApp-Auth' in all future Campaign rules download requests until ACPCampaign::resetLinkageFields is invoked.

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

Removes previously stored linkage fields in the mobile SDK and re-triggers Campaign rules download.

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


