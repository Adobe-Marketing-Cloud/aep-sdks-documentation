# Campaign Classic API reference

## extensionVersion

The `extensionVersion` API returns the version of the Campaign Classic extension that is registered with the Mobile Core extension.

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
public static String extensionVersion();
```

**Example**

```java
String campaignClassicExtensionVersion = CampaignClassic.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

Adobe Campaign Classic has not yet been released as an AEP 3.x Swift extension. Please reach out to your Adobe customer account manager if you have any questions or would like to express interest in the AEP 3.x Campaign Classic extension.

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
### Swift

**Syntax**

```swift
func extensionVersion() -> String
```

**Example**

```swift
let campaignClassicExtensionVersion  = ACPCampaignClassic.extensionVersion()
```

### Objective-C

**Syntax**

```objc
+(NSString) extensionVersion;
```

**Example**

```objectivec
NSString *campaignClassicExtensionVersion = [ACPCampaignClassic extensionVersion];
```
{% endtab %}
{% endtabs %}

## registerDevice

The `registerDevice` API lets you register a user device with Campaign Classic.

{% tabs %}
{% tab title="Android" %}
{% hint style="info" %}
To prepare your app to handle push notifications, see the tutorial on [setting up a Firebase Cloud Messaging client app on Android](https://firebase.google.com/docs/cloud-messaging/android/client). After you receive the Firebase Cloud Messaging (FCM) SDK registration token, send this token and the device information to Campaign Classic by using the `registerDevice` API.
{% endhint %}

The `registerDevice` API registers a device with your Campaign Classic registration server. It takes the FCM registration token as a parameter with a user key that identifies a user, such as an email address or a login name. You can also provide a map of the custom key-value pairs that you want to associate with the registration. A boolean value is returned in the callback, which signals whether the registration was successful.

### Java

**Syntax**

```java
public static void registerDevice(final String token, final String userKey, final Map<String, Object> additionalParams, final AdobeCallback<Boolean> callback)
```

**Example**

```java
@Override
public void onNewToken(String token) {
    Log.d("TestApp", "Refreshed token: " + token);

  // If you want to send messages to this application instance or
  // manage this app's subscriptions on the server side, send the
  // Instance ID token to your app server.
  if (token != null) {
    Log.d("TestApp", "FCM SDK registration token received : " + token);
    // Create a map of additional parameters
    Map<String, Object> additionalParams = new HashMap<String, Object>();
    additionalParams.put("name", "John");
    additionalParams.put("serial", 12345);
    additionalParams.put("premium", true);
    // Send the registration info
    CampaignClassic.registerDevice(token, "john@example.com", additionalParams,new AdobeCallback<Boolean>() {
      @Override
      public void call(final Boolean status) {
        Log.d("TestApp", "Registration Status: " + status);
      }
    });
  }
}
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

Adobe Campaign Classic has not yet been released as an AEP 3.x Swift extension. Please reach out to your Adobe customer account manager if you have any questions or would like to express interest in the AEP 3.x Campaign Classic extension.

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
{% hint style="info" %}
To get your app ready to handle push notifications, see the tutorial on [configuring remote notification support](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1). After you receive the Apple Push Notification service (APNs) token, send this token and the device information to Campaign Classic using the `registerDevice` API.
{% endhint %}

The `registerDevice` API registers a device with your Campaign Classic registration server. It takes the APNS token as a parameter with a user key that identifies a user, such as an email address or a login name. You can also provide a map of the custom key-value pairs that you want to associate with the registration. A boolean value is returned in the callback, which signals whether the registration was successful.

### Swift

**Syntax**

```swift
func registerDevice(_ token: Data, userKey: String?, additionalParams: [String: Any]?, callback: ((Bool) -> Void)?)
```

**Example**

```swift
func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
  let params: [String: Any] = [
    "name": "John",
    "serial": 12345,
    "premium": true
  ]
  ACPCampaignClassic.registerDevice(deviceToken, userKey: "john@example.com", additionalParams: params) { 
    result in
    print("Registration status: \(result)")
  }
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) registerDevice: (nonnull NSData*) token userKey: (nullable NSString*) userKey additionalParams: (nullable NSDictionary*) additionalParams callback: (nullable void (^) (BOOL success)) callback;
```

**Example**

```objectivec
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  // Set the deviceToken that the APNS has assigned to the device
  NSMutableDictionary *params = [[NSMutableDictionary alloc] initWithObjectsAndKeys:          @"John", @"name", nil];
  [params setObject: [NSNumber numberWithInt:12345] forKey: @"serial"];
  [params setObject: [NSNumber numberWithBool:YES]  forKey: @"premium"];

