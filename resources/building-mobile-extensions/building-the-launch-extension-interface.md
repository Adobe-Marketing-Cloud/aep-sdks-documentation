# Building the Launch extension interface

## Prerequisites

1. Create a new company.

   For more information, see [Company Setup. ](https://developer.adobelaunch.com/extensions/submissions/company-setup/)

2. \(Optional\) Create a new listing in the Exchange Partner Portal.

   For more information, see [Create Exchange Listing](https://developer.adobelaunch.com/extensions/submissions/create-listing/).

3. Create a new Adobe I/O integration.

   For more information, see [Create an Adobe I/O Integration](https://developer.adobelaunch.com/extensions/submissions/upload-and-test/#2-create-an-adobe-io-integration).

## Build a Launch extension interface

To build the Launch extension interface, complete the following steps:

1. Create a new directory for your Launch extension.
2. In a terminal window, run `npx @adobe/reactor-scaffold`.
   * The scaffold tool prompts you with a series of questions to build the extension folder and add the appropriate metadata. 
   * Make sure that you have your Android Maven and iOS CocoaPods URLs handy.
3. Develop the extension.

   a. Edit the `src/view/configuration/configuration.html` file that was created by the scaffold tool.

   b. Modify this page if you need to config parameters from customers.

   If you used the scaffold tool to add actions/events or data elements as part of your extension, these will have separate folders with HTML files that can be modified.

4. In a terminal window, run `npx @adobe/reactor-sandbox`.

   This step loads a simulated Launch environment `@ [http://localhost:3000](http://localhost:3000)` to test configuration inputs and so on.

5. In a terminal window, run `npx @adobe/reactor-packager`.

   This step creates a zip file of your finished Launch extension.

6. In a terminal window, run `npx @adobe/reactor-uploader`.

   This step uploads your extension to Launch.

   **Tip**: Adobe I/O integration keys are needed before you can build the interface. For more information, see [Create an Adobe I/O Integration](https://developer.adobelaunch.com/extensions/submissions/upload-and-test/#2-create-an-adobe-io-integration).

