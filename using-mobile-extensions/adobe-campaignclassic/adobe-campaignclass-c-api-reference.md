# Campaign Classic API Reference

## registerDevice API

### Registering a user's device with Campaign Classic

{% tabs %}

{% tab title="Android" %}

Follow [Google's instruct

ions](https://firebase.google.com/docs/cloud-messaging/android/client) to get your app ready to handle push notifications. Once you receive the FCM SDK registration token, you will need to send that token along with the device information to Campaign Classic using the registerDevice API.

### registerDevice

The registerDevice API will register a device with your Campaign Classic registration server. It takes the FCM registration token as a parameter along with a user key that identifies the user such as an email address or login name. It can also be given a Map of custom key value pairs that you want to associate with the registration. Lastly, a boolean value is returned in the callback which signals whether the registration was sucessful.

#### Java

#### Syntax

```java
public static void registerDevice(final String deviceToken, final String userKey, final Map<String, Object> additionalParams, final AdobeCallback<Boolean> callback)
```

#### Example

```java
/**
 * Called if InstanceID token is updated. This may occur if the security of
 * the previous token had been compromised. Note that this is called when the InstanceID token
 * is initially generated so this is where you would retrieve the token.
 */
@Override
public void onNewToken(String token) {
    Log.d(TAG, "Refreshed token: " + token);

    // If you want to send messages to this application instance or
    // manage this apps subscriptions on the server side, send the
    // Instance ID token to your app server.
    if (token != null) {
				System.out.println("FCM SDK registration token received : " + token);
                // Create a map of additional paramters
                Map<String, Object> additionalParams = new HashMap<String, Object>();
            	additionalParams.put("testNum", 12345);
            	additionalParams.put("testBool", true);
            	additionalParams.put("brand", "Adobe");
                // Send the registration info
				CampaignClassic.registerDevice(token, "user@gmail.com", 					 			additionalParams,new AdobeCallback<Boolean>() {
					@Override
					public void call(final Boolean status) {
						Log.w(TAG, "Status: " + status;
					}
				});
  	}
}
```

{% endtab %}

{% tab title="iOS" %}

Follow [Apple's instructions](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1) to get your app ready to handle push notifications. Once you receive the APNS token, you will need to send that token along with the device information to Campaign Classic using the registerDevice API.

### registerDevice

The registerDevice API will register a device with your Campaign Classic registration server. It takes the APNS token as a parameter along with a user key that identifies the user such as an email address or login name. It can also be given a dictionary of custom key value pairs that you want to associate with the registration. Lastly, a boolean value is returned in the callback which signals whether the registration was sucessful.

#### Objective-C

#### Syntax

```objectivec
+ (void) registerDevice: (nonnull NSData*) token userKey: (nonnull NSString*) userKey additionalParams: (nullable NSDictionary*) additionalParams callback: (nullable void (^) (BOOL success)) callback;
```

#### Example

```objectivec
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  // Set the deviceToken that the APNS has assigned to the device
  NSMutableDictionary *params = [[NSMutableDictionary alloc] initWithObjectsAndKeys:      	@"Adobe", @"brand", nil];
  [params setObject: [NSNumber numberWithInt:12345] forKey: @"testNum"];
  [params setObject: [NSNumber numberWithBool:YES]  forKey: @"testBool"];
    
[ACPCampaignClassic registerDevice:deviceToken userKey:@"user@gmail.com" additionalParams:params callback:^(BOOL success) {
	NSLog(@"Status: %d", success);
}
```

#### Swift

```swift
ACPCampaignClassic.registerDevice(deviceToken, userKey: userKey, additionalParams: additionalParams, callback: {(_ success: Bool?) -> Void in
            NSLog("Status: %d", success)                                                                                                                        })
```

{% endtab %}
{% endtabs %}

## trackNotification API

### Tracking for push message receive and clickthrough

Adobe Campaign Classic has two additional API used for tracking push messages received and push messages clicked.

### trackNotificationReceive

The trackNotificationReceive API should be called after a push message has been received in the app. On iOS it takes a dictionary as a parameter and the dictionary should contain the message id and delivery id retrieved from the received push message. On Android, the API takes a map containing the same message id and delivery id received from the push message.

{% tabs %}

{% tab title="Android" %}

#### Java

#### Syntax

```java
public static void trackNotificationReceive(final Map<String, String> trackInfo)
```

#### Example

```java
public class MyFirebaseMessagingService extends FirebaseMessagingService {

	private NotificationManager notifManager;
	private Activity testActivity;

	@Override
	public void onMessageReceived(RemoteMessage remoteMessage) {

		System.out.println("From: " + remoteMessage.getFrom());

		// Check if message contains a data payload.
		if (remoteMessage.getData().size() > 0) {
			System.out.println("Message data payload: " + remoteMessage.getData());
            // Send the tracking info for message received
            String broadlogId = remoteMessage.getMessageId();
        	String deliveryId = remoteMessage.getFrom();
            Map<String,String> trackInfo = new HashMap<>();
        	trackInfo.put("broadlogid", broadlogId);
        	trackInfo.put("deliveryid", deliveryId);
        	CampaignClassic.trackNotificationReceieve(trackInfo);
	}
}
```

{% endtab %}

{% tab title="iOS" %}

#### Objective-C

#### Syntax

```objectivec
+ (void) trackNotificationReceive: (nonnull NSDictionary<NSString*, NSString*>*) trackInfo;
```

#### Example

```objectivec
// Invoked when a notification is delivered to a foreground application (TrackReceive)
-(void)userNotificationCenter:(UNUserNotificationCenter *)center willPresentNotification:(UNNotification *)notification withCompletionHandler:(void (^)(UNNotificationPresentationOptions options))completionHandler{
    NSLog(@"User Info : %@",notification.request.content.userInfo);
    // call trackNotificationReceive API to send receive information
[ACPCampaignClassic trackNotificationReceive:notification.request.content.userInfo];
completionHandler(UNAuthorizationOptionSound | UNAuthorizationOptionAlert | UNAuthorizationOptionBadge);
}
```

#### Swift

```swift
ACPCampaignClassic.trackNotificationReceive(trackInfo[String:String])
```

{% endtab %}
{% endtabs %}

### trackNotificationClick

The trackNotificationClick API should be called after a push message has been opened by the user and clickedthrough it to launch the app. Similar to the trackNotificationReceive API, It takes a dictionary as a parameter and the dictionary should contain the message id and delivery id retrieved from the push message which was clickedthrough. On Android, the API takes a map containing the same message id and delivery id received from the push message clickthrough.

{% tabs %}

{% tab title="Android" %}

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
	App.setAppContext(this.getApplicationContext());
	App.setCurrentActivity(this);
    // ...
	// omitted other functionality that may be present in the onResume method
    // ...
    // The broadlog and delivery id can be passed in the intent extras.
    // This is assuming that you extract the broadlog and delivery id from the
	// received push message and are including it in the intent (intent.putExtra())
    // of the displayed notification.
	if (getIntent().getExtras() != null) {
		Map<String,String> trackInfo = new HashMap<>();
		for (String key : getIntent().getExtras().keySet()) {
			Object value = getIntent().getExtras().get(key);
			if(key.equals("broadlogid")){
				trackInfo.put(key, value.toString());
			}else if(key.equals("deliveryid")){
				trackInfo.put(key, value.toString());
			}
		}
		CampaignClassic.trackNotificationClick(trackInfo);
	}
}
```

{% endtab %}

{% tab title="iOS" %}

#### Objective-C

#### Syntax

```objectivec
+ (void) trackNotificationClick: (nonnull NSDictionary<NSString*, NSString*>*) trackInfo;
```

#### Example

```objectivec
// Indicates which action was selected by the user for a given notification.
-(void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler{
    NSLog(@"User Info : %@",response.notification.request.content.userInfo);
[ACPCampaignClassic trackNotificationClick:response.notification.request.content.userInfo];
completionHandler();
}
```

#### Swift

```swift
ACPCampaignClassic.trackNotificationClick(trackInfo[String:String])
```

{% endtab %}
{% endtabs %}