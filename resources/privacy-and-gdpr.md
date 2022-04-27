# Privacy and GDPR

The Adobe Experience Platform SDKs give you controls to manage consent and privacy obligations, such as the European Union's General Data Protection Regulation \(GDPR\). Developers can retrieve locally stored identities and set opt status flags for data collection and transmission.

Before implementing these controls, read the [Adobe Experience Platform Privacy Service documentation](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html).

When Adobe provides software and services to an enterprise, Adobe acts as a data processor for any personal data it processes and stores as part of providing these services. As a data processor, Adobe processes personal data in accordance with your company’s permission and instructions, as set out in your agreement with Adobe. As a data controller, you can use the Experience Platform SDKs to support privacy retrieve and delete requests from your mobile apps.

# Setup steps

The following sections provide details on how you can collect consent and privacy status to ensure collection of data suits your user's preferences.

Depending on the mobile extensions you use, there are two ways of collecting and enforcing consent preferences when using the Experience Platform SDKs:

1. When using the **Edge Network** mobile extensions, you should use the [Consent for Edge Network](../foundation-extensions/consent-for-edge-network) extension.
2. When using **Adobe Experience Cloud** mobile extensions, you should use privacy status settings.

The two options are documented in detail below.

{% hint style="info" %}
If you are using a mix of Edge Network and Adobe Experience Cloud mobile extensions, please follow the steps for configuring both consent and privacy status settings. See also the [frequently asked questions](../foundation-extensions/identity-for-edge-network/identity-faq.md) about consent and privacy settings or identities.
{% endhint %}

## Using Experience Platform SDKs for Edge Network

## Update and get collect consent preferences

You can set the collect consent status to ensure collection of data suits your user's preferences.

| Extension        | Collect (y)   | Collect (n)       | Collect (pending) |
| :--------------- | :------------ | :---------------- | :---------------- |
| **Edge Network** | Hits are sent | Hits are not sent | Hits are queued   |

> **Note:** When no default collect consent value is defined in configuration, the SDK defaults to Yes (y) for collect consent.

{% hint style="warning" %}
Updating the collect consent status to No (n) does not reset or clear the identities of the current user. If you need to reset all current identities, use the [MobileCore.resetIdentities()](../foundation-extensions/mobile-core/mobile-core-api-reference.md#resetidentities) API.
{% endhint %}

### Collect consent settings

{% tabs %}
{% tab title="Android" %}

#### Java

You can set the collect consent to one of the following values:

* `y`
* `n`

To understand the expected behavior, see the _Update and get collect consent preferences_ table above.
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}
You can set the collect consent to one of the following values:

#### Swift

* `y`
* `n`

#### Objective-C

You can set the collect consent to one of the following values:

* `y`
* `n`

To understand the expected behavior, see the _Update and get collect consent preferences_ table above.
{% endtab %}
{% endtabs %}

### getConsents

You can programmatically view the current collect consent preferences status in a dictionary representation by using the following API.

{% tabs %}
{% tab title="Android" %}

#### Java

**Syntax**

```java
public static void getConsents(final AdobeCallback<Map<String, Object>> callback);
```

* _callback_ - callback invoked with the current consents of the extension. If an `AdobeCallbackWithError` is provided, an `AdobeError`, can be retruned in the eventuality of any error that occured while getting the user consents. The callback may be invoked on a different thread.

**Example**

```java
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

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
static func getConsents(completion: @escaping ([String: Any]?, Error?) -> Void)
```

**Example**

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

**Syntax**

```objective-c
static func getConsents(completion: @escaping ([String: Any]?, Error?) -> Void)
```

**Example**

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

### updateConsents

Use this example to programmatically update the consent collect for the application user.

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void update(final Map<String, Object> consents);
```

**Example**

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

{% tab title="iOS (AEP 3.x)" %}
#### Swift

**Syntax**

```swift
static func update(with consents: [String: Any])
```

**Example**

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

**Syntax**

```swift
static func update(with consents: [String: Any])
```

**Example**

```text
// example 1, updating users collect consent to 'yes'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"y"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConsent}];

