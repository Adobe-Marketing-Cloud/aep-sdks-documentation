---
title: Implement the Launch Embed Code
description: Learn how to get your Launch property's embed codes and implement them in your website. This lesson is part of the Implementing the Experience Cloud in Websites with Launch tutorial.
seo-description:
seo-title: Implement the Launch Embed Code
solution: Experience Cloud
---

# Install the Mobile SDK

In this lesson, you will implement the Mobile SDK with the extensions and settings corresponding to your Launch property's Development environment. Along the way, you will learn about two main concepts of Launch&mdash;Environments and Embed Codes.

## Learning Objectives

At the end of this lesson, you will be able to:

* Obtain the installation instructions for your mobile Launch property
* Understand the difference between a Development, Staging, and Production environment
* Create and edit the Podfile
* Import the Mobile SDK into your AppDelegate file
* Verify that the SDK has been implemented successfully

## Get the Installation Instructions

The Installation Instructions for mobile Launch properties is a collection of code snippets that you either run in your Terminal or add to specific locations in your mobile app.

Click on the `Environments` tab in the top navigation to go to the environments page. Note that Development, Staging, and Production environments have been pre-created for you.

![Click Environments in the top nav](images/mobile-launch-environments.png)

Development, Staging, and Production environments correspond to the typical environments in the code development and release process. Code is first written by a developer in a Development environment. When they have completed their work, they send it to a Staging environment for QA and other teams to review. Once the QA and other teams are satisfied, the code is then published to the Production environment, which is the public-facing environment  which your visitors experience when they download your app.

Launch permits additional Development environments, which is useful in large organizations in which multiple developers are working on different projects at the same time.

These are the only environments we need to complete the tutorial. Environments allow you to have different working versions of your Launch libraries with different embed codes, so you can safely add new features and make them available to the right users (e.g. developers, QA engineers, the public, etc.) at the right time.

Now let's copy the embed code:

1. In the **[!UICONTROL Development]** row, click the Install icon ![Install icon](images/web-launch-installIcon.png) to open the modal.

1. If you have previously used Launch in websites, one of the first things you will notice is that there is a lot more information in this modal than for web Launch properties.

1. Now, beneath the `Environment ID`, change the operating system to `iOS`

   ![Install icon](images/mobile-launch-openEmbedCode.png)

Let's go through the instructions step-by-step.

## Create the Podfile

The Adobe Mobile SDK for iOS uses the CocoaPods to manage dependencies between its various components. If you don't already have [CocoaPods](https://cocoapods.org/) installed in your development environment, follow the installation instructions on their website. Also, if you haven't already downloaded the [Bus Booking app](assets/iOS_Standalone.zip), save it to your local machine and extract the zip archive to your desktop.

**To create the Podfile**

1. Open the `Terminal` Application on your Mac
1. Navigate to the project folder where you saved the Bus Booking app (e.g. `cd Desktop/iOS_Standalone/BusDemoSwift/`)
   ![navigate to the project directory](images/mobile-launch-install-goToProjectDirectory.png)
1. In the Launch interface, copy the first iOS instruction `pod init`, by clicking the ![Copy](images/mobile-launch-copyIcon.png) icon
   ![Copy pod init to your clipboard in the Launch interface](images/mobile-launch-install-copyPodInit.png)

1. In your Terminal app, run the `pod init` command and wait for it to complete
   ![Run pod init](images/mobile-launch-install-runPodInit.png)
1. In your Terminal app, open the podfile with the `open podfile` command
   ![Run open podfile](images/mobile-launch-install-openPodfile.png)
1. Your computer may open a dialog asking which application you would like to open the podfile with. Choose any text editor, like `TextEdit`

1. In the Launch interface, copy the list of dependencies by clicking the ![Copy](images/mobile-launch-copyIcon.png) icon. Note how there is a line corresponding to each one of the extensions you added in the earlier lesson. Each extension has its own set of code which builds on the Mobile Core extension and can only be added or removed with an app update:
   ![Copy dependencies to your clipboard in the Launch interface](images/mobile-launch-install-copyDependencies.png)

