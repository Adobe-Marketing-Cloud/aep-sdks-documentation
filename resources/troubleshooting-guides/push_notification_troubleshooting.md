#                         Push Notification Implementation and Tracking Troubleshooting
                         
### Setting up Android app for receiving push notification includes 3 main steps:

**1. Configuring app in Google Firebase (Android)**
   * Go to the Google [Firebase Console](https://console.firebase.google.com/) and sign in using your Google Developer credentials. Add a project and add your app under that project using the application Id that you used in app. Read more [here](https://firebase.google.com/docs/android/setup#console) for setting up.

  * Add generated **“google-service.json”** to project and set up the project and module level gradle files. Please 
  [refer](https://firebase.google.com/docs/android/setup#console) for setting up gradle files.

**2. Verify Server key is configured in Campaign instance.**

    Ensure that server key is successfully set up in Campaign instance.  
    This can be verified in Campaign instance under following section Campaign -> Administrator -> Channels -> Mobile App (AEP SDK).  
    Launch mobile app and check push channel settings, it should say Android key set up success. It should look like:
    
   ![alt text](https://github.com/shivam-tomar-sde/aep-sdks-documentation/blob/push-troubleshooting-document/.gitbook/assets/android_server_key.png "Server key configuration in Android.")
   
**3). Set up Android app for receiving push notifications: Android app should contain following for receiving push. 
notifications:**

  * Create Firebase Messing Service and add it to Android Manifest file. [Refer](https://firebase.google.com/docs/cloud-messaging/android/client).
  
  * Verify that user is opted in for receiving push notification. This can be verified in Griffon. [Refer](https://aep-sdks.gitbook.io/docs/resources/troubleshooting-guides/troubleshooting-push#ensure-user-opt-in-for-push-in-adobe-analytics).
  
  * Generate push token for app using Fire Base Instance Id class. Set push token to AEP SDK by calling Set [Push Identifier](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard/adobe-campaign-standard-api-reference#set-up-push-messaging). Verify that Push token is successfully synced with Identity service in Griffon. [Refer](https://aep-sdks.gitbook.io/docs/resources/troubleshooting-guides/troubleshooting-push#verify-push-token-sync-with-the-experience-cloud-identity-service).

  * For app to receive push notification it’s push token should be present in Campaign instance mapped with correct Experience cloud id(mid). This can be verified by following 2 steps:
                 
    * Verification in Griffon: Verify that the user id is correctly set. [Refer](https://aep-sdks.gitbook.io/docs/resources/troubleshooting-guides/troubleshooting-push#confirm-that-the-user-id-is-correctly-set).

    * Verification in Campaign Instance: Verify that app’s push token is present in Campaign instance mapped with correct Experience cloud id(mid). This can be verified by logging into Campaign instance and then navigating to following section: Campaign -> Administrator -> Channels -> Mobile App (AEP SDK). Launch your app and check under mobile application subscribers. It should contain list of all Subscribers of app. Verify mid and push token for your app are present there. This can be verified on the page shown in below screenshot.


  

