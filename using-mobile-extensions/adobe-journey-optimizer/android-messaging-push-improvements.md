# Android Messaging Push Notification Improvements

Messaging extension 1.1.0 introduces Messaging extension handled push notification creation and tracking. This new functionality provides a convenient way to display and track interactions with Adobe Journey Optimizer (AJO) created push notifications. The steps below will serve as a guide to enabling the new features provided in Messaging 1.1.0.

{% hint style="info" %}

The usage of these features is optional and no code changes are required if not using them.

{% endhint %}

When using Messaging handled push notification interaction tracking, the Messaging extension must also be used to create the push notification. To provide some additional flexibility in this scenario, two public interfaces are provided which allow a custom push notification factory (`IMessagingPushNotificationFactory`) or a custom notification image downloader (`IMessagingImageDownloader`) instance to be set. After these interfaces are implemented on the app side, they can be set via the new `setPushNotificationFactory` and `setPushImageDownloader` API.

{% hint style="info" %}

If the Messaging extension will be used to handle push notification interactions, ensure that your custom push notification factory sets a `PendingIntent` object for the content intent (`notificationBuilder.setContentIntent()`), delete intent (`notificationBuilder.setDeleteIntent()`), or button(s) when creating a push notification.

{% endhint %}

##### To get started with the Messaging 1.1.0 push notification features follow these steps:

#### Step 1: Add the Messaging receivers in the App manifest

Within your App's `AndroidManifest.xml` file, add a [manifest-declared receiver](https://developer.android.com/guide/components/broadcasts#manifest-declared-receivers) inside the application tag to subscribe to broadcast actions sent by the Messaging extension. A second manifest-declared receiver must be added to listen for notification interactions if Messaging handled push notification interaction tracking will be used:

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

The intent filters within the first receiver can be added to an existing manifest-declared `BroadcastReceiver` to listen for any notification events sent by the  Messaging extension.

{% endhint %}

#### Step 2: Call the new Messaging push notification creation API

In the `FirebaseMessagingService#onMessageReceived` function of your app, invoke `handlePushNotificationWithRemoteMessage` with the `RemoteMessage` received from Firebase Cloud Messaging. Additionally, a boolean flag enabling Messaging push notification interaction tracking is required when invoking the API.

```java
public void onMessageReceived(RemoteMessage message) {
  super.onMessageReceived(message);
  // Messaging handling of the push payload. If shouldHandleTracking is true then the Messaging extension will handle push notification interaction tracking automatically.
  Messaging.handlePushNotificationWithRemoteMessage(message, true);
}
```

#### Step 3: Add/Update a Broadcast Receiver object to listen for Messaging created push notification broadcasts

The Messaging extension will broadcast events on normal notification creation, silent notification creation, notification deletion, notification click, or notification button presses. A `BroadcastReceiver` [must be declared in the AndroidManifest.xml](#Step 1: Adding the Messaging receivers in the App manifest) and a class subclassing `BroadcastReceiver` must be added to handle the broadcasted events:

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