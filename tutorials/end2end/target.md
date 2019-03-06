---
title: Implement Target with Launch
description: Learn how to implement Adobe Target using Launch with at.js, a global mbox, parameters, an order mbox, and custom header/footer code. This lesson is part of the Implementing the Experience Cloud in Websites with Launch tutorial.
seo-description:
seo-title: Implement Target with Launch
solution: Experience Cloud
---

# Add Adobe Target Visual Experience Composer (VEC)

In this lesson, we will enable the Target Visual Experience Composer (VEC) for Mobile apps.

[Adobe Target](https://marketing.adobe.com/resources/help/en_US/target/) is the Adobe Experience Cloud solution that provides everything you need to tailor and personalize your customers' experience, so you can maximize revenue on your web and mobile sites, apps, social media, and other digital channels.

The Visual Experience Composer (VEC) for Native Mobile Apps lets you create activities and personalize content on native mobile apps in a do-it-yourself fashion without continuous development dependencies and app-release cycles.

In the lesson [Add Extensions](launch-add-extensions.md), you added the Target VEC extension to your Launch property. In the lesson [Install the Mobile SDK](launch-install-the-mobile-sdk.md) you imported the extension into the sample application. Only a few minor updates are required to start setting up activities in Target's mobile visual experience composer!

>[!NOTE] Both the Target and Target VEC Launch extensions are required to use the Target VEC in your mobile application.

## Learning Objectives

At the end of this lesson, you will be able to:

* Enable the sample app for the Target VEC
* Add parameters to the Target VEC request
* Pair your device with the VEC
* Create an activity using the VEC

## Prerequisites

To complete the lessons in this section, you must first complete the lessons in [Configure Launch](launch-create-a-property.md) section.

## Enable logging for the Target VEC extension

This is an optional step that will turn on special console logging specific to the VEC extension.

**To enable logging**

1. Open the AppDelegate.swift file
1. Add the line of code `ACPTargetVEC.allowDebugLogging(true)` just below the line where you register the Target VEC Extension

   ![Enable Target VEC Logging](images/mobile-targetvec-enableLogging.png)

Now that you've enabled the logging, it's time to confirm that it is working.

**To verify the logging**

1. Save the XCode project
1. Rebuild the app
1. When the app has opened successfully click in the Console pane of XCode
1. Use ⌘-F to open the Find box
1. Search for `targetvec` in the Find box
1. Hit `Enter` to jump to the Target request and Post body (Note that the Lifecycle parameters are automatically included):

   ![Verify Target VEC Logging](images/mobile-targetvec-requestInConsole.png)

## Add Parameters

As you just saw in the last exercise, app Lifecycle metrics are automatically included as parameters in the Target VEC request. You can also add custom parameters to the requests.

**To add custom parameters**

1. In XCode, open the `BookingViewController.swift` file
1. Import the Target VEC extension by adding `import ACPTargetVEC_iOS` beneath the existing import:
1. In the `viewDidLoad()` function, after the line with `super.viewDidLoad()` add the following code. This example code shows how mbox parameters, profile parameters, product (or entity) parameters, and order parameters can be added to the TargetVEC request. This example uses static values, while in your actual app you would want to use dynamic variables to populate the values:

```swift
        let mboxParams = ["mboxparam1":"mboxvalue1"]
        let profileParams = ["profilekey1":"profilevalue1"]
        let product : TargetProduct = TargetProduct.init(productId: "1234", categoryId: "furniture")
        let order : TargetOrder = TargetOrder.init(orderId: "12345", total: 123.45, purchasedProductIds: ["100", "200"])
        let targetParams : TargetParameters = TargetParameters.init(parameters: mboxParams, profileParameters: profileParams, product: product, order: order)
        ACPTargetVEC.setGlobalRequest(targetParams)
```

   ![Add Parameters to the TargetVEC request](images/mobile-targetvec-addParameters.png)

Now that you've added parameters to the app, it's time to confirm they are being passed in the request.

**To verify the parameters**

1. Save the XCode project
1. Rebuild the app
1. When the app has opened successfully click in the Console pane of XCode
1. Use ⌘-F to open the Find box
1. Search for `targetvec` in the Find box
1. Hit `Enter` to jump to the Target request and Post body (Note that the Lifecycle parameters are automatically included):

   ![Verify Parameters to the TargetVEC request](images/mobile-targetvec-verifyParams.png)

## Pairing the Mobile App with the Target UI

In order to create VEC activities in the Target interface, you must first pair Target with your app. This pairing is achieved with the use of deep links.

### Creating the Deep Link Scheme

iOS supports the use of [Universal Links](https://developer.apple.com/documentation/uikit/core_app/allowing_apps_and_websites_to_link_to_your_content) and [custom URL schemes](https://developer.apple.com/documentation/uikit/core_app/allowing_apps_and_websites_to_link_to_your_content/defining_a_custom_url_scheme_for_your_app) to create deep links to your app. You are probably already using custom URL schemes in your app already. If so, you can use these existing links to pair with Target. For this tutorial using the sample app in the simulator, you must create a custom URL scheme.

**To register your URL Scheme**

1. In XCode, click on your app to open the Settings screen
1. On the Settings screen, click the `Info` tab
1. Enter a **[!UICONTROL Identifier]** (e.g. `com.danielwright.BusDemo` substituting your name for `danielwright`)
1. Enter the **[!UICONTROL URL Scheme]** (e.g. `danielwrightBusDemo` substituting your name for `danielwright`)
1. Make sure  **[!UICONTROL Editor]** is selected as the **[!UICONTROL Role]**

   ![Register the URL Scheme](images/mobile-targetvec-registerScheme.png)

1. Click on the `General` tab so the scheme will save
1. Click back on the `Info` tab, expand the `URL type` section and verify that your URL type saved
  
The next step is to add a handler to the deep link.

**To handle the deep links**

1. Open the AppDelegate.swift file
1. Add the line `ACPTargetVEC.handleDeepLink(url)` to the `AppDelegate:application:openURL` section as pictured below
   ![Update the AppDelegate file](images/mobile-targetvec-appDelegate.png)

### Verify the deep link

Now, when a user with your app installed opens the URL `danielwrightBusDemo://com.danielwright.BusDemo` (or whatever scheme you defined) it will open your application.

**To verify the deep link scheme**

1. Save the XCode project
1. Rebuild the app
1. In the simulator, open Safari
1. Enter the url scheme you just defined into the address bar, e.g. `danielwrightBusDemo://com.danielwright.BusDemo`
1. You should get prompted with a modal to "Open this page in "BusDemoSwift" (if you get a Google search results page, try reentering the deep link into the address bar)
1. Click `Open`
1. This should open the sample application

   ![Verify the deep link](images/mobile-targetvec-verifyDeepLink.png)

Now that your deep link structure is set up, you are ready to use the Target VEC to set up activities!

## Create an activity in the Mobile VEC

Now let's create an activity in the Target UI.

**To Create an Activity with the Target VEC**

1. Log into the [Adobe Experience Cloud](https://experiencecloud.adobe.com)
1. Use the solution switcher to go to Target

   ![Verify the deep link](images/mobile-targetvec-goToTarget.png)

1. Launch Target

   ![Verify the deep link](images/mobile-targetvec-launchTarget.png)

1. Click the **[!UICONTROL Create Activity]** button and select **[!UICONTROL A/B Test]**
1. Select **[!UICONTROL Mobile App]**
1. Make sure **[!UICONTROL Visual]** is selected under **[!UICONTROL Choose Experience Composer]**
1. Click the **[!UICONTROL Next]** button
  
   ![Create an A/B Activity using the Mobile VEC](images/mobile-targetvec-createActivity.png)

1. On the **[!UICONTROL Select an app to use]** screen, click **[!UICONTROL Add New App]**

   ![Add a new app](images/mobile-targetvec-addNewApp.png)

1. Enter the url scheme you just defined in the  **[!UICONTROL Enter URL scheme]** field, e.g. `danielwrightBusDemo://com.danielwright.BusDemo`
1. Click **[!UICONTROL Create Deep Link]**

   ![Enter your URL Scheme and Create the Deep Link](images/mobile-targetvec-enterURLScheme.png)

    >![NOTE] You have a few options to send the deep link to the app. You can:
    >
    >   1. Take a photo of the QR code if you have an iOS device linked to XCode
    >   1. Copy the deep link from the Target interface and send it to the device however you would like
    >   1. Email the deep link to a valid email address and then open the link with an email application on the device

1. Click on the **[!UICONTROL Copy & Send Link]** tab.

   ![Copy the URL](images/mobile-targetvec-copyURL.png)

1. Switch back to the Simulator
1. Open Safari in the Simulator
1. Paste the deep link URL into the address bar
1. Click to open the app

   ![Copy the URL](images/mobile-targetvec-pasteURL.png)

    >![TIP] If you are unsuccessful when copy-and-pasting the URL from your Desktop to the Simulator try one of the following tricks:
    >
    >   1. **If your Desktop's clipboard is not synced with your Simulator's clipboard** this will prevent you from copy-and-pasting the URL from the Target UI into the Simulator's Safari browser. If this happens, try toggling off and on the `Automatically Sync Pasteboard` setting in the Simulator and copy/pasting again
    >
    >      ![Toggle the Simulator's clipboard setting](images/mobile-targetvec-toggleClipboard.png)
    >
    >   1. **If going to your URL keeps performing a search instead of opening the app**, and you were successful opening a deep link earlier, you won't be able to complete the pairing. Try repasting the deep link URL into the address bar and hitting `Enter` a few times.

1. After the App has loaded, switch back to your browser tab where you have Target opened. You should see your app loaded in the VEC.
1. Click on text and image assets in your app and you should see options to edit and replace them!

   ![App loads in the VEC](images/mobile-targetvec-devicePaired.png)

1. Make some changes to the first screen in your app
1. Now position the Simulator next to the browser with the VEC open
1. Navigate to a different screen in the app and notice how the VEC updates with the Simulator!
1. You can make updates to multiple views in your app, in a single activity!
   ![App loads in the VEC](images/mobile-targetvec-navigateTheApp.png)
1. You can also visually add click-tracking metrics!

## Building Audiences based on Lifecyle metrics

You can easily build Target Audiences based on Lifecycle metrics. Look for all of the Lifecycle metric parameters in the **[!UICONTROL Custom]** selection of the Audience builder:

   ![Select the Custom option](images/mobile-targetvec-buildingAudiencesCustom.png)

   ![App loads in the VEC](images/mobile-targetvec-buildingAudiences.png)
  
[Next "Add Adobe Analytics" >](analytics.md)