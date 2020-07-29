---
description: >-
  This step will show how you may generate a configuration identifier necessary
  for the Experience Edge Extension implementation.
---

# Generate Configuration Identifier

{% hint style="warning" %}
The Adobe Experience Platform - Experience Edge - Mobile extension is currently in beta. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more.
{% endhint %}

## Initialize Adobe Experience Platform for data collection

To begin collecting data in [Adobe Experience Platform](https://experience.adobe.com/platform), you need to create an XDM schema and a dataset that uses the schema. Follow these steps to get started:

1. [Create a schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-ui.html)
2. Assign the XDM ExperienceEvent class to your schema.
3. Add the following mixins: 
   * ExperienceEvent Application Details
   * ExperienceEvent Environment Details
   * ExperienceEvent Commerce Details
4. [Create a dataset](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/user-guide.html#create) where your data should be sent by using the schema that you created earlier.

## Generate a Experience Edge configuration identifier

In order to send events to the Experience Edge, the SDK will require a configuration identifier to ensure your implementation matches your server-side configuration and data is routed/received to/from the correct destination. 

To create a configuration identifier use the following steps:

1. Navigate to [Adobe Experience Platform Launch](https://experience.adobe.com/launch) and click on the `Edge Configurations` button from the left side menu, then click the `New Edge Configuration` button.
2. Set up the default environment settings - these settings are used as defaults across the Experience Edge environments.
3. In order to start sending events to Adobe Experience Platform, you should enable this section in your Edge configuration. This workflow requires that you have purchased the Adobe Experience Platform.

   * Select the AEP Sandbox.
   * Select the Streaming Inlet from the dropdown. If needed, create a new one `Create New Inlet...` . 
   * Select the dataset you created in the previous step `Prepare Platform`.

   ![Enable Adobe Experience Platform in Edge configuration](../../.gitbook/assets/aep-enable-dataset.png)

After you have have successfully generated a configuration identifier, you may continue with the [Set up the SDK](https://aep-sdks.gitbook.io/docs/beta/experience-platform-extension/set-up-the-sdk) steps.

