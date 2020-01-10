# Adobe Campaign Standard API reference

## extensionVersion

To return the current version of the Campaign extension, use the following APIs:

{% tabs %}
{% tab title="Android" %}

#### Java

#### Syntax

```java
public String extensionVersion()
```

#### Example

```java
Campaign.extensionVersion();
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (nonnull NSString*) extensionVersion;
```

#### Objective-C

#### Example

```objectivec
NSLog(@"ACPCampaign version: %@", [ACPCampaign extensionVersion]);
```

#### Swift

#### Example

```swift
print("ACPCampaign version: ", ACPCampaign.extensionVersion())
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

#### Syntax

```javascript
ACPCampaign.extensionVersion(): Promise<string>
```

#### Example

```javascript
ACPCampaign.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPCampaign version: " + version));
```
{% endtab %}
{% endtabs %}

## setLinkageFields

This API sets the Campaign linkage fields \(CRM IDs\) in the Mobile SDK that are used to download personalized messages from Campaign. The set linkage fields are stored as a base64-encoded JSON string in memory, and they are sent in a custom HTTP header `X-InApp-Auth` in all future Campaign rules download requests until `resetLinkageFields` is invoked. These in-memory variables are lost when an application crash event occurs, after a graceful termination of the application, or when the privacy status is updated to `OPT_OUT`. For more information, see [Preparing and sending an In-App message](https://helpx.adobe.com/campaign/standard/channels/using/preparing-and-sending-an-in-app-message.html).

{% tabs %}
{% tab title="Android" %}

#### Java

#### Syntax

```java
public static void setLinkageFields(final Map<String, String> linkageFields)
```

- *linkageFields* is a map that contains the linkage field key-value pairs.

#### Example

```java
HashMap<String, String> linkageFields = new HashMap<String, String>();
linkageFields.put("cusFirstName", "John");
linkageFields.put("cusLastName", "Doe");
linkageFields.put("cusEmail", "john.doe@email.com");
Campaign.setLinkageFields(linkageFields);
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

- *linkageFields* is a dictionary that contains the linkage field key-value pairs.

#### Example

#### Objective-C

```objectivec
[ACPCampaign setLinkageFields:@{@"cusFirstName" : @"John", @"cusLastName": @"Doe", @"cusEmail": @"john.doe@email.com"}];
```

#### Swift

```swift
var linkageFields = [String: String]()
linkageFields["cusFirstName"] = "John"
linkageFields["cusLastName"] = "Doe"
linkageFields["cusEmail"] = "john.doe@email.com"
ACPCampaign.setLinkageFields(linkageFields)
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

#### Syntax

```javascript
ACPCampaign.setLinkageFields(linkageFields: { string: string })
```

- *linkageFields* is a map that contains the linkage field key-value pairs.

#### Example

```javascript
ACPCampaign.setLinkageFields({"firstName": "John"});
```
{% endtab %}
{% endtabs %}

## resetLinkageFields

This method clears the cached rules from the previous download before triggering a rule download request to the configured Campaign server. If the current SDK privacy status is not OPT\_IN, no rules download occurs.

{% tabs %}
{% tab title="Android" %}

#### Syntax

```java
public static void resetLinkageFields()
```

#### Example

```java
Campaign.resetLinkageFields()
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (void) resetLinkageFields;
```

#### Objective-C

#### Example

```objectivec
[ACPCampaign resetLinkageFields];
```

#### Swift

```swift
ACPCampaign.resetLinkageFields()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

#### Syntax

```javascript
ACPCampaign.resetLinkageFields();
```

#### Example

```javascript
ACPCampaign.resetLinkageFields();
```
{% endtab %}
{% endtabs %}

## setPushIdentifier

