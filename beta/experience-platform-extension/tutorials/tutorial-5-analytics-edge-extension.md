# Using Analytics edge extension 

{% hint style="warning" %}
The Adobe Experience Platform Edge mobile extension is currently in BETA. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more and get access to the materials for this tutorial.
{% endhint %}

## Prerequisites for this tutorial

* Access to Adobe Experience Platform
* Minimal Swift / Android development knowledge 
* Knowledge about the AEP Edge extension
* Completion of [Assignment 1 - AEP Edge extension setup and XDM usage](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/tutorials/tutorial-1-edge-extension-setup) (required to have a mobile property in Launch with Edge configuration setup).

### Enable Analytics in Edge configuration

In Adobe Experience Platform Launch, navigate to your mobile property and select Edge Configurations from the left panel, then select the configuration created in Assignment 1

* Select development environment, enable `Adobe Analytics` and add a development report suite. If you don't have one, create a new report suite for this exercise using the Mobile template.

   ![](../../../.gitbook/assets/edge_analytics_config.png)


### Download the sample application

{% tabs %}

{% tab title="iOS" %}

#### Swift

Download the iOS Swift Sample application from [https://github.com/adobe/aepsdk-sample-app-ios/tree/beta-assignment-5](https://github.com/adobe/aepsdk-sample-app-ios/archive/beta-assignment-5.zip).

To get started, follow the steps described in [AEP SDK Sample App Swift - Installation](https://github.com/adobe/aepsdk-sample-app-ios/tree/beta-assignment-5#installation).
{% endtab %}
{% endtabs %}

### Set up the required fields

In [Adobe Experience Platform Launch](https://experience.adobe.com/launch), go to the **Environments** tab in the mobile property created in Assignment 1 and click on the Development![img](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Lf1Mc1caFdNCK_mBwhe%2F-Lf1N06T8hdv0-r5jPPN%2F-Lf1N3-ofPO9fLFT1edw%2Fscreen-shot-2018-10-18-at-11.22.17-am.png?generation=1558039279051937&alt=media)icon. Find the Environment File ID at the top and copy it.

Set the `LAUNCH_ENVIRONMENT_FILE_ID` to the copied Environment File ID in the `AppDelegate` \(iOS\) file.

### Install the AnalyticsEdge Extension

{% hint style="info" %}
Analytics Edge Android extension is currently under development and will be available soon.
{% endhint %}

1. Add the following code to the `aepsdk-sample-app-ios/Swift/Podfile`

```text
  pod 'AEPAnalyticsEdge', :git => 'https://github.com/adobe/aepsdk-analyticsedge-ios', :branch => 'main'
```

2. Run `pod install` in the `aepsdk-sample-app-ios/Swift` folder, it should download all the dependencies and add them to the project.
3. Open the project from `aepsdk-sample-app-ios/Swift/AEPSampleApp.xcworkspace`

### Init Extension

1. Open `AppDelegate.swift` and add the following `import` statements.

```swift
import AEPAnalyticsEdge
```

1. In the method `func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool` , register `Analytics` extension before starting the SDK. Also call the `MobileCore.configureWith(appId:)` to configure the app id. 

```swift
// enable the trace log, we need it in the future steps
MobileCore.setLogLevel(.trace)
// init SDK
MobileCore.registerExtensions([Lifecycle.self, Identity.self, Signal.self, Edge.self, Analytics.self], {
    // use the App id assigned to this application via Adobe Launch
    MobileCore.configureWith(appId: self.LAUNCH_ENVIRONMENT_FILE_ID)
})
```

2. Now run the app, find the `Track Action` or `Track State` button in the `Core` tab and click on it. You should see in the logs that a corresponding edge request is sent containing the track data. 

3. You should see the reports get populated in the configured report suite. 

Here is a sample real-time Analytics report which captures actions and page views from the sample application. 

  ![](../../../.gitbook/assets/edge_analytics_report.png)

### Next steps

Use this extension to support your existing analytics workflows.