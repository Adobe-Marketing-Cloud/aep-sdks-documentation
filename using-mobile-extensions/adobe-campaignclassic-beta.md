# Adobe Campaign Classic \(Beta\)

{% hint style="warning" %}
This extension is considered beta functionality and is available only in Launch's [Integration](http://launch-integration.adobe.com) environment.
{% endhint %}

## Configure Campaign Classic Extension in Launch

1. In Launch's Integration environment, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Campaign Classic** extension and click **Install**.
3. Provide extension settings \(see screen capture below\)
4. Click **Save**.
5. Follow the publishing process to update SDK configuration

### Configure Campaign Classic Extension

![ACC-configure-extension](../.gitbook/assets/ACC-configure-extension.png)

{% hint style="info" %}
Trying to find your ACC registration or tracking endpoint URLs? Contact your beta program manager.
{% endhint %}

#### Registration Endpoints

Provide registration endpoint URL\(s\) for your Adobe Campaign Classic instances. You may specify up to three unique endpoints for your development, staging, and production environments. 

#### Tracking Endpoints

Provide tracking endpoint URL\(s\) for your Adobe Campaign Classic instances. Like the registration URL's, you may specify up to three unique endpoints for your development, staging, and production environments. 

#### Integration Key (iOS)

Specify up to three unique iOS integration keys for your development, staging, and production environments. iOS integration keys are generated after creating a service containing iOS applications using the Adobe Campaign Classic [client console](https://docs.campaign.adobe.com/doc/AC/en/INS_Installation_steps_for_Windows__Installing_the_client_console.html). For more information on where to find the integration key, please see [Configuring the mobile application in Adobe Campaign](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Configuring_the_mobile_application_in_Adobe_Campaign).

#### Integration Key (Android)

Specify up to three unique Android integration keys for your development, staging, and production environments. Similar to iOS, Android integration keys are generated after creating a service containing Android applications using the Adobe Campaign Classic [client console](https://docs.campaign.adobe.com/doc/AC/en/INS_Installation_steps_for_Windows__Installing_the_client_console.html). For more information on where to find the integration key, please see [Configuring the mobile application in Adobe Campaign](https://docs.campaign.adobe.com/doc/AC/en/DLV_Sending_push_notifications_Setting_up_mobile_app_channel.html#Configuring_the_mobile_application_in_Adobe_Campaign).

#### Request Timeout

Time in seconds to wait for a response from the registration endpoint before timing out.

## Add Campaign Classic to your app

{% hint style="warning" %}
This beta extension is currently available only for the iOS development.
{% endhint %}

{% tabs %}
{% tab title="iOS" %}
{% hint style="warning" %}
This **beta** Campaign Classic extension requires the [Mobile Core](mobile-core/) **beta** extension. If you are using other versions of the Mobile Core library, use the beta version instead, as the instructions below indicate.
{% endhint %}

Add the Campaign Classic and [Mobile Core](mobile-core/) beta libraries to your project. You'll need to add the following pods to your `Podfile`:

```text
pod 'ACPCampaignClassicBeta', '1.0.0beta'
pod 'ACPCoreBeta', '1.0.2beta'
```

or you may manually include the [Mobile Core](https://github.com/Adobe-Marketing-Cloud/acp-sdks/releases/tag/v1.0.2beta-ACPCore) and [Campaign Classic](update to campaign classic beta location) beta extensions found in Github.

In Xcode, import the Mobile Core beta and Campaign Classic beta extensions:

#### Objective-C

```objectivec
#import <ACPCore_iOS/ACPCore_iOS.h>
#import <ACPCampaignClassic_iOS/ACPCampaignClassic_iOS.h>
#import <ACPLifecycle_iOS/ACPLifecycle_iOS.h>
```

#### Swift

```swift
import ACPCore_iOS
import ACPCampaign_iOS
import ACPLifecycle_iOS
```
{% endtab %}
{% endtabs %}

### Register Campaign Classic with Mobile Core

{% tabs %}
{% tab title="iOS" %}
In your app's`application:didFinishLaunchingWithOptions:` method, register the Campaign Classic extension:

#### Objective-C

```objectivec
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCampaignClassic registerExtension];
    [ACPLifecycle registerExtension];
  // Override point for customization after application launch.
  return YES;
}
```

#### Swift

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
   ACPCampaignClassic.registerExtension();
   ACPLifecycle.registerExtension();
  // Override point for customization after application launch.
  return true;
}
```
{% endtab %}
{% endtabs %}

### Registering a user's device with Campaign Classic

Follow [Apple's instructions](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1) to get your app ready to handle push notifications. Once you receive the APNS token, you will need to send the device information to Campaign Classic using the registerDevice API.

{% tabs %}
{% tab title="iOS" %}

### registerDevice

The registerDevice API will register a device with your Adobe Campaign Classic registration server. It takes the APNS token as a parameter along with a user key that identifies the user such as an email address or login name. It can also be given a dictionary of custom key value pairs that you want to associate with the registration. Lastly, a boolean value is returned in the callback with signals whether the registration was sucessful.

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

### Tracking for push message receive and clickthrough

Adobe Campaign Classic has two additional API used for tracking push messages received and push messages clicked. The two API are:

{% tabs %}
{% tab title="iOS" %}

### trackNotificationReceive

The trackNotificationReceive API should be called after a push message has been received in the app. It takes a dictionary as a parameter and the dictionary should contain the message id and delivery id retrieved from the received  push message.

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

{% tabs %}
{% tab title="iOS" %}

### trackNotificationClick

The trackNotificationClick API should be called after a push message has been opened by the user and clickedthrough it to launch the app. Similar to the trackNotificationReceive API, It takes a dictionary as a parameter and the dictionary should contain the message id and delivery id retrieved from the  push message which was clickedthrough.

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