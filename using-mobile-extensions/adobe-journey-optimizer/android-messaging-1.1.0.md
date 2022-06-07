# Android Messaging 1.1.0: Push Notification Improvements

Android AEPMessaging 1.1.0 introduces AEPMessaging handled push notification creation and tracking. This new functionality provides a convenient way to display and track interactions with Adobe Journey Optimizer (AJO) created push notifications. The steps below will serve as a guide to enabling the new features provided in AEPMessaging 1.1.0.

{% hint style="info" %}

The usage of these features are optional and no code changes are required if not using them.

{% endhint %}

When using AEPMessaging handled push notification interaction tracking, the AEPMessaging extension must also be used to create the push notification. To provide some additional flexibility in this scenario, two public interfaces are provided which allow a custom push notification factory (`IMessagingPushNotificationFactory`) or a custom notification image downloader (`IMessagingImageDownloader`) instance to be set. After these interfaces are implemented on the app side, they can be set via the new `setPushNotificationFactory` and `setPushImageDownloader` API.

{% hint style="info" %}

If the AEPMessaging extension will be used to handle push notification interactions, ensure that your custom push notification factory sets a `PendingIntent` object for the content intent (`notificationBuilder.setContentIntent()`), delete intent (`notificationBuilder.setDeleteIntent()`), or button(s) when creating a push notification.

{% endhint %}

##### To get started with the AEPMessaging 1.1.0 push notification features follow these steps:

#### Step 1: Add the AEPMessaging receivers in the App manifest

Within your App's `AndroidManifest.xml` file, add a [manifest-declared receiver](https://developer.android.com/guide/components/broadcasts#manifest-declared-receivers) inside the application tag to subscribe to broadcast actions sent by the AEPMessaging extension. A second manifest-declared receiver must be added to listen for notification interactions if AEPMessaging handled push notification interaction tracking will be used:

```groovy
 <!--messaging extension handled push notification broadcast receiver-->
   <receiver
			android:name=".NotificationBroadcastReceiver"
			android:exported="false">
      <intent-filter>
    		<action android:name="${applicationId}_adb_action_notification_clicked" />
        <action android:name="${applicationId}_adb_action_button_clicked" />
        <action android:name="${applicationId}_adb_action_notification_deleted" />
        <action android:name="${applicationId}_adb_action_notification_created" />
        <action android:name="${applicationId}_adb_action_silent_notification_created" />
      </intent-filter>
	</receiver>

<!--messaging extension handled push notification interactions broadcast receiver-->
  <receiver
			android:name="com.adobe.marketing.mobile.MessagingPushInteractionHandler"
      android:exported="false" >
  </receiver>
```

{% hint style="info" %}
The intent filters within the first receiver can be added to an existing manifest-declared `BroadcastReceiver` to listen for any notification events sent by the  AEPMessaging extension.

{% endhint %}

#### Step 2: Call the new AEPMessaging push notification creation API

In the `FirebaseMessagingService#onMessageReceived` function of your app, invoke `handlePushNotificationWithRemoteMessage` with the `RemoteMessage` received from Firebase Cloud Messaging. Additionally, a boolean flag enabling AEPMessaging push notification interaction tracking is required when invoking the API.

```java
public void onMessageReceived(RemoteMessage message) {
  super.onMessageReceived(message);
  // AEPMessaging handling of the push payload. If shouldHandleTracking is true then the AEPMessaging extension 	will handle push notification interaction tracking automatically.
  Messaging.handlePushNotificationWithRemoteMessage(message, true);
}
```

#### Step 3: Add/Update a Broadcast Receiver object to listen for AEPMessaging created push notification broadcasts

