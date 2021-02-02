# Privacy and GDPR

The Adobe Experience Platform SDKs give you controls to manage consent and privacy obligations under the European Union's General Data Protection Regulation \(GDPR\). Developers can retrieve locally stored identities and set opt status flags for data collection and transmission.

Before implementing these controls, read Adobe's [GDPR documentation](https://www.adobe.io/apis/cloudplatform/gdpr.html).

When Adobe provides software and services to an enterprise, Adobe acts as a data processor for any personal data it processes and stores as part of providing these services. As a data processor, Adobe processes personal data in accordance with your company’s permission and instructions, as set out in your agreement with Adobe. As a data controller, you can use the Experience Platform SDKs to support GDPR retrieve and delete requests from your mobile apps.

## Set and get privacy status

You can set a privacy status to ensure collection of data suits your user's preferences.

| Extension | Opt In | Opt Out | Opt Unknown |
| :--- | :--- | :--- | :--- |
| **Edge Network** | Hits are sent | Hits not sent | Hits queued |

### Privacy Status settings

{% tabs %}
{% tab title="Android" %}
#### Java

You can set the privacy status to one of the following values:

* `MobilePrivacyStatus.OPT_IN`
* `MobilePrivacyStatus.OPT_OUT`
* `MobilePrivacyStatus.UNKNOWN`

To understand the expected behavior, see the _Set and get privacy status_ table above.
{% endtab %}

{% tab title="iOS" %}
You can set privacy status to one of the following values:

#### Swift

* `PrivacyStatus.optedIn`
* `PrivacyStatus.optedOut` 
* `PrivacyStatus.unknown`

#### Objective-C

You can set privacy status to one of the following values:

* `AEPPrivacyStatusOptedIn`
* `AEPPrivacyStatusOptedOut` 
* `AEPPrivacyStatusUnknown`

To understand the expected behavior, see the _Set and get privacy status_ table above.
{% endtab %}
{% endtabs %}

### setPrivacyStatus <a id="setprivacystatus"></a>

To programmatically set the privacy status for the application user:

{% tabs %}
{% tab title="Android" %}
#### Java

#### Syntax

```java
public static void setPrivacyStatus(final MobilePrivacyStatus privacyStatus);
```

#### Example

```java
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT);
```
{% endtab %}

{% tab title="iOS" %}
#### Swift

#### Syntax

```swift
static func setPrivacyStatus(_ status: PrivacyStatus)
```

#### Example

```swift
MobileCore.setPrivacyStatus(PrivacyStatus.optedIn)
```

#### Objective-C

#### Syntax

```text
+ (void) setPrivacyStatus: (AEPPrivacyStatus) status;
```

#### Example

```text
[AEPMobileCore setPrivacyStatus:AEPPrivacyStatusOptedIn];
```
{% endtab %}
{% endtabs %}

You can also programmatically view the current privacy status by using the following:

{% hint style="info" %}
The following API returns an enum representation of the privacy status for the user.
{% endhint %}

### getPrivacyStatus <a id="getprivacystatus"></a>

{% tabs %}
{% tab title="Android" %}
#### Java

#### Syntax

```objectivec
void getPrivacyStatus(AdobeCallback<MobilePrivacyStatus> callback);
```

* _callback_ is invoked after the privacy status is available.
* If an instance of  `AdobeCallbackWithError` is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 5000ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate `AdobeError`.

#### Example

```objectivec
MobileCore.getPrivacyStatus(new AdobeCallback<MobilePrivacyStatus>() {
    @Override
    public void call(MobilePrivacyStatus value) {
          System.out.println("getPrivacyStatus: " + status);
    }
});
```
{% endtab %}

{% tab title="iOS" %}
#### Swift

#### Syntax

```swift
static func getPrivacyStatus(completion: @escaping (PrivacyStatus) -> Void)
```

#### Example

```swift
MobileCore.getPrivacyStatus { (status: PrivacyStatus) in
    switch status {
        case .optedIn:
            print("Privacy Status: Opt-In")
        case .optedOut:
            print("Privacy Status: Opt-Out")
        case .unknown:
            print("Privacy Status: Unknown")
        default:
            print("Privacy Status: Unknown")
        }
}
```

#### Objective-C

#### Syntax

```text
+ (void) getPrivacyStatus: (nonnull void (^) (AEPPrivacyStatus status)) callback;
```

#### Example

```text
[AEPMobileCore getPrivacyStatus:^(AEPPrivacyStatus status) {
  switch (status) {
    case AEPPrivacyStatusOptedIn:
      NSLog(@"Privacy Status: Opt-in");
      break;

    default:
      break;
  }
}];
```
{% endtab %}
{% endtabs %}

## Retrieving stored identifiers

To retrieve all the identifier data stored locally by the SDK as a JSON string, and send this data to your servers, use the [getSdkIdentities](../using-mobile-extensions/mobile-core/mobile-core-api-reference.md#getsdkidentities) API from the Mobile Core extension.

## Configuration keys

To update the SDK configuration, programmatically, use the following information to change your privacy configuration values. For more information, [Configuration API reference](../using-mobile-extensions/mobile-core/configuration/configuration-api-reference.md).

| Key | Description |
| :--- | :--- |
| `global.privacy` | Setting to control privacy opt status; values may include `optedid`, `optedout`, `optunknown` |

## Video

{% embed url="https://www.youtube.com/watch?v=kgUJNFQp3PI" caption="Using Mobile SDK Privacy APIs" %}

## Additional information

* For more information about GDPR, see [GDPR and Your Business](https://www.adobe.com/privacy/general-data-protection-regulation.html)
* To see the GDPR API documentation, go to [General Data Protection Regulation API](https://adobe.io/apis/cloudplatform/gdpr.html)

