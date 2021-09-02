# Building the Experience Platform Launch extension interface

## Prerequisites

1. Create a new company.

   For more information, see the document on [company setup](https://experienceleague.adobe.com/docs/launch/using/extension-dev/submit/setup.html).

2. (Optional) Create a new listing in the Exchange Partner Portal.

   For more information, see the document on \[creating an exchange listing\]([https://experienceleague.adobe.com/docs/launch/using/extension-dev/submit/create-listing.html](https://experienceleague.adobe.com/docs/launch/using/extension-dev/submit/create-listing.html).

3. Create a new Adobe I/O integration.

   For more information, see the tutorial on [creating an Adobe I/O integration](https://experienceleague.adobe.com/docs/launch/using/extension-dev/submit/upload-and-test.html?lang=en#integration).

## Build an Experience Platform Launch extension interface

To build the Experience Platform Launch extension interface, complete the following steps:

1. Create a new directory for your Experience Platform Launch extension.
2. In a terminal window, run `npx @adobe/reactor-scaffold`.
   * The scaffold tool prompts you with a series of questions to build the extension folder and add the appropriate metadata. 
   * Make sure that you have your Android Maven and iOS CocoaPods URLs handy.
3. Develop the extension.

   a. Edit the `src/view/configuration/configuration.html` file that was created by the scaffold tool.

   b. Modify this page if you need to config parameters from customers.

   If you used the scaffold tool to add actions/events or data elements as part of your extension, these will have separate folders with HTML files that can be modified.

4. In a terminal window, run `npx @adobe/reactor-sandbox`.

   This step loads a simulated Experience Platform Launch environment `@ [http://localhost:3000](http://localhost:3000)` to test configuration inputs and other aspects of the Launch extension.

5. In a terminal window, run `npx @adobe/reactor-packager`.

   This step creates a zip file of your finished Experience Platform Launch extension.

6. In a terminal window, run `npx @adobe/reactor-uploader`.

   This step uploads your extension to Experience Platform Launch.

{% hint style="info" %}
Adobe I/O integration keys are needed before you can build the interface. For more information, see [Create an Adobe I/O Integration](https://experienceleague.adobe.com/docs/launch/using/extension-dev/submit/upload-and-test.html?lang=en#integration).
{% endhint %}

