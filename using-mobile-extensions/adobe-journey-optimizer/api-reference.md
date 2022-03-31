# Adobe Journey Optimizer API reference

## extensionVersion <a id="extensionversion"></a>

The extensionVersion API returns the library version.

{% tabs %}

{% tab title="Android" %}

#### Java

**Syntax**

```java
public static String extensionVersion();
```

**Example**

```java
Messaging.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

#### Swift

**Syntax**

```swift
public static let extensionVersion
```

**Example**

```swift
Messaging.extensionVersion
```

#### Objective-C

**Syntax**

```swift
public static let extensionVersion
```

**Example**

```text
[AEPMobileMessaging extensionVersion];
```
{% endtab %}

{% endtabs %}

## handleNotificationResponse <a id="handlenotificationresponse"></a>

The handleNotificationResponse function transmits the push notification interaction feedback.

{% tabs %}

{% tab title="Android" %}

#### Java

**Syntax**

```java
public static void handleNotificationResponse(final Intent intent, final boolean applicationOpened, final String customActionId);
```

| Variable | Type | Description |
| :----------- | :------- | :-------------- |
| `intent` | Intent | The intent contains information related to the messageId and the data. |
| `applicationOpened` | Boolean | Shows whether the application has been opened or not. |
| `actionId` | String | The ID of the custom action. |

**Example**

```java
// Intent can be retrieved from the Activity/BroadcastReceiver using the getIntent() method.
Intent intent = getIntent();
Messaging.handleNotificationResponse(intent, true, "customActionId");
```

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

#### Swift

**Syntax**

```swift
static func handleNotificationResponse(_ response: UNNotificationResponse, applicationOpened: Bool, customActionId: String?)
```

| Variable | Type | Description |
| :----------- | :------- | :-------------- |
| `response` | UNNotificationResponse | An object containing information about the push notification details. |
| `applicationOpened` | Boolean | Shows whether the application has been opened or not. |
| `customActionId` | String | The ID of the custom action. |

**Example**

```swift
func userNotificationCenter(_: UNUserNotificationCenter,
                                didReceive response: UNNotificationResponse,
                                withCompletionHandler completionHandler: @escaping () -> Void) {
    Messaging.handleNotificationResponse(response, applicationOpened: true, customActionId: "customActionId")
    completionHandler()
}
```

#### Objective-C

**Syntax**

```objc
@objc(handleNotificationResponse:applicationOpened:withCustomActionId:)
static func handleNotificationResponse(_ response: UNNotificationResponse, applicationOpened: Bool, customActionId: String?)
```

**Example**

```objc
- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response
         withCompletionHandler:(void (^)())completionHandler {    
    [AEPMobileMessaging handleNotificationResponse:response applicationOpened:YES withCustomActionId:@"customActionId"];
    completionHandler();
}
```

{% endtab %}

{% endtabs %}

## registerExtension <a id="registerextension"></a>

The registerExtension API lets you register your extension with the [Mobile Core](../../foundation-extensions/mobile-core/).

{% tabs %}

{% tab title="Android" %}

#### Java

**Syntax**

```java
public static void registerExtension();
```

**Example**

```java
Messaging.registerExtension();
```

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

#### Swift

Use the MobileCore API `registerExtensions` to register the Messaging extension.

**Syntax**

```swift
public static func registerExtensions(_ extensions: [NSObject.Type], _ completion: (() -> Void)? = nil)
```

**Example**

```swift
MobileCore.registerExtensions([Messaging.self, ...], {
    // processing after registration
})
```

#### Objective-C

Use the AEPMobileCore API `registerExtensions` to register the Messaging extension.

**Syntax**

```objc
public static func registerExtensions(_ extensions: [NSObject.Type], _ completion: (() -> Void)? = nil)
```

**Example**

```objc
[AEPMobileCore registerExtensions:@[AEPMobileMessaging.class, ...] completion:^{
    // processing after registration
}];
```

{% endtab %}

{% endtabs %}

## setPushIdentifier <a id="setpushidentifier"></a>

{% hint style="info" %}

Although this API is provided in Mobile Core, its use is required when implementing AJO for the purposes of syncing push tokens to Adobe Experience Platform services.

{% endhint %}

The setPushIdentifier API sets the push token, allowing you to sync it with Profile in Adobe Experience Platform.

{% tabs %}
{% tab title="Android" %}
{% hint style="info" %}
To retrieve the push token from Firebase Messaging Service, please follow the tutorial within the [Firebase documentation](https://firebase.google.com/docs/cloud-messaging/android/client#retrieve-the-current-registration-token).
{% endhint %}

#### Java

**Syntax**

```java
public static void setPushIdentifier(final String pushIdentifier);
```

| Variable | Type | Description |
| :----------- | :------- | :-------------- |
| `pushIdentifier` | String | The push token that is synced with Adobe Experience Platform. |

**Example**

```java
FirebaseMessaging.getInstance().getToken().addOnCompleteListener(new OnCompleteListener<String>() {
    @Override
    public void onComplete(@NonNull Task<String> task) {
        if (task.isSuccessful()) {
            String token = task.getResult();
            MobileCore.setPushIdentifier(token);
        }
    }
});
```

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

To retrieve the push token in iOS, please read the tutorial within [Apple's documentation](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns).  

#### Swift

**Syntax**

```swift
public static func setPushIdentifier(_ deviceToken: Data?)
```

| Variable | Type | Description |
| :----------- | :------- | :-------------- |
| `deviceToken` | Data | The push token that is synced with Adobe Experience Platform. |

**Example**

```swift
func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    MobileCore.setPushIdentifier(deviceToken)
}
```

#### Objective-C

**Syntax**

```objc
public static func setPushIdentifier(_ deviceToken: Data?)
```

| Variable | Type | Description |
| :----------- | :------- | :-------------- |
| `deviceToken` | Data | The push token that is synced with Adobe Experience Platform. |

**Example**

```objc
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
    [AEPMobileCore setPushIdentifier:deviceToken];
}
```

{% endtab %}

{% endtabs %}

## addPushTrackingDetails (Android only) <a id="addpushtrackingdetails"></a>

The `addPushTrackingDetails` API is used to update a pending intent with important information, such as messageId and Customer Journey information.

**Note:** Calling this API is mandatory, so the pending intent can be used while tracking push notification interactions.

{% tabs %}

{% tab title="Android" %}

#### Java

**Syntax**

```java
public static boolean addPushTrackingDetails(final Intent intent, final String messageId, final Map<String, String> data)
```

| Variable | Type | Description |
| :----------- | :------- | :-------------- |
| `intent` | `Intent` | The pending intent that needs to be updated so it can be used when the user interacts with the notification. |
| `messageId` | `String` | The message ID for the push notification. |
| `data` | `Map<String, String>` | The data of the remoteMessage. |

This API returns a boolean, indicating whether the intent was updated with necessary information (messageId and Customer Journey data).

**Example**

```java
boolean success = addPushTrackingDetails(intent, messageId, data)
```

{% endtab %}

{% endtabs %}

## Public classes

### MessagingPushPayload (Android only)

`MessagePushPayload` is a helper class for extracting the data payload attributes from `RemoteMessage`, which are used while creating the push notification.

{% tabs %}

{% tab title="Android" %}

#### Java

**Syntax**

```java
public MessagingPushPayload(RemoteMessage message)
```

| **Variable** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `message` | `RemoteMessage` | A message that contains the necessary attributes for creating a push notification. |

```java
public MessagingPushPayload(Map<String, String> data)
```

| **Variable** | **Type** | **Description** |
| :----------- | :------- | :-------------- |
| `data` | `Map<String, String>` | A data payload that contains the necessary attributes for creating a push notification. |

**Examples**

```java
// Using the remote message
@Override
public void onMessageReceived(@NonNull RemoteMessage remoteMessage) {
    MessagingPushPayload payload = new MessagingPushPayload(remoteMessage);
}

