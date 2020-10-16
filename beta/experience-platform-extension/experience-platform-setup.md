---
description: >-
  This step outlines the generation of an Edge environment identifier necessary for the AEP Edge extension
  implementation.
---

# Generate Environment Identifier

{% hint style="warning" %}
The Adobe Experience Platform Edge mobile extension is currently in BETA. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more.
{% endhint %}

## Initialize Adobe Experience Platform for data collection

To start collecting data in [Adobe Experience Platform](https://experience.adobe.com/platform), an XDM schema and a Dataset need to be created. Follow these steps to get started:

1. [Create a schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/tutorials/create-schema-ui.html)
2. Assign the XDM ExperienceEvent class to the schema.
3. Add the following mixins: 
   * ExperienceEvent Application Details
   * ExperienceEvent Environment Details
   * ExperienceEvent Commerce Details
4. [Create a dataset](https://docs.adobe.com/content/help/en/experience-platform/catalog/datasets/user-guide.html#create) where the data should be sent by using the schema defined earlier.

## Generate an Experience Edge environment identifier

The SDK requires a configuration identifier that ensures the implementation matches the server-side Edge configuration and data is routed/received to/from the correct destination.

To create a configuration identifier use the following steps:

1. In [Adobe Experience Platform Launch](https://experience.adobe.com/launch), navigate to your mobile property and select _Edge Configurations_ from the left panel, then select _New Edge Configuration_.
2. Provide a name and description and then proceed to set up the default environment settings. These settings are used as defaults across the Experience Edge environments.
3. To send events to Adobe Experience Platform, enable the `Adobe Experience Platform` section as shown below:
   * Select the `AEP Sandbox`.
   * Select \(or create a new\) the `Streaming Inlet` from the dropdown.
   * For the `Event Dataset`, select the XDM dataset you created in [Initialize Adobe Experience Platform for data collection](experience-platform-setup.md#initialize-adobe-experience-platform-for-data-collection).
   * Click `Save`.

![](../../.gitbook/assets/aep-enable-dataset.png)

