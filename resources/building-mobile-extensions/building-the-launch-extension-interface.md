# Building the Launch Extension Interface

## Prerequisites

1. Create a new Company. For more information, see [Your Experience Cloud Account](https://developer.adobelaunch.com/guides/extensions/getting-started/#your-experience-cloud-account).
2. Create a new listing in the Exchange Partner Portal. For more information, see [Create a Listing in the Exchange Partner Portal \(optional\)](https://developer.adobelaunch.com/guides/extensions/getting-started/#create-a-listing-in-the-exchange-partner-portal-optional).
3. Create a new Adobe I/O integration. For more information, see [Creating an Adobe I/O Integration](https://developer.adobelaunch.com/guides/extensions/getting-started/#creating-an-adobe-io-integration).

## Build a Launch Extension Interface

To build the Launch extension interface, complete the following steps:

1. Create a new directory for your Launch extension.
2. Run `npm @adobe/reactor-scaffold`.
3. The scaffold tool will prompt you with a series of questions to build out the extension folder and add appropriate metadata. Make sure to have your Android Maven and iOS CocoaPods URLs handy.
4. Develop the extension.
5. Edit the src/view/configuration/configuration.html file created by the scaffold tool. Modify this page if you need to config parameters from customers. If you used the scaffold tool add actions/events or data elements as part of your extension, these will have separate folders with HTML files that can be modified.
6. Run npm @adobe/reactor-sandbox.
7. Loads a simulated Launch environment @ [http://localhost:3000](http://localhost:3000) for testing configuration inputs etc.
8. Run npm @adobe/reactor-package.
9. Creates a zip file of your finished Launch extension.
10. Run npm @adobe/reactor-uploader.
11. Will upload your Extension to Launch. \(Adobe I/O integration keys needed as pre-req\).

