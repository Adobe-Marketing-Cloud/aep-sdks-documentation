# Privacy and GDPR

The Experience Platform SDKs give you controls to manage consent and privacy obligations under the European Union's General Data Protection Regulation \(GDPR\). Developers can retrieve locally stored identities and set opt status flags for data collection and transmission.

Before implementing these controls, read Adobe's [GDPR documentation](https://www.adobe.io/apis/cloudplatform/gdpr.html).

When Adobe provides software and services to an enterprise, Adobe acts as a data processor for any personal data it processes and stores as part of providing these services. As a data processor, Adobe processes personal data in accordance with your company’s permission and instructions, as set out in your agreement with Adobe. As a data controller, you can use the Experience Platform SDKs to support GDPR retrieve and delete requests from your mobile apps.

## Set and get privacy status

You can set a privacy status to ensure collection of data suits your user's preferences.

| Exp**ected Behavior** | Opt In | Opt Out | Opt Unknown |
| :--- | :--- | :--- | :--- |
| **Analytics** | Hits are sent | Hits not sent | Hits queued |
| **Audience** **Manager** | Signals, ID syncs are sent | Signals, ID syncs not sent | Syncs queued |
| **Campaign Classic** | User data stored, calls are sent | User data cleared, calls not sent | User data stored, calls not sent |
| **Target** | Mbox requests are sent | Mbox requests not sent | Mbox requests queued |
| **Campaign Standard** | User data stored, calls are sent | User data cleared, calls not sent | User data stored, calls are queued |

{% hint style="info" %}
**Analytics users**: If your report suite is not timestamp enabled, hits are discarded until the privacy status changes to `opt in`.
{% endhint %}

To programmatically set the privacy status for the app user:

{% tabs %}
{% tab title="Android" %}
#### Java

### setPrivacyStatus <a id="setprivacystatus"></a>

You can set the privacy status to one of the following values:

* `MobilePrivacyStatus.OPT_IN`
* `MobilePrivacyStatus.OPT_OUT`
* `MobilePrivacyStatus.UNKNOWN`

To understand the expected behavior, see the _Set and get privacy status_ table above.

#### Syntax <a id="syntax-4"></a>

```java
public static void setPrivacyStatus(final MobilePrivacyStatus privacyStatus);
```

#### Example <a id="example-4"></a>

```java
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT);
```
{% endtab %}

{% tab title="iOS" %}
### setPrivacyStatus

You can set privacy status to one of the following values:

* `ACPMobilePrivacyStatusOptIn`
* `ACPMobilePrivacyStatusOptOut` 
* `ACPMobilePrivacyStatusUnknown`

To understand the expected behavior, see the _Set and get privacy status_ table above.

### Objective-C

#### Syntax

```objectivec
+ (void) setPrivacyStatus: (ACPMobilePrivacyStatus) status;
```

#### Example

```objectivec
[ACPCore setPrivacyStatus:ACPMobilePrivacyStatusOptIn];
```

### Swift

#### Syntax

```objectivec
class func setPrivacyStatus(_ status: ACPMobilePrivacyStatus) {
}
```

#### Example

```objectivec
ACPCore.privacyStatus = ACPMobilePrivacyStatusOptIn
```
{% endtab %}
{% endtabs %}

You can also programmatically view the current privacy status by using the following:

{% hint style="info" %}
The following API returns an enum representation of the privacy status for the user.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### getPrivacyStatus

The enum representation of the privacy status that corresponds to the following statuses:

* `MobilePrivacyStatus.OPT_IN`
* `MobilePrivacyStatus.OPT_OUT`
* `MobilePrivacyStatus.UNKNOWN`

### Java

#### Syntax

```objectivec
void getPrivacyStatus(AdobeCallback<MobilePrivacyStatus> callback);
```

* _callback_ is invoked after the privacy status is available.
* If an instance of  `AdobeCallbackWithError` is provided, and you are fetching the attributes from the Mobile SDK, the timeout value is 5000ms. If the operation times out or an unexpected error occurs, the `fail` method is called with the appropriate `AdobeError`.

#### Example <a id="example-5"></a>

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
### getPrivacyStatus

The enum representation of the privacy status that corresponds to the following statuses:

* `ACPMobilePrivacyStatusOptIn` 
* `ACPMobilePrivacyStatusOptOut`
* `ACPMobilePrivacyStatusUnknown`

### Objective-C

#### Syntax

```java
+ (void) getPrivacyStatus: (nonnull void (^) (ACPMobilePrivacyStatus status)) callback;
+ (void) getPrivacyStatusWithCompletionHandler: (nonnull void (^) (ACPMobilePrivacyStatus status, NSError* _Nullable error)) completionHandler;
```

* _callback_ is invoked after the privacy status is available.
* _completionHandler_ is invoked with the current privacy status, or _error_ if an unexpected error occurs or the request times out. The default timeout is 5000ms.

#### Example

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

### Swift

#### Syntax

```java
class func getPrivacyStatus(_ callback: @escaping (_ status: ACPMobilePrivacyStatus) -> Void) {//}

class func getPrivacyStatus(withCompletionHandler completionHandler: @escaping (_ status: ACPMobilePrivacyStatus, _ error: Error?) -> Void) {//}
```

* _callback_ is invoked after the privacy status is available.
* _completionHandler_ is invoked with the current privacy status, or _error_ if an unexpected error occurs or the request times out. The default timeout is 5000ms.

#### Example

```objectivec
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
{% endtab %}
{% endtabs %}

## Retrieving stored identifiers

To retrieve all the identifier data stored locally by the SDK as a JSON string, and send this data to your servers, use the [getSdkIdentities](../foundation-extensions/mobile-core/mobile-core-api-reference.md#getsdkidentities) API from the Mobile Core extension.

## Configuration keys

To update the SDK configuration, programmatically, use the following information to change your privacy configuration values. For more information, [Configuration API reference](../foundation-extensions/mobile-core/configuration/configuration-api-reference.md).

| Key | Description |
| :--- | :--- |
| `global.privacy` | Setting to control privacy opt status; values may include `optedid`, `optedout`, `optunknown` |

## Video

{% embed url="https://www.youtube.com/watch?v=kgUJNFQp3PI" caption="Using Mobile SDK Privacy APIs" %}

## Additional information

* For more information about GDPR, see [GDPR and Your Business](https://www.adobe.com/privacy/general-data-protection-regulation.html)
* To see the GDPR API documentation, go to [General Data Protection Regulation API](https://adobe.io/apis/cloudplatform/gdpr.html)

