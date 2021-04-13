# Privacy and GDPR

The Adobe Experience Platform SDKs give you controls to manage consent and privacy obligations under the European Union's General Data Protection Regulation \(GDPR\). Developers can retrieve locally stored identities and set opt status flags for data collection and transmission.

Before implementing these controls, read Adobe's [GDPR documentation](https://www.adobe.io/apis/cloudplatform/gdpr.html).

When Adobe provides software and services to an enterprise, Adobe acts as a data processor for any personal data it processes and stores as part of providing these services. As a data processor, Adobe processes personal data in accordance with your company’s permission and instructions, as set out in your agreement with Adobe. As a data controller, you can use the Experience Platform SDKs to support GDPR retrieve and delete requests from your mobile apps.

> **Note:** Collect consent is supported starting with v1.1.0 of the Edge network extension. Implementations using Edge Network extension v1.0.0 should adhere to privacy status settings. More information can be found [here](https://aep-sdks.gitbook.io/docs/resources/privacy-and-gdpr#set-and-get-privacy-status).

## Update and get collect consent preferences

You can set the collect consent status to ensure collection of data suits your user's preferences.

| Extension | Collect (y) | Collect (n) | Collect (pending) |
| :--- | :--- | :--- | :--- |
| **Edge Network** | Hits are sent | Hits not sent | Hits queued |

> **Note:** When no default collect consent value is defined in configuration, the SDK defaults to Yes (y) for collect consent.

### Collect Consent settings

{% tabs %}
{% tab title="Android" %}
#### Java

You can set the collect consent to one of the following values:

* `y`
* `n`

To understand the expected behavior, see the *Update and get collect consent preferences* table above.
{% endtab %}

{% tab title="iOS" %}
You can set the collect consent to one of the following values:

#### Swift

* `y`
* `n`

#### Objective-C

You can set the collect consent to one of the following values:

* `y`
* `n`

To understand the expected behavior, see the *Update and get collect consent preferences* table above.
{% endtab %}
{% endtabs %}

### getConsents<a id="getconsents"></a>

{% tabs %}
{% tab title="Android" %}

#### Java

#### Syntax

```objectivec
public static void getConsents(final AdobeCallback<Map<String, Object>> callback);
```

* _callback_ - callback invoked with the current consents of the extension. If an `AdobeCallbackWithError` is provided, an `AdobeError`, can be retruned in the eventuality of any error that occured while getting the user consents. The callback may be invoked on a different thread.

#### Example

```objectivec
Consent.getConsents(new AdobeCallback<Map<String, Object>>() {
	@Override
	public void call(Map<String, Object> currentConsents) {
		if (currentConsents == null) { return; }
    final Map<String, Object> consents = currentConsets.get("consents");
    final Map<String, Object> collectConsent = consents.get("collect");
    final String collectConsentStatus = collectConsent.get("val");
    // inspect collectConsentStatus
	}
});
```

{% endtab %}

{% tab title="iOS" %}

#### Swift

#### Syntax

```swift
static func getConsents(completion: @escaping ([String: Any]?, Error?) -> Void)
```

#### Example

```swift
Consent.getConsents { currentConsents, error in
	guard error == nil else { return }
	guard let consents = currentConsents["consents"] as? [String: Any] else { return }
	guard let collectConsent = consents["collect"] as? [String: Any] else { return }
	let collectConsentStatus = collectConsent["val"] as? String
  // inspect collectConsentStatus
}
```

#### Objective-C

#### Syntax

```text
static func getConsents(completion: @escaping ([String: Any]?, Error?) -> Void)
```

#### Example

```objective-c
[AEPMobileEdgeConsent getConsents:^(NSDictionary *currentConsents, NSError *error) {
	if (error) { return; }
	NSDictionary *consents = currentConsents[@"consents"];
  NSDictionary *collectConsent = currentConsents[@"collect"];
  NSString *collectConsentStatus = collectConsent[@"val"];
  // inspect collectConsentStatus
}];
```

{% endtab %}
{% endtabs %}

### updateConsents<a id="updateconsent"></a>

To programmatically update the consent collect for the application user:

> **Note:** After a user has selected collect consent no (n), the SDK will not allow you to set the users collect consent to yes (y).

{% tabs %}
{% tab title="Android" %}

#### Java

#### Syntax

```java
public static void update(final Map<String, Object> consents);
```

#### Example

```java
// example 1, updating users collect consent to 'yes'
final Map<String, Object> collectConsents = new HashMap<>();
collectConsents.put("collect", new HashMap<String, String>() {
	{
		put("val", "y");
	}
});

final Map<String, Object> consents = new HashMap<>();
consents.put("consents", collectConsents);

Consent.update(consents);

// example 2, updating users collect consent to 'no'
final Map<String, Object> collectConsents = new HashMap<>();
collectConsents.put("collect", new HashMap<String, String>() {
	{
		put("val", "n");
	}
});

final Map<String, Object> consents = new HashMap<>();
consents.put("consents", collectConsents);

Consent.update(consents);
```
{% endtab %}

{% tab title="iOS" %}
#### Swift

#### Syntax

```swift
static func update(with consents: [String: Any])
```

#### Example

```swift
// example 1, updating users collect consent to 'yes'
let collectConsent = ["collect": ["val": "y"]]
let currentConsents = ["consents": collectConsent]
Consent.update(with: currentConsents)

// example 2, updating users collect consent to 'no'
let collectConsent = ["collect": ["val": "n"]]
let currentConsents = ["consents": collectConsent]
Consent.update(with: currentConsents)
```

#### Objective-C

#### Syntax

```swift
static func update(with consents: [String: Any])
```

#### Example

```objective-c
// example 1, updating users collect consent to 'yes'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"y"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConsent}];

// example 2, updating users collect consent to 'no'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"n"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConsent}];
```
{% endtab %}
{% endtabs %}

You can also programmatically view the current collect consent preferences status by using the following:

{% hint style="info" %}
The following API returns a dictionary representation of the consent preferences for the user.
{% endhint %}

## Retrieving stored identifiers

When using the Edge Network extensions, use the [Identity.getIdentities](../using-mobile-extensions/adobe-edge-identity/edge-identity-api-reference.md#getidentities) API to retrieve all the identifier data stored locally by the SDK and send this data to your servers.

When using both Edge Network extension and Adobe Solutions extensions,  use both [Identity.getIdentities](../using-mobile-extensions/adobe-edge-identity/edge-identity-api-reference.md#getidentities) API and [MobileCore.getSdkIdentities](../using-mobile-extensions/mobile-core/mobile-core-api-reference.md#retrieving-stored-identifiers) API  to retrieve all the identifier data stored locally by the SDK and send this data to your servers.

## Configuration keys

To update the SDK configuration, programmatically, use the following information to change your default consent values. For more information, see [Configuration API reference](../using-mobile-extensions/mobile-core/configuration/configuration-api-reference.md).

| Key | Description |
| :--- | :--- |
| `consent.default` | Defines the set of default consent preferences for the SDK in XDM format. For more details, see [Privacy/Personalization/Marketing Preferences (Consents) Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-consents.schema.md). |

## Additional information

* For more information about GDPR, see [GDPR and Your Business](https://www.adobe.com/privacy/general-data-protection-regulation.html)
* To see the GDPR API documentation, go to [General Data Protection Regulation API](https://adobe.io/apis/cloudplatform/gdpr.html)

