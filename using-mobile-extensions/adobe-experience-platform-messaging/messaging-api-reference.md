# Messaging API reference

## extensionVersion <a id="extensionversion"></a>

Returns the version of the client-side Consent extension.

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

```objective-c
[AEPMobileMessaging extensionVersion];
```
{% endtab %}
{% endtabs %}

## handleNotificationResponse<a id="handlenotificationresponse"></a>

Sends the push notification interactions feedback to experience platform.

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
* _customActionId_ - String values denoting the id of the custom action.

#### Example

```swift
Messaging.handleNotificationResponse(response, applicationOpened: true, customActionId: "customActionId")
```

### Objective-C

#### Syntax

```objective-c
static func handleNotificationResponse(_ response: UNNotificationResponse, applicationOpened: Bool, customActionId: String?)
```

#### Example

```objective-c
[AEPMobileMessaging handleNotificationResponse:response applicationOpened:true withCustomActionId:@"customActionId"]
```
{% endtab %}
{% endtabs %}

## registerExtension <a id="registerextension"></a>

Registers the Messaging extension with the Mobile Core SDK.

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

```objective-c
[AEPMobileCore registerExtensions:@[AEPMobileMessaging.class, ...] completion:^{
  // processing after registration
}];
```

{% endtab %}
{% endtabs %}

## setPushIdentifier<a id="setpushidentifier"></a>

This Core API is used for syncing the push token to the profile in experience platform.

{% tabs %}
{% tab title="Android" %}

To retrieve the push token from Firebase Messaging Service follow this [link](https://firebase.google.com/docs/cloud-messaging/android/client#retrieve-the-current-registration-token). 
After retrieving the push token use the below core api to sync it with profile in platform.

### Java

#### Syntax

```java
public static void setPushIdentifier(final String pushIdentifier);
```

* *pushIdentifier* - A `String` value denoting the push token.

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

To retrieve the push token in iOS, checkout the apple documentation [here](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns).  
After retrieving the push token use the below core api to sync it with profile in platform.

#### Syntax

```swift
public static func setPushIdentifier(_ deviceToken: Data?)
```

* *deviceToken* - A `String` value denoting the push token..

#### Examples

```swift
func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
    MobileCore.setPushIdentifier(deviceToken)
}
```

### Objective-C

#### Syntax

```objective-c
public static func setPushIdentifier(_ deviceToken: Data?)
```

#### Examples

```objective-c
- (void)application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken { 
    [AEPMobileCore setPushIdentifier:deviceToken];
}
```

{% endtab %}
{% endtabs %}

## addPushTrackingDetails<a id="addpushtrackingdetails"></a>

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

* *intent* - `Intent` which is added to the pending intent so that it can be used when user interacts with the notification.
* *messageId* - `String` message ID of the push notification
* *data* - `Map` which represents the data part of the remoteMessage.
* Returns `boolean` indicating whether the intent was update with necessary information (messageId and customer journey data).


#### Examples

```java
boolean update = addPushTrackingDetails(intent, messageId, data)
```

{% endtab %}
{% endtabs %}

## Public Classes
### AEPMessagingFCMPushPayload

This is a helper class for extracting the data payload attributes from `RemoteMessage` which are used while creating the push notification.
Create the instance of `AEPMessagingFCMPushPayload` in the `onMessageReceived` method using the below constructors.

### Constructor

{% tabs %}
{% tab title="Android" %}
### Java

#### Syntax

```java
public AEPMessagingFCMPushPayload(RemoteMessage message)
```

* *message* - `RemoteMessage` message containing the payload data with the necessary attributes for creating push notification

```java
public AEPMessagingFCMPushPayload(Map<String, String> data)
```

* *data* - `Map<String, String>` data payload containing the necessary attributes for creating push notification

#### Examples

```java
// Using the remote message
@Override
public void onMessageReceived(@NonNull RemoteMessage remoteMessage) {
    AEPMessagingFCMPushPayload payload = new AEPMessagingFCMPushPayload(remoteMessage);
}

// Using the data map
@Override
public void onMessageReceived(@NonNull RemoteMessage remoteMessage) {
    AEPMessagingFCMPushPayload payload = new AEPMessagingFCMPushPayload(remoteMessage.getData());
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

##### Internal Classes and Enums

###### ActionType

```java
public enum ActionType {
    DEEPLINK, WEBURL, DISMISS, NONE
}
```

###### ActionButtons
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

