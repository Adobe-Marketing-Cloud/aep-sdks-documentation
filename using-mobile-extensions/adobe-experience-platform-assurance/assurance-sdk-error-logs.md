# Assurance SDK Troubleshooting

## Unable to open the app using the griffon deeplink

This might happen, If deeplink is not properly configured in your application.

**iOS** 

Follow [Apple developer](https://developer.apple.com/documentation/uikit/inter-process_communication/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app) documentation to set custom URL scheme for your application.

**Android**

Follow the [Android documention](https://developer.android.com/training/app-links/deep-linking ) on information about how to setup a deeplink.

## Pincode entry screen doesnot appear

a. This might happen if Griffon extension is not registered with the MobileCore.

### Possible Fix

Make sure that the Assurance Extension is registered with the EventHub.

**Android**

```java
  public class MobileApp extends Application {
   @Override
   public void onCreate() {
      super.onCreate();
      MobileCore.setApplication(this);
      MobileCore.configureWithAppId("yourAppId");
      try {
         Assurance.registerExtension();
         MobileCore.start(null);
      } catch (Exception e) {
         // Log the exception
      }
   }
  }
```

**iOS**

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
     ACPCore.configure(withAppId: "yourAppId")   
     ACPGriffon.registerExtension() // <-- register AEPAssurance with Core
     ACPCore.start(nil)
     // Override point for customization after application launch. 
     return true;
}
```

b. This might also happen if the deeplink URL to open griffon session doesn't contain the query parameter "adb_validation_sessionid" 

#### Sample logs

```latex
iOS
[AdobeExperienceSDK DEBUG <AEPAssurance>]: Not a valid Assurance deeplink, Ignorning start session API call. URL : <deeplink URL>

Android
W/AdobeExperienceSDK: Assurance - Not a valid Assurance deeplink, Ignorning start session API call. URL :  <deeplink URL>
```

### Possible Fix

Make sure you scan or copy the correct Assurance deeplink URL.

## Connection Error

After you successfully scan the assurance deeplink and entered the 4 digit code. And then if you see the following error.

<img src="../../.gitbook/assets/assurance_connection_error.png" alt="Assurance connection error" style="zoom:50%;" />

### Possible Fix

1. Make sure the 4 digit pin code is entered correctly from the session associated with the deeplink

   

   <img src="../../.gitbook/assets/assurance_pincode.png" alt="Assurance connection error" style="zoom:30%;" />

2. Check if the device has a proper internet connection.

## Invalid Launch & SDK Configuration

<img src="../../.gitbook/assets/assurance_invalid_configuration_error.png" alt="Adobe Target Extension Configuration" style="zoom:50%;" />

#### Sample logs

```
iOS
[AdobeExperienceSDK ERROR <AEPAssurance>]: Assurance connection closed. Reason: Invalid Launch & SDK Configuration, Description: The Experience Cloud Org identifier is unavailable from SDK configuration. Please ensure the Launch mobile property is properly configured.

Android
W/AdobeExperienceSDK: Assurance - Assurance connection closed. Reason: Invalid Launch & SDK Configuration, Description: The Experience Cloud Org identifier is unavailable from SDK configuration. Please ensure the Launch mobile property is properly configured.
```

### Possible Fix

* Verify if MobileCore is [configured properly](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).
* Make sure you have published the configuration with [Experience Platform Launch](https://launch.adobe.com/). See [Publish the configuration](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property#publish-the-configuration).
* Confirm if the device has an internet connection to download the remote configuration.



## Unauthorized access

<img src="../../.gitbook/assets/assurance_unauthorized_access_error.png" alt="Adobe Target Extension Configuration" style="zoom:50%;" />

#### Sample logs

```
iOS
[AdobeExperienceSDK ERROR <AEPAssurance>]: Assurance connection closed. Reason: Unauthorized Access, Description: AEP Assurance sessions and Launch mobile properties must be created in the same organization.

Android
W/AdobeExperienceSDK: Assurance - Assurance connection closed. Reason: Unauthorized Access, Description: AEP Assurance sessions and Launch mobile properties must be created in the same organization.
```

### Possible fix

- Make sure that the Organization in which the mobile property is setup in launch is same as the Organization of the griffon session that you have created.

  

## Timeout

This log message is not a problem by itself. It is expected if the app was not launched with a Assurance deep link. You may ignore this error if Assuracne SDK works as expected.

Sample log messages:

**iOS**

```text
[AdobeExperienceSDK DEBUG <AEPAssurance>]: Timeout - Griffon didnot receive deeplink to start griffon session. Shutting down griffon extension
```

**Android**

```
D/AdobeExperienceSDK: Assurance - Timeout - Assurance did not receive deeplink to start Assurance session within 5 seconds. Shutting down Assurance extension
```



## Failed to show fullscreen takeover

* This log message is not a problem and will appear with typical usage in Android. You may ignore this error if Assurance SDK works as expected.

Sample log:

```text
W/AdobeExperienceSDK: Assurance - Failed to show fullscreen takeover, could not get fullScreenTakeover object.
```