To enable push messaging with Adobe Campaign, the push identifier that is received from the Apple Push Notification Service \(APNS\) or Firebase Cloud Messaging Platform \(FCM\) must be sent to the Adobe Identity service by calling `setPushIdentifer`. More information regarding the `setPushIdentifer` API can be seen at [Identity API reference - setPushIdentifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/identity/identity-api-reference#setPushIdentifierTitle) After the API is invoked, a network request is made to Campaign that contains the message interaction event.

For more information about setting up your iOS app to connect to APNS and retrieve a device token that will be used as a push identifier, see [Registering Your App with APNs](https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns?language=objc). For more information about setting up your Android app to connect to FCM and retrieve a device registration token that will be used as a push identifier, see [Set up a Firebase Cloud Messaging client app on Android](https://firebase.google.com/docs/cloud-messaging/android/client).

{% tabs %}
{% tab title="Android" %}

#### Syntax

```java
public static void setPushIdentifier(final String registrationID)
```

- *registrationID*  is a string that contains the device token received from the Firebase Cloud Messaging Platform.

#### Example

```java
FirebaseInstanceId.getInstance().getInstanceId()
        .addOnCompleteListener(new OnCompleteListener<InstanceIdResult>() {
            @Override
            public void onComplete(@NonNull Task<InstanceIdResult> task) {
                if (!task.isSuccessful()) {
                    return;
                }
                // Get new Instance ID token
                String registrationID = task.getResult().getToken();
                // Log and toast
                System.out.println("Received new registration token: " + registrationID);
                // invoke the API to send the push identifier to the Identity Service
                MobileCore.setPushIdentifier(registrationID);
            }
});
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

- *deviceToken* is a string that contains the device token received from the Apple Push Notification Service.

#### Objective-C

#### Example

```objectivec
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  // Set the deviceToken that the APNS has assigned to the device
  [ACPCore setPushIdentifier:deviceToken];
  //...
}
```

#### Swift

#### Example

```swift
func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
  // Set the deviceToken that the APNS has assigned to the device
  ACPCore.setPushIdentifier(deviceToken)
  //...
}
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

#### Syntax

```javascript
ACPCore.setPushIdentifier(pushIdentifier);
```

- *pushIdentifier* is a string that contains the device token for push notifications.

#### Example

```javascript
ACPCore.setPushIdentifier("pushID");
```
{% endtab %}
{% endtabs %}

## collectMessageInfo

