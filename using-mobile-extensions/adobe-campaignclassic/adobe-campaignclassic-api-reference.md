# Campaign Classic API reference

## Version of the Campaign Classic extension

The `extensionVersion()` API returns the version of the Campaign Classic extension that is registered with the Mobile Core extension.

To get the version of the Campaign Classic extension, use the following code sample:

{% tabs %}
{% tab title="iOS" %}
**Objective C**

```objectivec
NSString *campaignClassicExtensionVersion = [ACPCampaignClassic extensionVersion];
```

**Swift**

```swift
let campaignClassicExtensionVersion  = ACPCampaignClassic.extensionVersion()
```
{% endtab %}
{% endtabs %}

## registerDevice API

### Registering a user's device with Campaign Classic

{% tabs %}
{% tab title="iOS" %}
To get your app ready to handle push notifications, follow [Apple's instructions](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1). After you receive the APNS token, send this token and the device information to Campaign Classic using the `registerDevice` API.

### registerDevice

The `registerDevice` API registers a device with your Campaign Classic registration server. It takes the APNS token as a parameter with a user key that identifies a user, such as an email address or a login name. You can also provide a map of the custom key-value pairs that you want to associate with the registration. A boolean value is returned in the callback, which signals whether the registration was successful.

#### Objective-C

#### Syntax

```objectivec
+ (void) registerDevice: (nonnull NSData*) token userKey: (nullable NSString*) userKey additionalParams: (nullable NSDictionary*) additionalParams callback: (nullable void (^) (BOOL success)) callback;
```

#### Example

```objectivec
- (void) application:(UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)deviceToken {
  // Set the deviceToken that the APNS has assigned to the device
  NSMutableDictionary *params = [[NSMutableDictionary alloc] initWithObjectsAndKeys:          @"John", @"name", nil];
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

Adobe Campaign Classic has the following APIs to track push message receive and opening:

{% tabs %}
{% tab title="iOS" %}
### trackNotificationReceive

The `trackNotificationReceive` API sends the received push notification's tracking information to the configured Adobe Campaign Classic server. You might pass the `launchOptions` that were received before opening the application or `userInfo` , which contains the received push payload in `trackInfo`. If `trackInfo` is null or does not contain the necessary tracking identifiers, `broadlogId` \(`_mId`\) and `deliveryId` \(`_dId`\), no track request is sent.

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
{% tab title="iOS" %}
### trackNotificationClick

The `trackNotificationClick` API sends the clicked push notification's tracking information to the configured Adobe Campaign Classic server. This API might be used to send tracking information when the notification is clicked, which may result in the application being opened. You might pass the `launchOptions` that was received before opening the application or `userInfo`, which contains the received push payload in `trackInfo`. If `trackInfo` is null or does not contain the necessary tracking identifiers, `broadlogId` \(`_mId`\) and `deliveryId` \(`_dId`\), no track request is sent.

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
    [ACPCampaignClassic             trackNotificationClick:response.notification.request.content.userInfo];
completionHandler();
}
```

#### Swift

```swift
ACPCampaignClassic.trackNotificationClick(trackInfo[String:String])
```
{% endtab %}
{% endtabs %}