// example 2, updating users collect consent to 'no'
NSDictionary *collectConsent = @{ @"collect": @{@"val": @"n"};
[AEPMobileEdgeConsent updateWithConsents:@{@"consents": collectConsent}];
```
{% endtab %}
{% endtabs %}

### getIdentities

When using the Edge Network extensions, use the [Identity.getIdentities](../foundation-extensions/identity-for-edge-network/api-reference.md#getidentities) API to retrieve all the identifier data stored locally by the SDK and send this data to your servers.

## Configuration keys

To programmatically update the SDK configuration, use the following information to change your default consent values. For more information, see the [configuration API reference](../foundation-extensions/mobile-core/configuration/configuration-api-reference.md).

| Key               | Description                                                  |
| :---------------- | :----------------------------------------------------------- |
| `consent.default` | Defines the set of default consent preferences for the SDK in XDM format. For more details, see [Privacy/Personalization/Marketing Preferences (Consents) Schema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-consents.schema.md). |



## Using Adobe Experience Cloud Solution extensions

## Set and get privacy status

You can set a privacy status to ensure collection of data suits your user's preferences.

| **Expected Behavior** | Opt In | Opt Out | Opt Unknown |
| :--- | :--- | :--- | :--- |
| **Analytics** | Hits are sent | Hits are not sent | Hits are queued |
| **Audience** **Manager** | Signals, ID syncs are sent | Signals, ID syncs are not sent | Syncs are queued |
| **Campaign Classic** | User data is stored, calls are sent | User data is cleared, calls are not sent | User data is stored, calls are not sent |
| **Target** | Mbox requests are sent | Mbox requests are not sent | Mbox requests are queued |
| **Campaign Standard** | User data is stored, calls are sent | User data is cleared, calls are not sent | User data is stored, calls are queued |

{% hint style="info" %}
**Analytics users**: If your report suite is not timestamp enabled, hits are discarded until the privacy status changes to `opt in`.
{% endhint %}

### setPrivacyStatus

{% tabs %}
{% tab title="Android" %}

You can set the privacy status to one of the following values:

* `MobilePrivacyStatus.OPT_IN`
* `MobilePrivacyStatus.OPT_OUT`
* `MobilePrivacyStatus.UNKNOWN`

To understand the expected behavior, see the "Set and get privacy status" table above.

#### Java

**Syntax**

```java
public static void setPrivacyStatus(final MobilePrivacyStatus privacyStatus);
```

**Example**

```java
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT);
```
{% endtab %}

{% tab title="iOS (ACP 3.x)" %}

You can set privacy status to one of the following values:

* `PrivacyStatus.optedIn`
* `PrivacyStatus.optedOut`
* `PrivacyStatus.unknown`

To understand the expected behavior, see the _Set and get privacy status_ table above.

#### Swift

**Syntax**

```swift
static func setPrivacyStatus(_ status: PrivacyStatus)
```

**Example**

```swift
MobileCore.setPrivacyStatus(.optedIn)
```

#### Objective-C

**Syntax**

```objective-c
@objc(setPrivacyStatus:)
static func setPrivacyStatus(_ status: PrivacyStatus)
```

**Example**

```objective-c
[AEPMobileCore setPrivacyStatus:AEPPrivacyStatusOptedIn];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

You can set privacy status to one of the following values:

* `ACPMobilePrivacyStatusOptIn`
* `ACPMobilePrivacyStatusOptOut` 
* `ACPMobilePrivacyStatusUnknown`

To understand the expected behavior, see the _Set and get privacy status_ table above.

#### Swift

**Syntax**

```swift
class func setPrivacyStatus(_ status: ACPMobilePrivacyStatus) {
}
```

**Example**

```swift
ACPCore.privacyStatus = ACPMobilePrivacyStatusOptIn
```
#### Objective-C

**Syntax**

```objectivec
+ (void) setPrivacyStatus: (ACPMobilePrivacyStatus) status;
```

**Example**

```objectivec
[ACPCore setPrivacyStatus:ACPMobilePrivacyStatusOptIn];
```

{% endtab %}
{% endtabs %}

### getPrivacyStatus

You can also programmatically view the current privacy status by using the following:

{% tabs %}
{% tab title="Android" %}

The enum representation of the privacy status that corresponds to the following statuses:

* `MobilePrivacyStatus.OPT_IN`
* `MobilePrivacyStatus.OPT_OUT`
* `MobilePrivacyStatus.UNKNOWN`

#### Java

**Syntax**

```java
void getPrivacyStatus(AdobeCallback<MobilePrivacyStatus> callback);
```

* _callback_ is invoked after the privacy status is available.
* If an instance of  `AdobeCallbackWithError` is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 5000ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate `AdobeError`.

**Example**

