# AEP Core setup

This tutorial illustrates how to install AEPCore Swfit SDK and use it in a sample application.

## Prerequisites for this tutorial

* [Access to Adobe Experience Launch dashboard](https://launch.adobe.com/)
* Xcode 12
* [Cocoapods](https://cocoapods.org/)

### Configure the Launch Mobile property

To finish the tutorial, you can either use a existing Mobile Property or create a new one. Follow the below steps if you need to create a new Mobile property in Launch UI:

1. Follow these steps to [Set up a mobile property](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property) in Adobe Experience Platform Launch.
2. Go to the Publishing Flow menu, select the development library you created and click `Add All Changed Resources`.
3. Click `Save & Build for Development` to publish the changes in the **Development** environment.

### Download the sample app

Download the [Swift base sample app](https://github.com/adobe/aepsdk-sample-app-ios/releases/download/1.0.0-beta.1/AEPSample_Base.zip) , upzip it and you will get a new folder `AEPSample_Base` containing the sample source code.

### Install the AEPCore SDK

1. Add the following code to the `Podfile`

```text
  pod 'AEPServices', :git => 'https://github.com/adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPCore', :git => 'https://github.com/adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPLifecycle', :git => 'https://github.com/adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPIdentity', :git => 'https://github.com/adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPSignal', :git => 'https://github.com/adobe/aepsdk-core-ios.git', :branch => 'main'
  pod 'AEPRulesEngine', :git => 'https://github.com/adobe/aepsdk-rulesengine-ios.git', :branch => 'main'
```

1. Run `pod install` in the `AEPSample_Base` folder, it should download all the dependencies and add them to the project.
2. Open the project from \`AEPSampleApp.xcworkspace

### Init SDK

1. Open `AppDelegate.swift` and add the following `import` statements.

```swift
import AEPCore
import AEPLifecycle
import AEPIdentity
import AEPSignal
```

1. In the method `func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool` , register `Lifecycle` , `Identity` and `Signal` extensions and start the SDK. Also call the `MobileCore.configureWith(appId:)` to configure the app id. 

```swift
// enable the trace log, we need it in the future steps
MobileCore.setLogLevel(.trace)
// init SDK
MobileCore.registerExtensions([Lifecycle.self, Identity.self, Signal.self], {
    // use the App id assigned to this application via Adobe Launch
    MobileCore.configureWith(appId: self.LAUNCH_ENVIRONMENT_FILE_ID)
})
```

1. In [Adobe Experience Platform Launch](https://experience.adobe.com/launch), go to the **Environments** tab in the mobile property created in the previous step \(Configure the Adobe Experience Platform Mobile SDK\) and click on the Development![img](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Lf1Mc1caFdNCK_mBwhe%2F-Lf1N06T8hdv0-r5jPPN%2F-Lf1N3-ofPO9fLFT1edw%2Fscreen-shot-2018-10-18-at-11.22.17-am.png?generation=1558039279051937&alt=media)icon. Find the Environment File ID at the top and copy it.

   Set the `LAUNCH_ENVIRONMENT_FILE_ID` to the copied Environment File ID in the `AppDelegate` \(iOS\) class.

2. Now run the app, you should be able to see the SDK logs being printed in the console.

### Enable Lifecycle

1. Open `AppDelegate.swift` and add the code to get `applicationState` and trigger `lifecycleStart`

   ```swift
    let appState = application.applicationState;
    // init SDK
    MobileCore.registerExtensions([Lifecycle.self, Identity.self, Signal.self], {
        // use the App id assigned to this application via Adobe Launch
        MobileCore.configureWith(appId: self.LAUNCH_ENVIRONMENT_FILE_ID)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: nil)
        }
    })
   ```

2. Open `SceneDelegate.swift` and import `AEPCore`

   ```swift
   import AEPCore
   ```

3. In the `sceneWillEnterForeground` method, add:

   ```swift
   MobileCore.lifecycleStart(additionalContextData: nil)
   ```

4. In the `sceneDidEnterBackground` method, add:

   ```swift
   MobileCore.lifecyclePause()
   ```

5. Now run the app. In the log, search for `LaunchEvent`, you should be able to see the log for the Lifecycle event which contains the `LaunchEvent` and other lifecycle data.

### Sync Identifier

1. Open `CoreViewController.swift`
2. Search for `Text("Sync Identifiers")`, and in the `action` block above it, use the `Identity.syncIdentifiers` API to sync the identifiers with the Identity service.

   ```swift
   Identity.syncIdentifiers(identifiers: ["customId":"1234567"], authenticationState: .authenticated)
   ```

3. Now run the app, find the `Sync Identifiers` button in the `Core` tab and click on it. You should see in the log that a network request is sent to the `dpm.demdex.net` server containing the ids in the code.

### Next steps

To know more about Swift Core SDK check out the [AEPCore Documentation](https://github.com/adobe/aepsdk-core-ios/tree/dev/Documentation).

Get the [sample apps](https://github.com/adobe/aepsdk-sample-app-ios) to learn how to use AEPCore SDK in a Swift app or an Obj-c app.

