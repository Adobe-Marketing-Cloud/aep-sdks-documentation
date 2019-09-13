# Troubleshooting Push Messaging

When implementing push messaging via the SDK, you can validate client-side implementation by verifying you've done the following steps:

1. [Pass the device's push token to the SDK](#pass-the-push-identifier-to-the-sdk)
2. [Verify the push token has been sent to Adobe's Visitor Identity servers](#validate-setpushidentifier-event)
3. [Ensure the user has been opted in for push messaging in Adobe Analytics](#validate-analytics-request-with-push-optin)
4. [Confirm that the ID for the user is the same in steps 2 and 3 above](validate-the-user-id-is-correct)

## Pass the Push Identifier to the SDK

The `setPushIdentifier` API sets the device token for push notifications in the SDK. This will result in multiple calls to the necessary Adobe servers to associate the user with the push token.

{% hint style="info" %}
If the current SDK privacy status is `optedout`, the push identifier will not be set.
{% endhint %}

### setPushIdentifier

{% tabs %}

{% tab title="Android" %}

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

{% tab title="objective-c" %}

#### Syntax

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

#### Example

```objectivec
// pass the deviceToken that the APNS has assigned to the device
[ACPCore setPushIdentifier:deviceToken];
```

{% endtab %}

{% tab title="Swift" %}

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

#### Example

```jsx
ACPCore.setPushIdentifier("pushIdentifier");
```

{% endtab %}

{% endtabs %}

### Validate SetPushIdentifier event

Launch your app with the device connected to an [Adobe Griffon session](../../beta/project-griffon). Verify in the list of events that you have an event with type `SetPushIdentifier`. In the details panel on the right, you can verify the value of the push token for this device. The value in `pushIdentifier` is the same value sent to the Adobe servers.

<img src="../../.gitbook/assets/push_token_to_identity.png" />

### Validate Analytics request with Push OptIn

Launch your app with the device connected to an [Adobe Griffon session](../../beta/project-griffon). Verify in the list of events that you have an event with type `AnalyticsForIdentityRequest`. In the details panel on the right, you can see that there is a value sent to Analytics which opts this user in to receive push notifications.

<img src="../../.gitbook/assets/push_analytics_optin.png" />

### Validate the User ID is correct

Launch your app with the device connected to an [Adobe Griffon session](../../beta/project-griffon). Verify in the list of events that you have an event with type `UPDATED_IDENTITY_RESPONSE`. In the details panel on the right, you will want to confirm that two values are correct:

1. The value for `pushidentifier` should match the value sent in step 2 above
2. The value for `mid` should match the value for `mid` that is sent to Analytics. If you are using a [custom visitor identifier](../../using-mobile-extensions/adobe-analytics/analytics-api-reference#setidentifier), this payload should also contain a `vid` variable with a matching value of that used to identify this user.

<img src="../../.gitbook/assets/push_identities.png" />

<hr />

After completing the above steps, you can be confident that your app is correctly configured to send push messages via the SDK and Adobe.
