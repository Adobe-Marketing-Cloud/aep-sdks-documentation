# Adobe Campaign Standard API reference

## Version of the Campaign Standard extension

The `extensionVersion()` API returns the version of the Campaign Standard extension that is registered with the Mobile Core extension.

To get the version of the Campaign Standard extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
#### Java

#### Syntax

```java
public String extensionVersion()
```

#### Example

```java
Campaign.extensionVersion();
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (nonnull NSString*) extensionVersion;
```

#### Examples

#### Objective C

```objectivec
NSLog(@"ACPCampaign version: %@", [ACPCampaign extensionVersion]);
```

#### Swift

```swift
print("ACPCampaign version: ", ACPCampaign.extensionVersion())
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

#### Syntax

```javascript
extensionVersion(): Promise<string>
```

#### Example

```javascript
ACPCampaign.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPCampaign version: " + version));
```
{% endtab %}
{% endtabs %}

## resetLinkageFields

This method clears the cached rules from the previous download before triggering a rule download request to the configured Campaign server. If the current SDK privacy status is not OPT\_IN, no rules download occurs.

{% tabs %}
{% tab title="Android" %}
#### Java

#### Syntax

```java
public static void resetLinkageFields()
```

#### Example

```java
Campaign.resetLinkageFields()
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (void) resetLinkageFields;
```

#### Objective C

#### Example

```objectivec
[ACPCampaign resetLinkageFields];
```

#### Swift

```swift
ACPCampaign.resetLinkageFields()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

#### Syntax

```javascript
resetLinkageFields();
```

#### Example

```javascript
ACPCampaign.resetLinkageFields();
```
{% endtab %}
{% endtabs %}

## setLinkageFields

This API sets the Campaign linkage fields \(CRM IDs\) in the Mobile SDK that are used to download personalized messages from Campaign. The set linkage fields are stored as a base64-encoded JSON string in memory, and they are sent in a custom HTTP header `X-InApp-Auth` in all future Campaign rules download requests until `resetLinkageFields` is invoked. These in-memory variables are lost in the following scenarios:

* When an application crash event occurs.
* After a graceful termination of the application.
* When the privacy status is updated to `OPT_OUT`.  For more information, see [Set and Get Privacy Status](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr#set-and-get-privacy-status)

For more information about setting up linkage fields in Campaign, see [Extending the subscriptions to an application resource](https://docs.adobe.com/content/help/en/campaign-standard/using/developing/use-cases--extending-resources/extending-the-subscriptions-to-an-application-resource.html).

{% tabs %}
{% tab title="Android" %}
#### Java

#### Syntax

```java
public static void setLinkageFields(final Map<String, String> linkageFields)
```

* _linkageFields_ is a map that contains the linkage field key-value pairs.

#### Example

```java
HashMap<String, String> linkageFields = new HashMap<String, String>();
linkageFields.put("cusFirstName", "John");
linkageFields.put("cusLastName", "Doe");
linkageFields.put("cusEmail", "john.doe@email.com");
Campaign.setLinkageFields(linkageFields);
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

* _linkageFields_ is a dictionary that contains the linkage field key-value pairs.

#### Examples

#### Objective C

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

{% tab title="React Native" %}
#### JavaScript

#### Syntax

```javascript
setLinkageFields(linkageFields: { string: string })
```

* _linkageFields_ is a map that contains the linkage field key-value pairs.

#### Example

```javascript
ACPCampaign.setLinkageFields({"firstName": "John"});
```
{% endtab %}
{% endtabs %}

