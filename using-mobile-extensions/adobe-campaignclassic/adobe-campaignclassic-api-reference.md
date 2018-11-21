# Campaign Classic API Reference

## registerDevice API

### Registering a user's device with Campaign Classic

{% tabs %}

{% tab title="Android" %}

Follow [Google's instructions](https://firebase.google.com/docs/cloud-messaging/android/client) to get your app ready to handle push notifications. Once you receive the FCM SDK registration token, you will need to send that token along with the device information to Campaign Classic using the registerDevice API.

### registerDevice

The registerDevice API will register a device with your Campaign Classic registration server. It takes the FCM registration token as a parameter along with a user key that identifies a user, such as an email address or login name. You may also provide a Map of custom key-value pairs that you want to associate with the registration. A boolean value is returned in the callback which signals whether the registration was successful.

#### Java

#### Syntax

```java
public static void registerDevice(final String token, final String userKey, final Map<String, Object> additionalParams, final AdobeCallback<Boolean> callback)
```

#### Example

```java
@Override
public void onNewToken(String token) {
    Log.d("TestApp", "Refreshed token: " + token);

    // If you want to send messages to this application instance or
    // manage this app's subscriptions on the server side, send the
    // Instance ID token to your app server.
    if (token != null) {
        		Log.d("TestApp", "FCM SDK registration token received : " + token);
                // Create a map of additional paramters
                Map<String, Object> additionalParams = new HashMap<String, Object>();
        		additionalParams.put("name", "John");
            	additionalParams.put("serial", 12345);
            	additionalParams.put("premium", true);
                // Send the registration info
				CampaignClassic.registerDevice(token, "johndoe@gmail.com", 					 			additionalParams,new AdobeCallback<Boolean>() {
					@Override
					public void call(final Boolean status) {
						Log.d("TestApp", "Registration Status: " + status);
					}
				});
  	}
}
```

{% endtab %}

{% tab title="iOS" %}

Follow [Apple's instructions](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1) to get your app ready to handle push notifications. Once you receive the APNS token, you will need to send that token with the device information to Campaign Classic using the registerDevice API.

### registerDevice

The registerDevice API will register a device with your Campaign Classic registration server. It takes the APNS token as a parameter alonng with a user key that identifies a user, such as an email address or login name. You may also provide a Map of custom key-value pairs that you want to associate with the registration. A boolean value is returned in the callback which signals whether the registration was successful.

#### Objective-C

#### Syntax

```objectivec
+ (void) registerDevice: (nonnull NSData*) token userKey: (nullable NSString*) userKey additionalParams: (nullable NSDictionary*) additionalParams callback: (nullable void (^) (BOOL success)) callback;
```

#### Example

```objectivec
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  // Set the deviceToken that the APNS has assigned to the device
  NSMutableDictionary *params = [[NSMutableDictionary alloc] initWithObjectsAndKeys:      	@"John", @"name", nil];
  [params setObject: [NSNumber numberWithInt:12345] forKey: @"serial"];
  [params setObject: [NSNumber numberWithBool:YES]  forKey: @"premium"];
    
[ACPCampaignClassic registerDevice:deviceToken userKey:@"johndoe@gmail.com" additionalParams:params callback:^(BOOL success) {
	NSLog(@"Registration Status: %d", success);
}
```

#### Swift

```swift
ACPCampaignClassic.registerDevice(deviceToken, userKey: userKey, additionalParams: additionalParams, callback: {(_ success: Bool?) -> Void in
            NSLog("Registration Status: %d", success)                                                                                                                        })
```

{% endtab %}
{% endtabs %}

## trackNotification API

### Tracking push notifications

Adobe Campaign Classic has two additional APIs used for tracking push message receive and opening.

{% tabs %}

{% tab title="Android" %}

### trackNotificationReceive

The trackNotificationReceive API sends notification tracking information to the configured Adobe Campaign Classic server. This API may be used to send tracking information when a notification is received on the device. If `trackInfo` is null or does not contain the necessary tracking identifiers, messageId `_mId` and deliveryId `_dId` no track request is sent.

#### Java

#### Syntax

```java
public static void trackNotificationReceive(final Map<String, String> trackInfo)
```

#### Example

```java
public class MyFirebaseMessagingService extends FirebaseMessagingService {
	@Override
	public void onMessageReceived(RemoteMessage remoteMessage) {
		Log.d("TestApp", "Receive message from: " + remoteMessage.getFrom());
		Map<String,String> payloadData = message.getData();
        
		// Check if message contains data payload.
		if (payloadData.size() > 0) {
            Map<String,String> trackInfo = new HashMap<>();
            trackInfo.put("_mId", payloadData.get("_mId"));
            trackInfo.put("_dId", payloadData.get("_dId"));
            
            // Send the tracking information for message received
        	CampaignClassic.trackNotificationReceive(trackInfo);
        }
	}
}
```

{% endtab %}

{% tab title="iOS" %}

### trackNotificationReceive

The trackNotificationReceive API sends notification tracking information to the configured Adobe Campaign Classic server. This API may be used to send tracking information when a notification is received on the device. You may pass the  `launchOptions` received before opening the application or  `userInfo` containing the received push payload in trackInfo. If `trackInfo` is null or does not contain the necessary tracking identifiers, broadlogId `_mId` and deliveryId `_dId`, no track request is sent.

#### Objective-C

#### Syntax

```objectivec
+ (void) trackNotificationReceive: (nonnull NSDictionary<NSString*, NSString*>*) trackInfo;
```

#### Example

```objectivec
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)launchOptions fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler 
{
    if ( launchOptions) NSLog(@"launchOptions: %@", [launchOptions description]);
    // Tracking silent push notification receive
    if ( [launchOptions[@"aps"][@"content-available"] intValue] == 1 ) {
        NSLog(@"Silent Push Notification");
        [ACPCampaignClassic trackNotificationReceive:launchOptions];
        completionHandler(UIBackgroundFetchResultNoData);
    }
}
```

#### Swift

```swift
ACPCampaignClassic.trackNotificationReceive(trackInfo[String:String])
```

{% endtab %}
{% endtabs %}

{% tabs %}

{% tab title="Android" %}

### trackNotificationClick

The trackNotificationClick API sends notification tracking information to the configured Adobe Campaign Classic server. This API may be used to send tracking information when the notification is clicked. If `trackInfo` is null or does not contain the necessary tracking identifiers, messageId `_mId` and deliveryId `_dId`, no track request is sent.

#### Java

#### Syntax

```java
public static void trackNotificationClick(final Map<String, String> trackInfo)
```

#### Example

```java
@Override
public void onResume() {
	super.onResume();
	// Perform any other app related tasks 
    // The messageId (_mId) and deliveryId (_dId) can be passed in the intent extras.
    // This is assuming you extract the messageId and deliveryId from the
	// received push message and are including it in the intent (intent.putExtra())
    // of the displayed notification.
    
    Bundle extras = getIntent().getExtras();
	if (extras != null) {
        String deliveryId = extras.getString("_dId");
    	String messageId = extras.getString("_mId");
        if (deliveryId != null && messageId != null) {
            Map<String,String> trackInfo = new HashMap<>();
            trackInfo.put("_mId", messageId);
        	trackInfo.put("_dId", deliveryId);
        
        	// Send the tracking information for message opening
			CampaignClassic.trackNotificationClick(trackInfo);
        }
	}
}
```

{% endtab %}

{% tab title="iOS" %}

### trackNotificationClick

The trackNotificationClick API sends notification tracking information to the configured Adobe Campaign Classic server. This API may be used to send tracking information when the notification is clicked, which may result in opening the application. You may pass the  `launchOptions` received before opening the application or  `userInfo` containing the received push payload in trackInfo. If `trackInfo` is null or does not contain the necessary tracking identifiers, broadlogId `_mId` and deliveryId `_dId`, no track request is sent.

#### Objective-C

#### Syntax

```objectivec
+ (void) trackNotificationClick: (nonnull NSDictionary<NSString*, NSString*>*) trackInfo;
```

#### Example

```objectivec
-(void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler
{
    NSLog(@"User Info : %@",response.notification.request.content.userInfo);
    // Track action selected by the user for a given notification
	[ACPCampaignClassic 			trackNotificationClick:response.notification.request.content.userInfo];
completionHandler();
}
```

#### Swift

```swift
ACPCampaignClassic.trackNotificationClick(trackInfo[String:String])
```

{% endtab %}
{% endtabs %}