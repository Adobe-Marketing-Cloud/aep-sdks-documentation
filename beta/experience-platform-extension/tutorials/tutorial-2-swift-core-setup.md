# Tutorial 2 - Swift Core setup

This tutorial illustrates how you may send XDM commerce events to Adobe Experience Platform via Experience Edge using the AEP Edge extension in a sample application, provided to you in iOS \(Swift\) and Android.

The demo mobile application has multiple tabs. For this exercise, the `Edge` and `Assurance` tabs will be used, demonstrating XDM commerce events in a mobile application.

## Prerequisites for this tutorial

- Access to Adobe Experience Launch dashboard
- Xcode 12
- Cocoapod

### Configure the Launch Mobile property

To finish the tutorial, you can either use a existing Mobile Property and create a new one. Follow the below steps if you need to create a new Mobile property in Launch UI:

1. First, follow these steps to [Set up a mobile property](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property) in Adobe Experience Platform Launch.

2. Go to the Publishing Flow menu, select the development library you created and click `Add All Changed Resources`. 
3. Click `Save & Build for Development` to publish the changes in the **Development** environment.

### Download the sample app

Clone or download the iOS Swift Sample application from https://github.com/adobe/aepsdk-sample-app-ios.

To get started, follow the steps described in [AEP SDK Sample App Swift - Installation](https://github.com/adobe/aepsdk-sample-app-ios#installation).

### Install the AEPCore SDK

Add the following code to the `Podfile`

```

  pod 'AEPServices', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPCore', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPLifecycle', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPIdentity', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPSignal', :git => 'git@github.com:adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPRulesEngine', :git => 'git@github.com:adobe/aepsdk-rulesengine-ios.git', :branch => 'main'
```

Run `pod install`, now it should download all the dependencies and add them to the project.

Open the project from `AEPSampleApp.xcworkspace`



### Init SDK

1. Open the AppDelegate.swift, add the following import statements.

```
import AEPCore
import AEPLifecycle
import AEPIdentity
import AEPSignal
```

2. In the method ` func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool` , register `Lifecycle` , `Identity` and `Signal` extensions and start the SDK. Also call the `MobileCore.configureWith(appId:)` to configure the app id. 

```

        MobileCore.setLogLevel(level: .trace)
			  MobileCore.registerExtensions([Lifecycle.self, Identity.self, Signal.self], {

            // Use the App id assigned to this application via Adobe Launch
            MobileCore.configureWith(appId: self.LAUNCH_ENVIRONMENT_FILE_ID)
        })
```

3. In [Adobe Experience Platform Launch](https://experience.adobe.com/launch), go to the **Environments** tab in the mobile property created in the previous step (Configure the Adobe Experience Platform Mobile SDK) and click on the Development![img](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Lf1Mc1caFdNCK_mBwhe%2F-Lf1N06T8hdv0-r5jPPN%2F-Lf1N3-ofPO9fLFT1edw%2Fscreen-shot-2018-10-18-at-11.22.17-am.png?generation=1558039279051937&alt=media)icon. Find the Environment File ID at the top and copy it.

   Set the  `LAUNCH_ENVIRONMENT_FILE_ID` to the copied Environment File ID in the `AppDelegate` (iOS) class.

4. Now run the app, you should be able to see the SDK logs being printed in the console.



### Enable Lifecycle

1. Open the file `SceneDelegate.swift`. 

2. In the `sceneWillEnterForeground` method, add:

   ```
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

3. In the `sceneDidEnterBackground` method, add:

   ```
   MobileCore.lifecyclePause()
   ```

4. Now run the app, since we don't have a Analytics extension yet, you won't be see any request going out, but in the log, you can find Lifecycle event which contains the `LaunchEvent` and other lifecycle data.



### Sync Identifier

1. Open the file `CoreViewController.swift`

2. Search for `Text("Sync Identifiers")`, and in the `action` block above it,  use the `Identity.syncIdentifiers` API to sync the identifiers with the Identity service.

   ```
   Identity.syncIdentifiers(identifiers: ["idType1":"1234567"], authenticationState: .authenticated)
   ```

3. Now run the app, find the `Sync Identifiers` button in the `Core` tab and click on it. You should see in the log that a network request is sent to `dpm.demdex.net` server containing the ids in the code.



### Next steps

If you would like to explore more you the Core, please go to https://github.com/adobe/aepsdk-sample-app-ios and download the full sample, you can learn how to make various SDK calls. If you want to learn more you can check out all the documention we have in https://github.com/adobe/aepsdk-core-ios/tree/dev/Documentation.

