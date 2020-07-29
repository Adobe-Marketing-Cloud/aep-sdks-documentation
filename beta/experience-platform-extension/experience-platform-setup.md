# Setup Adobe Experience Platform

{% hint style="warning" %}
The Adobe Experience Platform - Experience Edge - Mobile extension is currently in beta. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more.
{% endhint %}

## Setup Adobe Experience Platform

To send data to [Adobe Experience Platform](https://platform.adobe.com/), you need to create an XDM schema and a dataset that uses the schema.

* [Create a schema](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md)
* Assign the XDM ExperienceEvent class to your schema.
* Add the following mixins: 
  * ExperienceEvent Application Details
  * ExperienceEvent Environment Details
  * ExperienceEvent Commerce Details
* [Create a dataset](https://platform.adobe.com/dataset/overview) where your data should be sent by using the schema that you created earlier.

## Requesting a configuration ID

To use the Mobile SDK, you need a configuration ID, which ensures that your data is routed to the correct location. To obtain a configuration ID from your consultant or through Adobe Client Care, provide the following information:

* Org ID: To locate this ID, complete the instructions in [Organizations and account linking](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html).
* Dataset ID, which is available in the dataset UI when you click on a dataset.
* Schema ID, which is available at the end of the URL of the schema creation/viewing page.
* Friendly Name, which is the name that will be used in future UIs for this configuration.

After you received your configuration ID, you can continue with the [Set up the SDK](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/794ac7be1c848e8501c4af1f7fbdbbb2970a04aa/alpha/experience-platform-extension/set-up-the-sdk/README.md) steps.

