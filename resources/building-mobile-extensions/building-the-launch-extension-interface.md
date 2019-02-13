# Building the Launch extension interface

## Prerequisites

1. Create a new Company.

   For more information, see [Your Experience Cloud Account](https://developer.adobelaunch.com/guides/extensions/getting-started/#your-experience-cloud-account).

2. Create a new listing in the Exchange Partner Portal.

   For more information, see [Create a Listing in the Exchange Partner Portal \(optional\)](https://developer.adobelaunch.com/guides/extensions/getting-started/#create-a-listing-in-the-exchange-partner-portal-optional).

3. Create a new Adobe I/O integration.

   For more information, see [Creating an Adobe I/O Integration](https://developer.adobelaunch.com/guides/extensions/getting-started/#creating-an-adobe-io-integration).

## Build a Launch Extension Interface

To build the Launch extension interface, complete the following steps:

1. Create a new directory for your Launch extension.
2. Run `npx @adobe/reactor-scaffold`.
   * The scaffold tool prompts you with a series of questions to build the extension folder and add appropriate metadata. 
   * Make sure that you have your Android Maven and iOS CocoaPods URLs handy.
3. Develop the extension.
   * Edit the _src/view/configuration/configuration.html_ file that was created by the scaffold tool. 
   * Modify this page if you need to config parameters from customers. 
   * If you used the scaffold tool to add actions/events or data elements as part of your extension, these will have separate folders with HTML files that can be modified.
4. Run `npx @adobe/reactor-sandbox`.

   This step loads a simulated Launch environment `@ [http://localhost:3000](http://localhost:3000)` to test configuration inputs and so on.

5. Run `npx @adobe/reactor-packager`.

   This step creates a zip file of your finished Launch extension.

6. Run `npx @adobe/reactor-uploader`.

   This step uploads your Extension to Launch.

   **Tip**: Adobe I/O integration keys are needed before you can build the interface. For more information, see [Creating an Adobe I/O Integration](https://developer.adobelaunch.com/guides/extensions/getting-started/#creating-an-adobe-io-integration).