[ACPCampaignClassic registerDevice:deviceToken userKey:@"john@example.com" additionalParams:params callback:^(BOOL success) {
    NSLog(@"Registration Status: %d", success);
}
```
{% endtab %}
{% endtabs %}

## trackNotificationClick

The `trackNotificationClick` API sends the clicked push notification's tracking information to the configured Adobe Campaign Classic server. This API can be used to send tracking information when the notification is clicked, which may result in the application being opened. 

{% tabs %}
{% tab title="Android" %}

### Java

{% hint style="info" %}
If `trackInfo` is null, or does not contain the necessary tracking identifiers, `messageId` (`_mId`) and `deliveryId` (`_dId`), a track request is **not** sent.
{% endhint %}

**Syntax**

```java
public static void trackNotificationClick(final Map<String, String> trackInfo)
```

**Example**

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

{% tab title="iOS (AEP 3.x)" %}

Adobe Campaign Classic has not yet been released as an AEP 3.x Swift extension. Please reach out to your Adobe customer account manager if you have any questions or would like to express interest in the AEP 3.x Campaign Classic extension.

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}
{% hint style="info" %}
You can pass the `launchOptions` that were received upon opening the application or `userInfo`, which contains the received push payload in `trackInfo`. If `trackInfo` is null or does not contain the necessary tracking identifiers, `broadlogId` (`_mId`) and `deliveryId` (`_dId`), a track request is **not** sent.
{% endhint %}

### Swift

**Syntax**

```swift
func trackNotificationClick(_ trackInfo: [String: String])
```

**Example**

```swift
func userNotificationCenter(_ center: UNUserNotificationCenter, didReceive response: UNNotificationResponse, withCompletionHandler completionHandler: @escaping () -> Void) {
  guard let userInfo = response.notification.request.content.userInfo as? [String: String] else {
    return;
  }
  ACPCampaignClassic.trackNotificationClick(userInfo);
  completionHandler();
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) trackNotificationClick: (nonnull NSDictionary<NSString*, NSString*>*) trackInfo;
```

**Example**

```objectivec
-(void)userNotificationCenter:(UNUserNotificationCenter *)center didReceiveNotificationResponse:(UNNotificationResponse *)response withCompletionHandler:(void(^)(void))completionHandler
{
  NSLog(@"User Info : %@",response.notification.request.content.userInfo);
  // Track action selected by the user for a given notification
  [ACPCampaignClassic trackNotificationClick:response.notification.request.content.userInfo];
  completionHandler();
}
```

{% endtab %}
{% endtabs %}

## trackNotificationReceive

The `trackNotificationReceive` API sends the received push notification's tracking information to the configured Adobe Campaign Classic server.

{% tabs %}
{% tab title="Android" %}

### Java

{% hint style="info" %}

If `trackInfo` is null or does not contain the necessary tracking identifiers, `messageId` (`_mId`) and `deliveryId` (`_dId`), a track request is **not** sent.

{% endhint %}

**Syntax**

```java
public static void trackNotificationReceive(final Map<String, String> trackInfo)
```

**Example**

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

{% tab title="iOS (AEP 3.x)" %}

Adobe Campaign Classic has not yet been released as an AEP 3.x Swift extension. Please reach out to your Adobe customer account manager if you have any questions or would like to express interest in the AEP 3.x Campaign Classic extension.

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

{% hint style="info" %}
You can pass the `launchOptions` that were received upon opening the application or `userInfo` , which contains the received push payload in `trackInfo`. If `trackInfo` is null or does not contain the necessary tracking identifiers, `broadlogId` (`_mId`) and `deliveryId` (`_dId`), a track request is **not** sent.
{% endhint %}

### Swift

**Syntax**

```swift
func trackNotificationReceive(_ trackInfo: [String: String])
```

**Example**

```swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
    
  guard let aps = userInfo["aps"] as? [String: Any] else {
    completionHandler(.failed)
    return
  }
  if aps["content-available"] as? Int == 1 {
    // Track silent push notification receive
    ACPCampaignClassic.trackNotificationReceive(userInfo)
    completionHandler(.noData)
  }
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) trackNotificationReceive: (nonnull NSDictionary<NSString*, NSString*>*) trackInfo;
```

**Example**

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

{% endtab %}
{% endtabs %}