The AEPMessaging extension will broadcast events on normal notification creation, silent notification creation, notification deletion, notification click, or notification button presses. A `BroadcastReceiver` [must be declared in the AndroidManifest.xml](#Step 1: Adding the AEPMessaging receivers in the App manifest) and a class subclassing `BroadcastReceiver` must be added to handle the broadcasted events:

```java
public void onReceive(Context context, Intent intent) {
  String action = intent != null ? intent.getAction() : null;
  String packageName = context != null ? context.getPackageName() : null;
  // these values are broadcast when a silent push notification is handled by the Messaging extension
  MessagingPushPayload pushPayload = null;
  String messageId = null;

  if (action != null && packageName != null) {
    if (action.equals(packageName + "_adb_action_notification_clicked")) {
      Log.d("NotificationBroadcast", action);
    } else if (action.equals(packageName + "_adb_action_notification_deleted")) {
      Log.d("NotificationBroadcast", packageName + "_adb_action_notification_deleted");
    } else if (action.equals(packageName + "_adb_action_button_clicked")) {
      Log.d("NotificationBroadcast", packageName + "_adb_action_button_clicked");
    } else if (action.equals(packageName + "_adb_action_notification_created")) {
      Log.d("NotificationBroadcast", packageName + "_adb_action_notification_created");
    } else if (action.equals(packageName + "_adb_action_silent_notification_created")) {
      Log.d("NotificationBroadcast", packageName + "_adb_action_silent_notification_created");
      Bundle extras = intent.getExtras();
      if (extras != null) {
        pushPayload = (MessagingPushPayload) extras.getParcelable("pushPayload");
        messageId = extras.getString("messageId");
      }
    }
  }
}
```

To confirm that the `BroadcastReceiver` is correctly receiving broadcasted actions, verify that the logging above is displayed in the `adb` debug logs:

```
D/NotificationBroadcast: com.adobe.marketing.mobile.messagingsample.push_adb_action_silent_notification_created
D/NotificationBroadcast: com.adobe.marketing.mobile.messagingsample.push_adb_action_notification_created
```

## Android AEPMessaging 1.1.0 API Reference
### handlePushNotificationWithRemoteMessage

In the `FirebaseMessagingService#onMessageReceived` function of your app, invoke `handlePushNotificationWithRemoteMessage` with the `RemoteMessage` received from Firebase Cloud Messaging. Additionally, a boolean flag enabling AEPMessaging push notification interaction tracking is required when invoking the API.

**Syntax**

```java
public static boolean handlePushNotificationWithRemoteMessage(final RemoteMessage remoteMessage, final boolean shouldHandleTracking);
```

| Variable             | Type          | Description                                                  |
| -------------------- | ------------- | ------------------------------------------------------------ |
| remoteMessage        | RemoteMessage | Remote message received from FCM containing an AJO push data notification |
| shouldHandleTracking | Boolean       | If true, the Messaging extension should handle push notification tracking |

**Example**

```java
public void onMessageReceived(RemoteMessage message) {
  super.onMessageReceived(message);
  Messaging.handlePushNotificationWithRemoteMessage(message, true);
}
```

## Push notification creation customization

The Messaging extension defines two interfaces (`IMessagingPushNotificationFactory` and `IMessagingImageDownloader`) which can be implemented to customize the Messaging extension's creation of push notifications as well as customize the downloading of push notification image assets. Alongside these interfaces, two setters have been added to set custom instances of these interfaces within the Messaging extension:

##### IMessagingPushNotificationFactory interface

```java
public interface IMessagingPushNotificationFactory {
  /**
   * Creates a push notification from the given {@link MessagingPushPayload}.
   *
   * @param context              the application {@link Context}
   * @param payload              the {@code MessagingPushPayload} containing the data payload from AJO
   * @param messageId            a {@code String} containing the message id
   * @param notificationId       {@code int} id used when the notification was scheduled
   * @param shouldHandleTracking {@code boolean} if true the AEPMessaging extension will handle notification interaction tracking
   * @return the created {@link Notification}
   */
   Notification create(Context context, MessagingPushPayload payload, String messageId, int notificationId,
                       boolean shouldHandleTracking);
}
```

##### IMessagingImageDownloader interface

```java
public interface IMessagingImageDownloader {
  /**
   * Downloads the image asset referenced in the image URL {@code String}.
   *
   * @param context  the application {@link Context}
   * @param imageUrl a {@code String} containing the image asset to be downloaded
   * @return the {@link Bitmap} created from the downloaded image asset
   */
   Bitmap getBitmapFromUrl(Context context, String imageUrl);
}
```

## setPushNotificationFactory

**Syntax**

```java
public static void setPushNotificationFactory(final IMessagingPushNotificationFactory factory);
```

**Example**

```java
// customFactory is an instance of a class which implements IMessagingPushNotificationFactory
Messaging.setPushNotificationFactory(customFactory);
```

## setPushImageDownloader

**Syntax**

```java
public static void setPushImageDownloader(final IMessagingImageDownloader downloader);
```

**Example**

```java
// customImageDownloader is an instance of a class which implements IMessagingImageDownloader
Messaging.setPushImageDownloader(customImageDownloader);
```