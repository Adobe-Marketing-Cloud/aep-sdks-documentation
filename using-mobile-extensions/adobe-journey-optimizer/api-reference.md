# API Reference

## extensionVersion <a id="extensionversion"></a>

Returns the library version.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static String extensionVersion();
```

#### Example

```java
Messaging.extensionVersion();
```
{% endtab %}

{% tab title="iOS" %}
### Swift

#### Syntax

```swift
public static let extensionVersion
```

#### Example

```swift
Messaging.extensionVersion
```

### Objective-C

#### Syntax

```swift
public static let extensionVersion
```

#### Example

```text
[AEPMobileMessaging extensionVersion];
```
{% endtab %}
{% endtabs %}

## handleNotificationResponse <a id="handlenotificationresponse"></a>

Transmits the push notification interactions feedback.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void handleNotificationResponse(final Intent intent, final boolean applicationOpened, final String customActionId);
```

* _intent_ - Intent which contains information related to messageId and data.
* _applicationOpened_ - boolean values denoting whether the application was opened or not. 
* _actionId_ - String values denoting the id of the custom action.

#### Example

```java
// Intent can be retrieved from the Activity/BroadcastReceiver using the getIntent() method. 
Intent intent = getIntent();
Messaging.handleNotificationResponse(intent, true, "customActionId");
```
{% endtab %}

{% tab title="iOS" %}
### Swift

#### Syntax

```swift
static func handleNotificationResponse(_ response: UNNotificationResponse, applicationOpened: Bool, customActionId: String?)
```

* _response_ - UNNotificationResponse response object containing push notification details 
* _applicationOpened_ - Bool values denoting whether the application was opened or not. 
* _customActionId_ - Option String values denoting the id of the custom action.

#### Example

```swift
func userNotificationCenter(_: UNUserNotificationCenter,
                                didReceive response: UNNotificationResponse,
                                withCompletionHandler completionHandler: @escaping () -> Void) {
    Messaging.handleNotificationResponse(response, applicationOpened: true, customActionId: "customActionId")
    completionHandler()
}
```

### Objective-C

#### Syntax

```text
@objc(handleNotificationResponse:applicationOpened:withCustomActionId:)
static func handleNotificationResponse(_ response: UNNotificationResponse, applicationOpened: Bool, customActionId: String?)
```

#### Example

```text
- (void)userNotificationCenter:(UNUserNotificationCenter *)center
didReceiveNotificationResponse:(UNNotificationResponse *)response
         withCompletionHandler:(void (^)())completionHandler {
    // Your code
    [AEPMobileMessaging handleNotificationResponse:response applicationOpened:true withCustomActionId:@"customActionId"]
    completionHandler();
}
```
{% endtab %}
{% endtabs %}

## registerExtension <a id="registerextension"></a>