User interactions with local or push notifications can be tracked by invoking the `collectMessageInfo` API. After the API is invoked, a network request is made to Campaign that contains the message interaction event. For more information on Campaign message interaction events, see [Implementing local notification tracking](https://helpx.adobe.com/campaign/kb/local-notification-tracking.html#Description).

{% tabs %}
{% tab title="Android" %}

#### Syntax

```java
public static void collectMessageInfo(final Map<String, Object> messageInfo)
```

- *messageInfo* is a map which contains the delivery id, message id, and action type for a local notification which was interacted with. The delivery id and message id are extracted from the local notification payload while the action type is inferred from the method in which the local notification was interacted.  

#### Example

```java
@Override
protected void onResume() {
  super.onResume();
  handleTracking();
}

// handle a push or local notification click  
private void handleTracking() {
  Intent intent = getIntent();
  Bundle data = intent.getExtras();
  HashMap<String, Object> userInfo = null;

  if (data != null) {
    userInfo = (HashMap)data.get("NOTIFICATION_USER_INFO");
  } else {
    return;
  }

  // Check if we have local notification click through data.
  // If it is present, this view was opened based on a notification.
  if (userInfo != null) {
    String deliveryId = (String)userInfo.get("deliveryId");
    String broadlogId = (String)userInfo.get("broadlogId");

    HashMap<String, Object> contextData = new HashMap<>();

    if (deliveryId != null && broadlogId != null) {
      contextData.put("deliveryId", deliveryId);
      contextData.put("broadlogId", broadlogId);

      // Send Click Tracking since the user did click on the notification
      contextData.put("action", "2");
      MobileCore.collectMessageInfo(contextData);

      // Send Open Tracking since the user opened the app
      contextData.put("action", "1");
      MobileCore.collectMessageInfo(contextData);
    }
  }
}
```
{% endtab %}

{% tab title="iOS" %}
#### Syntax

```objectivec
+ (void) collectMessageInfo: (nonnull NSDictionary*) messageInfo;
```

- *messageInfo* is a dictionary which contains the delivery id, message id, and action type for a local notification which was interacted with. The delivery id and message id are extracted from the local notification payload while the action type is inferred from the way in which the local notification was interacted.  

#### Objective-C

#### Example

```objectivec
// Handle notification interaction from background or closed
-(void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler{
    NSLog(@"User Info : %@",response.notification.request.content.userInfo);
    dispatch_async(dispatch_get_main_queue(), ^{
        NSLog(@"App state : %ld",(long)[UIApplication sharedApplication].applicationState);
        NSDictionary *userInfo = response.notification.request.content.userInfo;
        NSString *broadlogId = userInfo[@"_mId"] ?: userInfo[@"broadlogId"];
        NSString *deliveryId = userInfo[@"_dId"] ?: userInfo[@"deliveryId"];

        // handle the user response to the local notification action buttons
        if([response.actionIdentifier isEqualToString:@"YES_ACTION"] || [response.actionIdentifier isEqualToString:UNNotificationDefaultActionIdentifier]){
            NSLog(@"Received a positive action with action identifier %@", response.actionIdentifier);

            if ([UIApplication sharedApplication].applicationState == UIApplicationStateInactive || [UIApplication sharedApplication].applicationState == UIApplicationStateBackground) {
                // App is launched from notification (action = "1")
                [self sendTracking:tOpen withBroadlogId:broadlogId andDeliveryId:deliveryId];
            }

            // Push or Local notification is clicked (action = "2")
            [self sendTracking:tClick withBroadlogId:broadlogId andDeliveryId:deliveryId];

        } else if ([response.actionIdentifier isEqualToString:@"NO_ACTION"] || [response.actionIdentifier isEqualToString:UNNotificationDismissActionIdentifier]){
            NSLog(@"Received a dismiss action with action identifier %@", response.actionIdentifier);

            // Push or Local notification is clicked (action = "2")
            [self sendTracking:tClick withBroadlogId:broadlogId andDeliveryId:deliveryId];  
        }
}

- (void) sendTracking:(TrackType)trackType withBroadlogId:(NSString *)broadlogId andDeliveryId:(NSString *)deliveryId {
    if (broadlogId != nil && deliveryId != nil) {
        NSString *action = nil;
        switch (trackType) {
            case tImpression:
                action = @"7";
                break;

            case tOpen:
                action = @"1";
                break;

            case tClick:
                action = @"2";
                break;

            default:
                NSLog(@"Received invalid tracking type, aborting send!");
                return;
        }
        [ACPCore collectMessageInfo:@{
                                      @"broadlogId" : broadlogId,
                                      @"deliveryId": deliveryId,
                                      @"action": action
                                      }];
    }
}
```

#### Swift

#### Example

```swift
func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
    print("User Info :", response.notification.request.content.userInfo)
    DispatchQueue.main.async {
        print(String(format: "App state :", UIApplication.shared.applicationState.rawValue))
        let userInfo = response.notification.request.content.userInfo
        let broadlogId = userInfo["_mId"] ?? userInfo["broadlogId"] as? String
        let deliveryId = userInfo["_dId"] ?? userInfo["deliveryId"] as? String

        // handle the user response to the local notification action buttons
        if (response.actionIdentifier == "YES_ACTION") || (response.actionIdentifier == UNNotificationDefaultActionIdentifier) {
            print("Received a positive action with action identifier", response.actionIdentifier)

        if UIApplication.shared.applicationState == .inactive || UIApplication.shared.applicationState == .background {
            // App is launched from notification (action = "1")
            self.sendTracking(tOpen, withBroadlogId: broadlogId, andDeliveryId: deliveryId)
        }

        // Push or Local notification is clicked (action = "2")
        self.sendTracking(tClick, withBroadlogId: broadlogId, andDeliveryId: deliveryId)
        } else if (response.actionIdentifier == "NO_ACTION") || (response.actionIdentifier == UNNotificationDismissActionIdentifier) {
            print("Received a dismiss action with action identifier",response.actionIdentifier)
            // Push or Local notification is clicked (action = "2")
            self.sendTracking(tClick, withBroadlogId: broadlogId, andDeliveryId: deliveryId)
        }
    }
}

func sendTracking(_ trackType: TrackType, withBroadlogId broadlogId: String?, andDeliveryId deliveryId: String?) {
    if broadlogId != nil && deliveryId != nil {
        var action: String? = nil
        switch trackType {
            case tImpression:
                action = "7"
            case tOpen:
                action = "1"
            case tClick:
                action = "2"
            default:
                print("Received invalid tracking type, aborting send!")
                return
        }
        ACPCore.collectMessageInfo([
        "broadlogId": broadlogId,
        "deliveryId": deliveryId,
        "action": action
        ])
    }
}
```
{% endtab %}
{% endtabs %}