```java
MobileCore.getPrivacyStatus(new AdobeCallback<MobilePrivacyStatus>() {
    @Override
    public void call(MobilePrivacyStatus value) {
          System.out.println("getPrivacyStatus: " + status);
    }
});
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

The enum representation of the privacy status that corresponds to the following statuses:

* `PrivacyStatus.optedIn`
* `PrivacyStatus.optedOut`
* `PrivacyStatus.unknown`

#### Swift

**Syntax**

```swift
static func getPrivacyStatus(completion: @escaping (PrivacyStatus) -> Void)
```

* _completion_ is invoked with the current `PrivacyStatus`.

**Example**

```swift
MobileCore.getPrivacyStatus { privacyStatus in
	switch privacyStatus {
	case .optedIn:
		print("Privacy Status: Opted in")
	case .optedOut:
		print("Privacy Status: Opted out")
	case .unknown:
		print("Privacy Status: Unknown")
}
```

#### Objective-C

**Syntax**

```objective-c
@objc(getPrivacyStatus:)
static func getPrivacyStatus(completion: @escaping (PrivacyStatus) -> Void)
```

* _completion_ is invoked with the current `PrivacyStatus`.

**Example**

```objectivec
[AEPMobileCore getPrivacyStatus:^(AEPPrivacyStatus status) {
	switch (status) {
		case AEPPrivacyStatusOptedIn:
			NSLog(@"Privacy status: Opted in");
			break;
		case AEPPrivacyStatusOptedOut:
			NSLog(@"Privacy status: Opted out");
			break;
		case AEPPrivacyStatusUnknown:
			NSLog(@"Privacy status: Unknown");
			break;
  }
}];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

The enum representation of the privacy status that corresponds to the following statuses:

* `ACPMobilePrivacyStatusOptIn` 
* `ACPMobilePrivacyStatusOptOut`
* `ACPMobilePrivacyStatusUnknown`

#### Swift

**Syntax**

```swift
class func getPrivacyStatus(_ callback: @escaping (_ status: ACPMobilePrivacyStatus) -> Void)

class func getPrivacyStatus(withCompletionHandler completionHandler: @escaping (_ status: ACPMobilePrivacyStatus, _ error: Error?) -> Void)
```

* _callback_ is invoked after the privacy status is available.
* _completionHandler_ is invoked with the current privacy status, or _error_ if an unexpected error occurs or the request times out. The default timeout is 5000ms.

**Example**

```swift
ACPCore.getPrivacyStatus(
    { status in
        switch status {
            case ACPMobilePrivacyStatusOptIn:
                print("Privacy Status: Opt-In")
            default:
                break
        }
    })


ACPCore.getPrivacyStatus(withCompletionHandler: { status, error in
    if error != nil {
        // handle error here
    } else {
        // handle the retrieved privacy status
    }
})
```
#### Objective-C

**Syntax**

```java
+ (void) getPrivacyStatus: (nonnull void (^) (ACPMobilePrivacyStatus status)) callback;
+ (void) getPrivacyStatusWithCompletionHandler: (nonnull void (^) (ACPMobilePrivacyStatus status, NSError* _Nullable error)) completionHandler;
```

* _callback_ is invoked after the privacy status is available.
* _completionHandler_ is invoked with the current privacy status, or _error_ if an unexpected error occurs or the request times out. The default timeout is 5000ms.

**Example**

```objectivec
[ACPCore 
getPrivacyStatus:^(ACPMobilePrivacyStatus status) { 
     switch (status) { 
          case ACPMobilePrivacyStatusOptIn: NSLog(@"Privacy Status: Opt-In");               break; 
          } 
}];


[ACPCore getPrivacyStatusWithCompletionHandler:^(ACPMobilePrivacyStatus status, NSError * _Nullable error) {
        if (error) {
            // handle error here
        } else {
            // handle the retrieved privacy status
        }
    }];
```

{% endtab %}
{% endtabs %}

### getSdkIdentities

To retrieve all the identifier data stored locally by the SDK as a JSON string, use the [getSdkIdentities](../foundation-extensions/mobile-core/mobile-core-api-reference.md#getsdkidentities) API from the Mobile Core extension.

{% hint style="info" %}
When using both Edge Network and Adobe Solutions extensions, use both [Identity.getIdentities](../foundation-extensions/identity-for-edge-network/api-reference.md#getidentities) API and [MobileCore.getSdkIdentities](../foundation-extensions/mobile-core/mobile-core-api-reference.md#getsdkidentities) APIs to retrieve all the identifier data stored locally by the SDK.
{% endhint %}

## Configuration keys

To update the SDK configuration, programmatically, use the following information to change your privacy configuration values. For more information, [Configuration API reference](../foundation-extensions/mobile-core/configuration/configuration-api-reference.md).

| Key | Description |
| :--- | :--- |
| `global.privacy` | Setting to control privacy opt status; values may include `optedin`, `optedout`, `optunknown` |

## Video

{% embed url="https://www.youtube.com/watch?v=kgUJNFQp3PI" caption="Using Mobile SDK Privacy APIs" %}

## Additional information

* For more information about GDPR, see [GDPR and Your Business](https://www.adobe.com/privacy/general-data-protection-regulation.html)
* To see the Privacy Service API documentation, go to [Privacy Service API](https://experienceleague.adobe.com/docs/experience-platform/privacy/home.html)

