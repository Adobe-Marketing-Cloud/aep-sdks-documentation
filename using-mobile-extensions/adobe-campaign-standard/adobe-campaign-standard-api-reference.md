# Adobe Campaign Standard API reference

## Get the extension version

To return the current version of the Campaign extension, use the following APIs:

{% tabs %}
{% tab title="Android" %}

### extensionVersion

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

### extensionVersion

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

### extensionVersion

#### JavaScript

```javascript
ACPCampaign.extensionVersion().then(version => console.log("AdobeExperienceSDK: ACPCampaign version: " + version));
```
{% endtab %}
{% endtabs %}

## Set linkage fields

This API sets the Campaign linkage fields (CRM IDs) in the mobile SDK that are used to download personalized messages from Campaign. The set linkage fields are stored as a base64 encoded JSON string in memory, and they are sent in a custom HTTP header `X-InApp-Auth` in all future Campaign rules download requests until `resetLinkageFields` is invoked. These in-memory variables are also lost in the wake of an Application crash event or upon graceful Application termination or when the privacy status is updated to OPT_OUT. For more information, see [Preparing and sending an In-App message](https://helpx.adobe.com/campaign/standard/channels/using/preparing-and-sending-an-in-app-message.html).

{% tabs %}
{% tab title="Android" %}

### setLinkageFields

#### Java

#### Syntax

```java
public static void setLinkageFields(final Map<String, String> linkageFields)
```

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

### setLinkageFields

#### Syntax

```objectivec
+ (void) setLinkageFields: (nonnull NSDictionary<NSString*, NSString*>*) linkageFields;
```

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

### setLinkageFields

```javascript
ACPCampaign.setLinkageFields({"linkageKey": "linkageValue"});
```
{% endtab %}
{% endtabs %}

## Reset linkage fields

This method clears cached rules from previous download before triggering a rule download request to the configured Campaign server. If the current SDK privacy status is not OPT_IN, no rules download happens.

{% tabs %}
{% tab title="Android" %}

### resetLinkageFields

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
### resetLinkageFields

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

### resetLinkageFields

```javascript
ACPCampaign.resetLinkageFields();
```
{% endtab %}
{% endtabs %}

## Set up push messaging

To enable push messaging with Adobe Campaign, the push identifier that is received from the Apple Push Notification Service (APNS) or Firebase Cloud Messaging (FCM) must be sent to the Adobe Identity service by calling `setPushIdentifer`. After the API is invoked, a network request is made to Campaign that contains the message interaction event. For more information about Campaign message interaction events, see [Implementing local notification tracking](https://helpx.adobe.com/campaign/kb/local-notification-tracking.html#Description).

For more information about setting up your iOS app to connect to APNS and retrieve a device token that will be used as a push identifier, see https://developer.apple.com/documentation/usernotifications/registering_your_app_with_apns?language=objc.
For more information about setting up your Android app to connect to FCM and retrieve a device registration token that will be used as a push identifier, see https://firebase.google.com/docs/cloud-messaging/android/client..

{% tabs %}
{% tab title="Android" %}

### setPushIdentifier

#### Syntax

```java
public static void setPushIdentifier(final String registrationID)
```

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
### setPushIdentifier

#### Syntax

```objectivec
+ (void) setPushIdentifier: (nullable NSData*) deviceToken;
```

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
### setPushIdentifier

#### JavaScript

```javascript
ACPCore.setPushIdentifier("pushIdentifier");
```
{% endtab %}
{% endtabs %}

## Tracking push or local notification message interactions

User interactions with local or push notifications can be tracked by invoking the `collectMessageInfo` API. After the API is invoked, a network request will be made to Campaign containing the message interaction event. For more info on Campaign message interaction events, see [Implementing local notification tracking](https://helpx.adobe.com/campaign/kb/local-notification-tracking.html#Description). 

{% tabs %}
{% tab title="Android" %}

### collectMessageInfo

#### Syntax

```java
public static void collectMessageInfo(final Map<String, Object> messageInfo)
```

#### Example

```java
@Override
protected void onResume() {
    super.onResume();
    handleTracking();
}
// handle a push or local notification click  
private void handleTracking() {
    // Check to see if this view was opened based on a notification
    Intent intent = getIntent();
    Bundle data = intent.getExtras();
  	if(data != null) {
			HashMap<String,Object> userInfo = (HashMap)data.get("NOTIFICATION_USER_INFO");
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

### collectMessageInfo

#### Syntax

```objectivec
+ (void) collectMessageInfo: (nonnull NSDictionary*) messageInfo;
```

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

