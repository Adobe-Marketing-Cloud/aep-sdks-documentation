# Push Messaging

{% hint style="warning" %}
This troubleshooting guide requires [Project Griffon](../../beta/project-griffon/). For more information about access and how to set up Project Griffon, see the [documentation](../../beta/project-griffon/).
{% endhint %}

When implementing push messaging via the Adobe Experience Platform Mobile SDK, you can validate the client-side implementation by verifying that you completed the following steps:

1. [Pass the device's push token to the SDK](troubleshooting-push.md#pass-the-push-identifier-to-the-sdk).
2. [Verify push token sync with the Experience Cloud Identity service](troubleshooting-push.md#validate-push-token-sync-with-the-experience-cloud-identity-service).
3. [Ensure user opt in for push in Adobe Analytics](troubleshooting-push.md#ensure-user-opt-in-for-push-in-adobe-analytics).
4. [Confirm user ID is correctly set \(and is same from steps 2 and 3, above](troubleshooting-push.md#confirm-that-the-user-id-is-correctly-set).

## Pass the Push Identifier to the SDK

The `setPushIdentifier` API sets the device token for push notifications in the SDK. This results in a few network calls made to the requisite Adobe servers to associate the user with the push token.

{% hint style="warning" %}
If SDK privacy status is`optedout`, the push identifier will not be set.
{% endhint %}

### setPushIdentifier

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void setPushIdentifier(final String pushIdentifier);
```

#### Example

```java
// retrieve the token from either GCM or FCM, and pass it to the SDK
MobileCore.setPushIdentifier(token);
```
{% endtab %}

{% tab title="iOS" %}
### Objective C

#### Syntax

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

#### Example

```objectivec
// pass the deviceToken that the APNS has assigned to the device
[ACPCore setPushIdentifier:deviceToken];
```

### Swift

#### Syntax

```swift
Void setPushIdentifier(deviceToken: Data?)
```

#### Example

```swift
// pass the deviceToken that the APNS has assigned to the device
ACPCore.setPushIdentifier(deviceToken)
```
{% endtab %}

{% tab title="React Native" %}
### Javascript

#### Example

```jsx
ACPCore.setPushIdentifier("pushIdentifier");
```
{% endtab %}
{% endtabs %}

## Verify push token sync with the Experience Cloud Identity service

Launch your app with the device connected to a [Project Griffon session](../../beta/project-griffon/).

In the list of events, verify that you have an event with type `SetPushIdentifier`. In the details panel on the right, verify the value of the push token for this device. The value in `pushIdentifier` is the same value that is sent to the Adobe servers.

![](../../.gitbook/assets/push_token_to_identity.png)

## Ensure user opt-in for push in Adobe Analytics

Launch your app with the device connected to a [Project Griffon session](../../beta/project-griffon/).

In the resulting list of events, verify that you have an event with type `AnalyticsForIdentityRequest`. In the details panel on the right, you can see that there is a value that was sent to Analytics that opts this user in to receive push notifications.

![](../../.gitbook/assets/push_analytics_optin.png)

## Confirm that the user ID is correctly set

Launch your app with the device connected to a [Project Griffon session](../../beta/project-griffon/).

In the list of events, verify that you have an event with type `UPDATED_IDENTITY_RESPONSE`. In the details panel on the right, confirm that the following values are correct:

* The value for `pushidentifier` should match the value that was sent in step 2 above.
* The value for `mid` should match the value for `mid` that is sent to Analytics.  If you are using a [custom visitor identifier](../../using-mobile-extensions/adobe-analytics/analytics-api-reference.md#setidentifier), this payload should also contain a `vid` variable with a value that matches the value that was used to identify this user.

![](../../.gitbook/assets/push_identities.png)

After completing these steps, your app is correctly configured and is ready to send push messages via the SDK and Adobe.

