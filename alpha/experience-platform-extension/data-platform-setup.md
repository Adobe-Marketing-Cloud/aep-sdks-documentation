# Data Platform setup

## Prepare Platform

To be able to send data to [Adobe Data Platform](https://platform.adobe.com/) you will need to create an XDM schema and a dataset that uses that schema.

- [Create a schema](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md)
- Assign the XDM ExperienceEvent class to your schema.
- Add the following Mixins: 
  - ExperienceEvent Application Details
  - ExperienceEvent Environment Details
  - ExperienceEvent Commerce Details
- [Create a dataset](https://platform.adobe.com/dataset/overview) where your data should be sent by using the schema created above.

## Requesting a Configuration ID

You must have a configuration ID to be able to use the Mobile SDK. The configuration ID is what ensures that your data is routed to the right place. You can obtain a configuration ID either from your consultant or through Adobe client care, by providing the following information:

- Org ID: You can find this using the instructions [here](https://docs.adobe.com/content/help/en/core-services/interface/manage-users-and-products/organizations.html)
- Dataset ID: This is available in the dataset UI when you click on a dataset
- Schema ID: This is available at the end of the URL of the schema creation/viewing screen
- Friendly Name: This will be the friendly name that will be used in future UIs for this configuration

Once you received your Configuration ID, you can continue with the [Set  up the SDK](./set-up-the-sdk) steps.