Registers the extension with the [Mobile Core](../../foundation-extensions/mobile-core/).

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static void registerExtension();
```

#### Example

```java
Messaging.registerExtension();
```
{% endtab %}

{% tab title="iOS" %}
### Swift

Use the MobileCore API to register the Messaging extension.

#### Syntax

```swift
public static func registerExtensions(_ extensions: [NSObject.Type], _ completion: (() -> Void)? = nil)
```

#### Example

```swift
MobileCore.registerExtensions([Messaging.self, ...], {
  // processing after registration
})
```

### Objective-C

Use the AEPMobileCore API to register the Messaging extension.

#### Syntax

```swift
public static func registerExtensions(_ extensions: [NSObject.Type], _ completion: (() -> Void)? = nil)
```

#### Example

```text
[AEPMobileCore registerExtensions:@[AEPMobileMessaging.class, ...] completion:^{
  // processing after registration
}];
```
{% endtab %}
{% endtabs %}

## setPushIdentifier <a id="setpushidentifier"></a>

Although this API is provided in Mobile Core, the use of this API is required and leveraged by the Adobe Journey Optimizer extension to sync provided push tokens with Adobe Experience Platform services.

{% tabs %}
{% tab title="Android" %}
To retrieve the push token from Firebase Messaging Service follow this [Firebase documentation](https://firebase.google.com/docs/cloud-messaging/android/client#retrieve-the-current-registration-token). After retrieving the push token use the below core API to sync it with profile in platform.

### Java

#### Syntax

```java
public static void setPushIdentifier(final String pushIdentifier);
```

* _pushIdentifier_ - A `String` value denoting the push token.

#### Examples

```java
FirebaseMessaging.getInstance().getToken()
        .addOnCompleteListener(new OnCompleteListener<String>() {
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

{% tab title="iOS" %}
### Swift

To retrieve the push token in iOS, checkout the apple documentation [Apple's documentation](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns).  
After retrieving the push token use the below core API to sync it with profile in platform.

#### Syntax

```swift
public static func setPushIdentifier(_ deviceToken: Data?)
```

* _deviceToken_ - A `Data` value denoting the push token.

#### Examples

```swift
func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    MobileCore.setPushIdentifier(deviceToken)
}
```

### Objective-C

#### Syntax

```text
public static func setPushIdentifier(_ deviceToken: Data?)
```

* _deviceToken_ - A `Data` value denoting the push token.

#### Examples

```text
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken { 
    [AEPMobileCore setPushIdentifier:deviceToken];
}
```
{% endtab %}
{% endtabs %}

## addPushTrackingDetails <a id="addpushtrackingdetails"></a>

This API is used to updated the push notification pending intent with necessary customer journey information.

{% hint style="warning" %}
Call to this API is necessary to ensure that all the important information (messageId, Customer journey information) are added to the pending intent so that they can be used while tracking the push notification interactions.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public static boolean addPushTrackingDetails(final Intent intent, final String messageId, final Map<String, String> data)
```

* _intent_ - `Intent` which is added to the pending intent so that it can be used when user interacts with the notification.
* _messageId_ - `String` message ID of the push notification
* _data_ - `Map` which represents the data part of the remoteMessage.
* Returns `boolean` indicating whether the intent was updated with necessary information (messageId and customer journey data).

#### Examples

```java
boolean success = addPushTrackingDetails(intent, messageId, data)
```
{% endtab %}
{% endtabs %}

## Public Classes

### MessagingPushPayload

This is a helper class for extracting the data payload attributes from `RemoteMessage` which are used while creating the push notification. Create the instance of `MessagingPushPayload` in the `onMessageReceived` method using the below constructors.

### Constructor

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public MessagingPushPayload(RemoteMessage message)
```

* _message_ - `RemoteMessage` message containing the payload data with the necessary attributes for creating push notification

```java
public MessagingPushPayload(Map<String, String> data)
```

* _data_ - `Map<String, String>` data payload containing the necessary attributes for creating push notification

#### Examples

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

Public APIs for getting attributes from push payload which are used while creating the push notification.

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

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
// Check out the firebase documentation here (https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#notificationpriority) 
public int getNotificationPriority()

// Returns the channel Id from the remote message. 
public String getChannelId()

// Returns the icon string from the remote message.
// The icon string represents the drawable resource name in the app.
public String getIcon()

// Returns the image url from the remote message.
// The icon string represents the drawable resource name in the app.
public String getImageUrl()

// Returns the data map from the remote message.
public Map<String, String> getData()

// Returns an ActionType object which represents the type of action which needs to be performed on push notification interaction.
// Check the ActionType enum definition below.
public ActionType getActionType()

// Returns a String action uri which is used to direct the push notification interaction.
public String getActionUri()

// Returns a list of ActionButtons. Check the ActionButtons class definition below
public List<ActionButton> getActionButtons()
```

**Internal Classes and Enums**

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

### Payload Keys

Description of Push Notification payload keys

{% tabs %}
{% tab title="iOS" %}
```javascript
{
   "aps":{
      "alert":{
         "title":"Hello from CJM",
         "body":"Stay safe, wear mask"
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

| Key | Description |  |
| :--- | :--- | :--- |
| adb\_media | URL of the rich media like image/video/gif. This url can be used to download the rich media before showing the push notification. |  |
| adb\_uri | Web URL / Deeplink URI - Used to open appropriate webpage/app screen when notification is clicked. |  |
| adb\_a\_type | Can be one of the following string `DEEPLINK / WEBURL / DISMISS`. Used to determine what type of action to be performed when notification is clicked. |  |
| adb\_act | `Array` containing the Action json object. |  |
| aid | Part of action object denoting the action ID |  |
| label | Part of action object denoting the action name |  |
| type | Part of action object denoting the action type. Can have one of the following value `DEEPLINK / WEBURL / DISMISS` |  |
{% endtab %}

{% tab title="Android" %}
{% hint style="info" %}
We recommend you use the `MessagingPushPayload` class for extracting the payload values.
{% endhint %}

```javascript
{
   "message":{
      "android":{
         "collapse_key": "new_message",
         "priority": "HIGH",
         "data":{
            "adb_title":"Game Request",
            "adb_body":"Bob wants to play poker",
            "adb_sound" : "somesound_res",
            "adb_n_count" : "3",
            "." : "PRIORITY_LOW",
            "adb_channel_id": "cid",
            "adb_icon" : "notification_icon",
            "adb_image": "www.imageUrl.com",           
            "adb_a_type": "DEEPLINK/WEBURL/DISMISS",
            "adb_uri" : "uri/weburl",
            "adb_act" : "[\n            {\n \"label\" : \"deeplink\",\n \"uri\" : \"notificationapp://\",\n \"type\" : \"DEEPLINK\"\n },\n {\n \"label\" : \"weburl\",\n \"uri\" : \"https://www.yahoo.com\",\n \"type\" : \"WEBURL\"\n},\n{\n\"label\" : \"dismiss\",\n\"uri\" : \"\",\n \"type\" : \"DISMISS\"\n}\n]",          
            "some_custom_data_key": "some data"
         }
      }
   }
}
```

| Key | Description |
| :--- | :--- |
| adb\_title | String value denoting the push notification title |
| adb\_body | String value denoting the push notification body |
| adb\_sound | String value denoting the push notification sound |
| adb\_n\_count | String value denoting the push notification badge count |
| adb\_n\_priority | String value denoting the push notification priority Check firebase [documentation](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages#notificationpriority) |
| adb\_channel\_id | String value denoting the push notification channel id |
| adb\_icon | String value denoting the push notification icon resource name |
| adb\_image | URL of the image to be displayed on the notification |
| adb\_a\_type | Can be one of the following string `DEEPLINK / WEBURL / DISMISS`. Used to determine what type of action to be performed when notification is clicked. |
| adb\_uri | Web URL / Deeplink URI - Used to open appropriate webpage/app screen when notification is clicked. |
| adb\_act | String value denoting the action objects with label, uri and type. |
| label | Part of `adb_act` string denoting the action type. |
| uri | Part of `adb_act` string denoting the uri of the action |
| type | Part of `adb_act` string denoting the action type. Can have one of the following value `DEEPLINK / WEBURL / DISMISS` |
{% endtab %}
{% endtabs %}

