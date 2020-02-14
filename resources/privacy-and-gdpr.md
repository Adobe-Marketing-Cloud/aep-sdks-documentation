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

{% hint style="info" %}
**Analytics users**: If your report suite is not timestamp enabled, hits are discarded until the privacy status changes to `opt in`.
{% endhint %}

To programmatically set the privacy status for the app user:

{% tabs %}
{% tab title="Android" %}
#### Java

### setPrivacyStatus  <a id="setprivacystatus"></a>

You can set the privacy status to one of the following values:

* `MobilePrivacyStatus.OPT_IN`
* `MobilePrivacyStatus.OPT_OUT`
* `MobilePrivacyStatus.UNKNOWN`

To understand the expected behavior, see the _Set and get privacy status_ table above.

#### Syntax  <a id="syntax-4"></a>

```java
public static void setPrivacyStatus(final MobilePrivacyStatus privacyStatus);
```

#### Example  <a id="example-4"></a>

```java
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT);
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

### setPrivacyStatus

You can set privacy status to one of the following values:

* `ACPMobilePrivacyStatusOptIn`
* `ACPMobilePrivacyStatusOptOut` 
* `ACPMobilePrivacyStatusUnknown`

To understand the expected behavior, see the _Set and get privacy status_ table above.

### Syntax  <a id="syntax-4"></a>

```objectivec
+ (void) setPrivacyStatus: (ACPMobilePrivacyStatus) status;
```

### Example  <a id="example-4"></a>

```objectivec
[ACPCore setPrivacyStatus:ACPMobilePrivacyStatusOptIn
```
{% endtab %}
{% endtabs %}

You can also programmatically view the current privacy status by using the following:

{% hint style="info" %}
The following API returns an enum representation of the privacy status for the user.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

### getPrivacyStatus

The enum representation of the privacy status that corresponds to the following statuses:

* `MobilePrivacyStatus.OPT_IN`
* `MobilePrivacyStatus.OPT_OUT`
* `MobilePrivacyStatus.UNKNOWN`

#### Syntax

```objectivec
void getPrivacyStatus(final AdobeCallback callback);
```

#### Example  <a id="example-5"></a>

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
#### Objective-C

### getPrivacyStatus

The enum representation of the privacy status that corresponds to the following statuses:

* `ACPMobilePrivacyStatusOptIn` 
* `ACPMobilePrivacyStatusOptOut`
* `ACPMobilePrivacyStatusUnknown`

#### Syntax

```java
+ (void) getPrivacyStatus: (nonnull void (^) (ACPMobilePrivacyStatus status)) callback;
```

#### Example

```objectivec
[ACPCore 
getPrivacyStatus:^(ACPMobilePrivacyStatus status) { 
     switch (status) { 
          case ACPMobilePrivacyStatusOptIn: NSLog(@"Privacy Status: Opt-In");               break; 
          } 
}];
```
{% endtab %}
{% endtabs %}

## Retrieving stored identifiers

The following SDK identities \(as applicable\) are locally stored:

* Company Context - IMS Org IDs
* Experience Cloud ID \(MID\)
* User IDs
* Integration codes \(ADID, push IDs\)
* Data source IDs \(DPID, DPUUID\)
* Analytics IDs \(AVID, AID, VID, and associated RSIDs\)
* Target legacy IDs \(TNTID, TNT3rdpartyID\)
* Audience Manager ID \(UUID\)

To retrieve data as a JSON string from the SDKs, and send this data to your servers, use the following:

{% hint style="warning" %}
You must call the API below and retrieve identities stored in the SDK, **before** the user opts out.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

#### Syntax

```java
MobileCore.getSdkIdentities()
```

#### Example

```java
MobileCore.getSdkIdentities(new AdobeCallback<String>() {
    @Override
    public void call(String value) {
        // handle the json string
    }
});
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

#### Syntax

```objectivec
[ACPCore getSdkIdentities:]
```

#### Example

```objectivec
[ACPCore getSdkIdentities:^(NSString * _Nullable content){
    NSLog(content);
}];
```
{% endtab %}
{% endtabs %}

## Configuration keys

To update the SDK configuration, programmatically, use the following information to change your privacy configuration values. For more information, [Configuration API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

| Key | Description |
| :--- | :--- |
| `global.privacy` | Setting to control privacy opt status; values may include `optedid`, `optedout`, `optunknown` |

## Video

{% embed url="https://www.youtube.com/watch?v=kgUJNFQp3PI" caption="Using Mobile SDK Privacy APIs" %}

## Additional information

* For more information about GDPR, see [GDPR and Your Business](https://www.adobe.com/privacy/general-data-protection-regulation.html)
* To see the GDPR API documentation, go to [General Data Protection Regulation API](https://adobe.io/apis/cloudplatform/gdpr.html)

