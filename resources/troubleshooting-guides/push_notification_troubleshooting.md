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

  