1. In your text editor, add paste the dependencies from your clipboard right after the  line `# Pods for BusDemoSwift`
1. Save the updates to the podfile in your text editor
   ![Add dependencies and save](images/mobile-launch-install-addDependenciesAndSave.png)

1. In the Launch interface, copy the next iOS instruction `pod repo update`, by clicking the ![Copy](images/mobile-launch-copyIcon.png) icon
   ![Copy pod repo update](images/mobile-launch-install-copyPodRepoUpdate.png)

1. In your Terminal app, run the `pod repo update` command and wait for it to complete (this might take a few minutes)
   ![Run pod repo update](images/mobile-launch-install-podRepoUpdate.png)

1. In the Launch interface, copy the next iOS instruction `pod install`, by clicking the ![Copy](images/mobile-launch-copyIcon.png) icon
   ![Copy pod install to your clipboard in the Launch interface](images/mobile-launch-install-copyPodInstall.png)

1. In your Terminal app, run the `pod install` command and wait for it to complete
   ![Run pod install](images/mobile-launch-install-podInstall.png)

1. Open a Finder window, navigate to the folder where you saved the Bus Booking app, and confirm that the BusDemoSwift.xcworkspace file, the Podfile, the Podfile.lock file, as well as the Pods folder have been created

   ![Confirm pods in the finder](images/mobile-launch-install-podsInFinder.png)

## Update the AppDelegate

Now it's time to update the App to import the SDK

1. Open the `BusDemoSwift.xcworkspace` file in XCode
1. Open the AppDelegate.swift file

   ![Copy the Swift import statements to your clipboard](images/mobile-launch-install-openAppDelegate.png)

1. In the Launch interface, scroll to the **[!UICONTROL Add Initialization Code]** section and choose **[!UICONTROL Swift]** as the iOS language you are using.
1. Copy the import statements, by clicking the first ![Copy](images/mobile-launch-copyIcon.png) icon in the [!UICONTROL Add Initialization Code] section:

   ![Copy the Swift import statements to your clipboard](images/mobile-launch-install-copyImports.png)

1. In XCode, paste these import statements into the AppDelegate file after the import for the `UIKit`

   ![Paste the Swift import statements into your AppDelegate file](images/mobile-launch-install-pasteImports.png)

1. In the Launch interface, copy the two lines related to the Core extension, by clicking the second ![Copy](images/mobile-launch-copyIcon.png) icon in the [!UICONTROL Add Initialization Code] section. The first line turns on console logging statements (available options are "debug", "verbose", "warning", and "error"). The second line points to the unique identifier of the Launch environment. This is important, as you will need to update this value when we are ready to deploy the app to the production environment.

   ![Copy the Core statements to your clipboard](images/mobile-launch-install-copyCore.png)

1. In XCode, paste these Core statements into the AppDelegate file at the top of the `application(_:didFinishLaunchingWithOptions:)` method:

   ![Paste the Core statements into your AppDelegate file](images/mobile-launch-install-pasteCore.png)

1. In the Launch interface, copy the extension statements, by clicking the third ![Copy](images/mobile-launch-copyIcon.png) icon in the [!UICONTROL Add Initialization Code] section:

   ![Copy the Extension statements to your clipboard](images/mobile-launch-install-copyExtensions.png)

1. In XCode, paste these extension statements into the AppDelegate file just before the `return true` line of the `application(_:didFinishLaunchingWithOptions:)` method:

   ![Paste the Extension statements into your AppDelegate file](images/mobile-launch-install-pasteExtension.png)

## Verify the implementation

1. Save your XCode project
1. Run the app and launch it in the emulator. If you don't have any emulator devices configured, configure one now, being sure to configure a device running iOS 10+ (in the screenshots below, the app will launch in an iPhone XR emulator)

   ![Run the app and launch it in the emulator](images/mobile-launch-install-buildAndLaunch.png)

1. Wait for the emulator to launch and fully open the app to the booking screen

   ![Wait for the app to full open](images/mobile-launch-install-simulator.png)
  