// Using the data map
@Override
public void onMessageReceived(@NonNull RemoteMessage remoteMessage) {
    MessagingPushPayload payload = new MessagingPushPayload(remoteMessage.getData());
}
```
{% endtab %}
{% endtabs %}

### Public APIs

Public APIs are used to get attributes from the push payload, which are used while creating the push notification.

{% tabs %}

{% tab title="Android" %}

#### Java

**Syntax**

```java
// Returns the title from the remote message
public String getTitle()

// Returns the body from the remote message
public String getBody()

// Returns the sound from the remote message
// The sound string represents the filename of a sound resource bundled in the app.
public String getSound()

// Returns the notification badge count from the remote message
public int getBadgeCount()

// Returns the notification priority from the remote message.
// For more information, please read the Firebase documentation (https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#notificationpriority)
public int getNotificationPriority()

// Returns the channel ID from the remote message.
public String getChannelId()

// Returns the icon string from the remote message.
// The icon string represents the drawable resource name in the app.
public String getIcon()

// Returns the image URL from the remote message.
public String getImageUrl()

// Returns the data map from the remote message.
public Map<String, String> getData()

// Returns an ActionType object which represents the type of action which needs to be performed on push notification interaction.
// More information about the ActionType enum definition can be found in the ActionType section below.
public ActionType getActionType()

// Returns the action URI as a string. The action URI is used to direct the push notification interaction.
public String getActionUri()

