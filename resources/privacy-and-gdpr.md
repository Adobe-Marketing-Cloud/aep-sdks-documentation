# Privacy and GDPR

The Adobe Experience Platform SDK gives you controls to manage consent and privacy obligations under the European Union's General Data Protection Regulation \(GDPR\). Developers may retrieve locally stored identities and set opt status flags for data collection and transmission.

Before instrumenting these controls, be sure to read Adobe's [GDPR documentation](https://www.adobe.io/apis/cloudplatform/gdpr.html).

When Adobe provides software and services to an enterprise, Adobe acts as a data processor for any personal data it processes and stores as part of providing these services. As a data processor, Adobe processes personal data in accordance with your company’s permission and instructions \(for example, as set out in your agreement with Adobe\). As a data controller, you can use the Adobe Cloud Platform SDKs to support GDPR retrieve and delete requests from your mobile apps.

## Set & get privacy status

You may set a privacy status to ensure collection of data suits your users' preferences.

| Exp**ected Behavior** | Opt In | Opt Out | Opt Unknown |
| :--- | :--- | :--- | :--- |
| **Analytics** | Hits are sent | Hits not sent | Hits queued |
| **Audience** **Manager** | Signals, ID syncs are sent | Signals, ID syncs not sent | Syncs queued |
| **Target** | Mbox requests are sent | Mbox requests not sent | Mbox requests queued |

{% hint style="info" %}
Analytics users: If your report suite is not timestamp enabled, hits will be discarded until the privacy status changes to opt in.
{% endhint %}

To programmatically set the privacy status for the app user:

{% tabs %}
{% tab title="Android" %}
#### Java

### setPrivacyStatus {#setprivacystatus}

You may set privacy status to one of the following values, see table above for expected behavior:

* `MobilePrivacyStatus.OPT_IN`
* `MobilePrivacyStatus.OPT_OUT`
* `MobilePrivacyStatus.UNKNOWN`

#### Syntax {#syntax-4}

```java
public static void setPrivacyStatus(final MobilePrivacyStatus privacyStatus);
```

#### Example {#example-4}

```java
MobileCore.setPrivacyStatus(MobilePrivacyStatus.OPT_OUT);
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

### setPrivacyStatus

You may set privacy status to one of the following values, see table above for expected behavior:

* `ACPMobilePrivacyStatusOptIn`
* `ACPMobilePrivacyStatusOptOut` 
* `ACPMobilePrivacyStatusUnknown`

### Syntax {#syntax-4}

```objectivec
+ (void) setPrivacyStatus: (ACPMobilePrivacyStatus) status;
```

### Example {#example-4}

```objectivec
[ACPCore setPrivacyStatus:ACPMobilePrivacyStatusOptIn
```
{% endtab %}
{% endtabs %}

You may also, programmatically, view current privacy status by using the following:

{% hint style="info" %}
This API returns an enum representation of the privacy status for the user.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Java

### getPrivacyStatus

Enum representation of privacy status correspond to the following status:

* `MobilePrivacyStatus.OPT_IN`
* `MobilePrivacyStatus.OPT_OUT`
* `MobilePrivacyStatus.UNKNOWN`

#### Syntax

```objectivec
void getPrivacyStatus(final AdobeCallback callback);
```

#### Example {#example-5}

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

Enum representation of privacy status correspond to the following status:

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

| Identifiers |
| :--- |
| Company Context - IMS Org IDs |
| Experience Cloud ID \(ECID\) |
| User IDs |
| Integration codes \(ADID, push IDs\) |
| Data source IDs \(DPID, DPUUID\) |
| Analytics IDs \(AVID, AID, VID, and associated RSIDs\) |
| Target legacy IDs \(TNTID, TNT3rdpartyID\) |
| Audience Manager ID \(UUID\) |

To retrieve data, as a JSON string, from the SDKs, and send this data to your servers, use the following:

{% hint style="warning" %}
You must call the API below and retrieve identities stored in the SDK, **before** the user opts-out.
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

## Configuration Keys

If you need to update SDK configuration, programmatically, please use the following information to change your privacy configuration values. For more information, [Configuration Methods Reference](../mobile-extensions/mobile-core/configuration-reference.md#update-configuration).

| Key | Description |
| :--- | :--- |
| global.privacy | Setting to control privacy opt status; values may include `optedid`, `optedout`, `optunknown` |

## Further Reading

* For more information about GDPR, see [GDPR and Your Business](https://www.adobe.com/privacy/general-data-protection-regulation.html)
* To see the GDPR API documentation, go to [General Data Protection Regulation API](https://adobe.io/apis/cloudplatform/gdpr.html)