1. Confirm that calls are being made to the Adobe servers in the XCode Console

   ![Wait for the app to full open](images/mobile-launch-install-console.png)

Here are examples of some specific calls you can look for:

1. **Calls to retrieve the Launch configuration** (filter your console to `adobedtm.com`). Note the extension configurations which you entered in the earlier lesson. While adding the extension requires an update to the app, these settings can be managed externally in Launch and changed at any time:
    ```swift
    2019-01-15 12:11:44.518220-0500 BusDemoSwift[52399:5056293] [AMSDK DEBUG <RulesDownloader>]: Successfully downloaded Rules from 'https://assets.adobedtm.com/launch-EN360aefc739b04410816f751a95861744-development-rules.zip'
    {"target.propertyToken":"","target.timeout":5,"global.privacy":"optedin","analytics.backdatePreviousSessionInfo":true,"analytics.offlineEnabled":true,"build.environment":"dev","rules.url":"https://assets.adobedtm.com/launch-EN360aefc739b04410816f751a95861744-development-rules.zip","target.clientCode":"techmarketingdemos","experienceCloud.org":"7ABB3E6A5A7491460A495D61@AdobeOrg","target.autoFetch":true,"target.fetchBackground":true,"lifecycle.sessionTimeout":300,"target.environmentId":"busbookingapp","analytics.server":"tmd.sc.omtrdc.net","analytics.rsids":"tmd-mobile-dev1","analytics.batchLimit":0,"property.id":"PRb4881271498b4f2cbaf67d38a8f3891a","global.ssl":true,"analytics.aamForwardingEnabled":true}
    ```

1. **Request to the ID Service** (filter your console to `demdex.net`) In this example, the ID (`d_mid`)has already been set and is just being reported up again)

    ```swift
    2019-01-15 12:11:45.164590-0500 BusDemoSwift[52399:5056322] [AMSDK DEBUG <com.adobe.module.identity>]: Sending request (https://dpm.demdex.net/id?d_rtbd=json&d_ver=2&d_orgid=7ABB3E6A5A7491460A495D61@AdobeOrg&d_mid=17179986463578698626041670574784107777&d_blob=j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI&dcs_region=9)
    ```

1. **Response from the ID Service** (filter your console to `ID Service`). Note how the `mid` value matches the `d_mid` value in the request above:

    ```swift
    2019-01-15 12:11:45.681821-0500 BusDemoSwift[52399:5056322] [AMSDK DEBUG <com.adobe.module.identity>]: ID Service - Got ID Response (mid: 17179986463578698626041670574784107777, blob: j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI, hint: 9, ttl: "604800000 ms")
    ```
1. **Analytics request** (filter your console to `Analytics request`)

    ```swift
    2019-01-15 12:11:45.828465-0500 BusDemoSwift[52399:5056336] [AMSDK DEBUG <AnalyticsHitDatabase>]: Analytics request was sent with body (ndh=1&c.&a.&AppID=BusDemoSwift%201%20%281.0%29&CarrierName=%28null%29&DayOfWeek=3&DaysSinceFirstUse=0&DaysSinceLastUse=0&DeviceName=x86_64&HourOfDay=12&LaunchEvent=LaunchEvent&Launches=3&OSVersion=iOS%2012.1&Resolution=828x1792&RunMode=Application&TimeSinceLaunch=0&ignoredSessionLength=-1547572244&internalaction=Lifecycle&locale=en-US&.a&.c&aamb=j8Odv6LonN4r3an7LhD3WZrU1bUpAkFkkiY1ncBR96t2PTI&aamlh=9&ce=UTF-8&cp=foreground&mid=17179986463578698626041670574784107777&pageName=BusDemoSwift%201%20%281.0%29&pe=lnk_o&pev2=ADBINTERNAL%3ALifecycle&t=00%2F00%2F0000%2000%3A00%3A00%200%20300&ts=1547572305)
    ```

Congratulations, you've added the SDK to a mobile app!

[Next "Add the Experience Cloud ID Service" >](id-service.md)