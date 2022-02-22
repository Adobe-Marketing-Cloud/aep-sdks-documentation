# Push Debug View

## Overview

The Push Debug View provides the ability to validate the Push setup for your app and send a test message to your device. To get us started, here is a screen shot of the complete view when everything is working as expected:

![Happy Path](../../../.gitbook/assets/push-happy-path)

## Guide

This guide will cover the view from top to bottom.

### Clients

At the very top of the window you'll find a clients dropdown:

![Client Dropdown](../../../.gitbook/assets/push-clients)

Inside the dropdown you'll find a list of each unique client that has connected to this Griffon session. A client is either a unique device or a unique app install for a device. So for example, if I connect an Android device and an iOS device to my session, I'd see those in the Clients dropdown. If I reinstall my iOS app and reconnect to the same Griffon session, I'd see a third client (usually my device name with a #2).

This view validates clients one at a time so selecting a different client will change the details on the screen.

### Push Details

This section will validate and provide additional details about your push setup. In a perfect world, you'll see three green checkmarks in the three panels. This means that your app is configured for push messaging, is writing push tokens to the user profile, and has an associated App Surface configured.

If something is not working as expected, you will see an alert with details on how to fix that problem:

![Invalid State](../../../.gitbook/assets/push-invalid-state)

#### Client Details

This panel checks to see if the device is configured correctly. This includes configuring the extension in Launch, initializing the extension and its prerequisites in your application, and capturing the push token from the device.

If valid, the Panel will display the Ecid for the device, the Push Token, and the Edge Sandbox name and type.

#### Profile Details

Once your client is set up correctly, this will check to see if the device is writing to profile. It also validates that the Push Token in the profile matches the one on the device.

If valid, the panel will show the Ecid for the device, the Push Token, the App ID of your application, the messaging platform, and whether the push token has been deny listed. The token can be deny listed for various reasons like the user has uninstalled the app or the user has disabled push messaging for the app.

![Blocked](../../../.gitbook/assets/push-deny-list-blocked)

Finally, at the bottom of the panel is a link that will open this specific profile in a new tab.

#### App Store Credentials & Configuration

This validates that the App ID and the messaging platform that was saved in the profile has a matching App Surface created. This is where you will go to upload your push credentials for the application.

If valid, the profile will display the name of the App Surface, the App ID, and the name of the messaging service.

Finally, at the bottom of the panel is a link that will open this specific App Surface in a new tab.


### Testing

If everything is set up correctly, you can send a test message to your device. There are a couple use cases for this:

#### Use Case: Validate Setup

If you are looking to make sure everything is set up correctly and that your push credentials are valid, you'll simply set a title and a body for your message and send it:

![Send Test](../../../.gitbook/assets/push-send-test)

In the test results section a new entry will appear. This is showing the message as it is passed through the Adobe Messaging Services and onto the push credential's messaging service. If everything goes according to plan, you'll see the message popup on your device:

![Test Results](../../../.gitbook/assets/push-test-results)

If something went wrong, the Test Results section should show an error of some sort for more information:

![Test Results Error](../../../.gitbook/assets/push-test-error)

#### Use Case: Developing/Testing Advanced Message Features

Several of the advanced message features like click behaviors and rich media will require additional setup steps from your developers. The additional tabs in the Testing section can help the developer test that these features are working.

![Rich Media](../../../.gitbook/assets/push-rich-media)
