# Setup Adobe Experience Platform

## Prepare Platform

To send data to [Adobe Experience Platform](https://platform.adobe.com/), you need to create an XDM schema and a dataset that uses the schema.

* [Create a schema](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md)
* Assign the XDM ExperienceEvent class to your schema.
* Add the following mixins: 
  * ExperienceEvent Application Details
  * ExperienceEvent Environment Details
  * ExperienceEvent Commerce Details
* [Create a dataset](https://platform.adobe.com/dataset/overview) where your data should be sent by using the schema that you created earlier.

## Create an Experience Edge configuration ID

In order to send experience events to Adobe Experience Platform Edge Network, you need an Experience Edge configuration ID, which ensures that your data is routed to the correct location and references the server-side configuration. To create a configuration ID use the following steps:

* Navigate to [AEP Launch UI](https://experience.adobe.com/launch) and click on the `Edge Configurations` button from the left side menu, then click the `New Edge Configuration` button.

* Set up the default environment settings - these settings are used as defaults across the Experience Edge environments.

* In order to start sending events to Adobe Experience Platform, you should enable this section in your Edge configuration. This workflow requires that you have purchased the Adobe Experience Platform. 

  * Select the AEP Sandbox.
  * Select the Streaming Inlet from the dropdown. If needed, create a new one `Create New Inlet...` . 
  * Select the dataset you created in the previous step `Prepare Platform`.

  ![Enable Adobe Experience Platform in Edge configuration](../../.gitbook/assets/aep-enable-dataset.png)

After you created your configuration ID, you can continue with the [Set up the SDK](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/794ac7be1c848e8501c4af1f7fbdbbb2970a04aa/alpha/experience-platform-extension/set-up-the-sdk/README.md) steps.
