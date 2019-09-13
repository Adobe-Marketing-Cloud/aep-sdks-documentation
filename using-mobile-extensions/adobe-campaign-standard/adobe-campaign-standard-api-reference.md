# Adobe Campaign Standard API reference

## Get the extension version

To return the current version of the ACPCampaign extension, use the following APIs:

{% tabs %}
{% tab title="Android" %}
#### Java

#### Example

```java
Campaign.getExtensionVersion();
```
{% endtab %}

{% tab title="iOS" %}
### extensionVersion

#### Objective-C

#### Syntax

```objectivec
+ (nonnull NSString*) extensionVersion;
```

#### Example

```objectivec
NSLog([ACPCore extensionVersion]);
```

#### Swift

#### Syntax

```swift
class func extensionVersion() -> String {}
```

#### Example

```swift
print(ACPCore.extensionVersion());
```
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

Removes the previously stored linkage fields in the SDK and triggers the Campaign rules download again. Personalized messages that were previously stored in the cache are erased.

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

## Set up push messaging

{% tabs %}
{% tab title="Android" %}
### setPushIdentifier

#### Syntax

```java
void setPushIdentifier(final String registrationID)
```

#### Example

```java
MobileCore.setPushIdentifier(registrationID);
```
{% endtab %}

{% tab title="iOS" %}
### setPushIdentifier

#### Objective-C

#### Syntax

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

#### Example

```objectivec
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  // Set the deviceToken that the APNS has assigned to the device
  [ACPCore setPushIdentifier:deviceToken];
  //...
}
```

#### Swift

```swift
ACPCore.setPushIdentifier(deviceToken)
```
{% endtab %}

{% tab title="React Native" %}
### setPushIdentifier

#### JavaScript

```javascript
ACPCore.setPushIdentifier("pushIdentifier");
```
{% endtab %}
{% endtabs %}