// Returns a list of ActionButtons. More information about the ActionButtons class definition can be found in the ActionButtons section below.
public List<ActionButton> getActionButtons()
```

**Internal classes and enums**

**ActionType**

```java
public enum ActionType {
    DEEPLINK, WEBURL, DISMISS, NONE
}
```

**ActionButtons**

```java
// Constructor
public ActionButton(final String label, final String link, final String type)

// Public APIs

// Returns the label for the action button
public String getLabel()

// Returns the link for the action button
public String getLink()

// Returns the ActionType for the action button
public ActionType getType()
```

{% endtab %}

{% endtabs %}

### Payload keys

{% tabs %}

{% tab title="Android" %}

{% hint style="info" %}
You should use the `MessagingPushPayload` class to extract the payload values.
{% endhint %}

**FCM Payload Example**

```json
{
   "message":{
      "android":{
         "collapse_key": "new_message",
         "priority": "HIGH",
         "data":{
            "adb_title":"Game Request",
            "adb_body":"Bob wants to play chess",
            "adb_sound" : "somesound_res",
            "adb_n_count" : "3",
            "." : "PRIORITY_LOW",
            "adb_channel_id": "cid",
            "adb_icon" : "notification_icon",
            "adb_image": "www.imageUrl.com",           
            "adb_a_type": "DEEPLINK/WEBURL/DISMISS",
            "adb_uri" : "uri/weburl",
            "adb_act": [
                {
                    "label" : "deeplink",
                    "uri" : "notificationapp://",
                    "type" : "DEEPLINK"
                },
                {
                    "label" : "weburl",
                    "uri" : "https://www.yahoo.com",
                    "type" : "WEBURL"
                },
                {
                    "label" : "dismiss",
                    "uri" : "",
                    "type" : "DISMISS"
                }
            ],          
            "some_custom_data_key": "some data"
         }
      }
   }
}
```

| Key | Type | Description |
| :------ | :------- | :-------------- |
| `adb_title` | String | The push notification's title |
| `adb_body` | String | The push notification's body |
| `adb_sound` | String | The push notification's sound |
| `adb_n_count` | String | The push notification badge count |
| `adb_n_priority` | String | The push notification's priority. For more information, please read the [Firebase documentation](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#notificationpriority) |
| `adb_channel_id` | String | The push notification's channel ID |
| `adb_icon` | String | The push notification's icon resource name |
| `adb_image` | String | The URL of the image to be displayed on the notification |
| `adb_a_type` | enum | An enum that determines what type of action will be performed when the notification is clicked. It can be one of the following values: `DEEPLINK`, `WEBURL`, or `DISMISS`. |
| `adb_uri` | String | The URI used for deeplinking. The deeplink is used to open the appropriate webpage or app screen when the notification is clicked. |
| `adb_act` | Array | An array that contains the action object(s). |
| `adb_act.label` | String | The label for the action object |
| `adb_act.uri` | String | The URI for the action object |
| `adb_act.type` | enum | The action type for the action object. It can be one of the following values: `DEEPLINK`, `WEBURL`, `DISMISS` |

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

**APNS Payload Example**

```json
{
   "aps":{
      "alert":{
         "title":"Hello from CJM",
         "body":"Have a good day!"
      },
      "sound":"dingDong",
      "badge":2,
      "mutable-content":1,
      "category":"iosCategory",
      "thread-id":"myGroup",
      "content-available":1
   },
   "a":"x",
   "b":"y",
   "adb_media":"www.imageUrl.com",
   "adb_a_type":"DEEPLINK/WEBURL/DISMISS",
   "adb_uri":"deeplink://url / weburl",
   "adb_act":[
      {
         "aid":"customId1",
         "label":"dismiss",
         "type":"DISMISS"
      }
   ]
}
```

| Key | Type | Description |
| :------ | :------- | :-------------- |
| `adb_media` | String | The URL of the media. In this situation, media refers to either an image or a video. This URL can be used to download the rich media before showing the push notification. |
| `adb_uri` | String | The URI used for deeplinking. The deeplink is used to open appropriate webpage or app screen when the notification is clicked. |
| `adb_a_type` | enum | An enum that determines what type of action will be performed when the notification is selected. It can be one of the following string values: `DEEPLINK`, `WEBURL`, `DISMISS`. |
| `adb_act` | Array | An array that contains the action object(s). |
| `adb_act.aid` | String | The ID for the action object. |
| `adb_act.label` | String | The name for the action object |
| `adb_act.type` | String | The type for the action object. It can be one of the following string values: `DEEPLINK`, `WEBURL`, `DISMISS` |

{% endtab %}

{% endtabs %}
