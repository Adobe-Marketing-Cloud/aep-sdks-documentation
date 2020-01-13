#                         Push Notification Implementation and Tracking Troubleshooting
                         
### Setting up Android/iOS app for receiving push notification includes 3 main steps:

  {% tabs %} {% tab title="Android" %}


   * **Configuring app in Google Firebase (Android)**: Go to the Google [Firebase Console](https://console.firebase.google.com/) and sign in using your Google Developer credentials. Add a project and add your app under that project using the application Id that you used in app. Read more [here](https://firebase.google.com/docs/android/setup#console) for setting up.

  * Add generated **“google-service.json”** to project and set up the project and module level gradle files. 
  [Refer](https://firebase.google.com/docs/android/setup#console) for setting up gradle files.
  
{% endtab %}

{% tab title="iOS" %}

  * Register app on Apple developer account and generate server certificate. [Refer](https://developer.apple.com/documentation/usernotifications/setting_up_a_remote_notification_server/establishing_a_certificate-based_connection_to_apns?language=objc) for more details.
{% endtab %} {% endtabs %}

{% tabs %} { % tab title="Android" % }

  * **Verify that Server key is configured in Campaign instance.**

    Ensure that server key is successfully set up in Campaign instance.  
    This can be verified in Campaign instance under following section Campaign -> Administrator -> Channels -> Mobile App (AEP SDK).  
    Launch mobile app and check push channel settings, _it should say Android key set up success_. It should look like:
    
   ![alt text](https://github.com/shivam-tomar-sde/aep-sdks-documentation/blob/push-troubleshooting-document/.gitbook/assets/android_server_key.png "Server key configuration in Android.")

{% endtab %}

{% tabs %} { % tab title="iOS" % }

  * **Verify that Server cerificate is configured in Campaign instance.**
  
      Ensure that server certificate (.pem file) is successfully set up in Campaign instance. This can be verified in Campaign instance under following section Campaign -> Administrator -> Channels -> Mobile App (AEP SDK). Launch mobile app and check push channel settings, it should say Android key set up success. It should look like:
  ![alt text](https://github.com/shivam-tomar-sde/aep-sdks-documentation/blob/push-troubleshooting-document/.gitbook/assets/campaign_ios_cert_configured.png "Configured push certificate in Campaign.")

{% endtab %}

{% endtabs %}

{% tabs %} { % tab title="Android" % }   
  * **Set up Android app for receiving push notifications: Android app should contain following for receiving push notifications:**

    * Create Firebase Messing Service and add it to Android Manifest file. [Refer](https://firebase.google.com/docs/cloud-messaging/android/client).
  
    * Verify that user is opted in for receiving push notification. This can be verified in Griffon. [Refer](https://aep-sdks.gitbook.io/docs/resources/troubleshooting-guides/troubleshooting-push#ensure-user-opt-in-for-push-in-adobe-analytics).
  
    * Generate push token for app using Fire Base Instance Id class. Set push token to AEP SDK by calling Set [Push Identifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard/adobe-campaign-standard-api-reference#set-up-push-messaging). Verify that Push token is successfully synced with Identity service in Griffon. [Refer](https://aep-sdks.gitbook.io/docs/resources/troubleshooting-guides/troubleshooting-push#verify-push-token-sync-with-the-experience-cloud-identity-service).

    * For app to receive push notification it’s push token should be present in Campaign instance mapped with correct Experience cloud id(mid). This can be verified by following 2 steps:
                 
    * Verification in Griffon: Verify that the user id is correctly set. [Refer](https://aep-sdks.gitbook.io/docs/resources/troubleshooting-guides/troubleshooting-push#confirm-that-the-user-id-is-correctly-set).

    * Verification in Campaign Instance: Verify that app’s push token is present in Campaign instance mapped with correct Experience cloud id(mid). This can be verified by logging into Campaign instance and then navigating to following section: Campaign -> Administrator -> Channels -> Mobile App (AEP SDK). Launch your app and check under mobile application subscribers. It should contain list of all Subscribers of app. Verify mid and push token for your app are present there. This can be verified on the page shown in below screenshot. **Experience Cloud ID** and **Registration Token** for the user should be present here.
    
   ![alt text](https://github.com/shivam-tomar-sde/aep-sdks-documentation/blob/push-troubleshooting-document/.gitbook/assets/campaign_app_subscriber_list.png "App subscriber list, verify mid and push token.")
    
   For more information about verifying it, see point 7 of [_**Channel specific application configuration**_](https://helpx.adobe.com/campaign/kb/configuring-app-sdk.html) in Adobe Campaign
{% endtab %}

{ % tab title="iOS" % }   

  * **Set up iOS application to set APNS push token in SDK**   
      Register the app for receiving APNS token on app launch by calling registerForRemoteNotifications, which will in turn    generate the APNS token and return through callback. In callback set the Push identifier by call setPushIdentifier method. Refer [here](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics-mobile-services#set-up-push-messaging) for more details.

{% endtab %}

{% endtabs %}
 
## Troubleshooting Push Notification events tracking in Android and iOS:  
Following three events related to push notifications are tracked: 
  * impression (Notification is delivered)
  * click (User clicked the notification)
  * open (App opened in response to user's click on notification) 
  [Refer](https://helpx.adobe.com/campaign/kb/push-tracking.html) for implementation of tracking push notification events.
  Whether these events are successfully tracked or not can be verified by checking logs on Griffon. In case Griffon is not     available it can be verified using Charles as well.
  
  * **Troubleshooting push notifications tracking events using Griffon:**  
      Open the Griffon session and look for **TYPE** **CollectData**.  
      Pleae see screenshots below:
  
   ![alt text](https://github.com/shivam-tomar-sde/aep-sdks-documentation/blob/push-troubleshooting-document/.gitbook/assets/push_tracking_impression.png "Shows Push notification impression tracking.")
   
   Shows tracking of push notification **impression** event. It is indicated by action 7.
   
   ![alt text](https://github.com/shivam-tomar-sde/aep-sdks-documentation/blob/push-troubleshooting-document/.gitbook/assets/push_tracking_click.png "Shows Push notification click tracking.")
   
   Shows tracking of push notification **click** event. It is indicated by action 2.
   
   ![alt text](https://github.com/shivam-tomar-sde/aep-sdks-documentation/blob/push-troubleshooting-document/.gitbook/assets/push_tracking_open.png "Shows Push notification open tracking.")
   
   Shows tracking of push notification **open** event. It is indicated by action 1.
  
  
  * **Troubleshooting push notifications tracking events using Charles:**
