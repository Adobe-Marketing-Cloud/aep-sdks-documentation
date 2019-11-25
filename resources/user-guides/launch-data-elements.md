# Data elements

Data elements are the building blocks for your data dictionary and are used to collect, organize, and deliver data across marketing and ad technology.

A data element is a variable where the value can be mapped to data in the Experience Platform Mobile SDK such as a visitor ID, a device name, a user profile, a number of launches, and so on. In Experience Platform Launch, you can reference this value by its variable name. This collection of data elements becomes the dictionary of defined data that you can use to build rules for your application, and this dictionary is shared across Experience Platform Launch where it can be used with any extension that is added to your property.

You can use data elements during rule creation to consolidate the definition of dynamic data. After defining your data elements, you can reuse them in multiple places.

*Tip*: We recommend reusing data elements as a best practice.

Data elements are building blocks for rules. Data elements allow you create a data dictionary of commonly used data in the Experience Platform Mobile SDK, regardless of where they originate (shared state, event data) or which extension creates them. Data elements are populated with data when they are processed in the Experience Platform Mobile SDK [Rules Engine](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine). 

To use data elements, at a high level, complete the following steps:

{% hint style="info" %}

When a new extension is added to your property, new data elements might become available to use. To use data elements when creating new rules, repeat the following steps to create a data element.

{% endhint %}

## 1. Create a data element

1. On the Property page, on the **Data Elements** tab, click **Add Data Element**.

2. Type a unique data element name.

3. In the **Extension** drop-down list, select the extension that will generate the data element type. 

   You can only select extensions which are currently installed in your property.

4. In the **Data Element Type** drop-down list, select the required configuration parameters. 

   Most data element types do not require any configuration.

5. Click **Save**.

For example, to create a data element that maps to an Experience Cloud ID, on the Create New Data Element page, type **ECID** as the name, select the **Mobile Core** extension, and select the **Experience Cloud ID** data type

![create ECID data element](../../.gitbook/assets/data-elements-create-data-element-ecid.png)

## 2. Using data elements

You can use data elements to define rules in Experience Platform Launch. When a rule configuration allows the use of data elements, click the cylinder icon to display a list of data elements that are defined in the mobile property.

### Example: Creating a rule to send a postback

Here is an example which creates a rule to send a postback containing the Experience Cloud ID when the application launches.

1. On the property page for your mobile property, click the **Rules** tab, and click **Create New Rule**.

2. Type a unique name for the the rule.
3. In the **Events** section, click **Add**. 
   a. In the **Extension** drop-down list, select **Mobile Core**.
   b. In the **Event Type** drop-down list, select **Launched**.
   c. Click **Keep Changes**.
4. In the **Condition** section, click **Add**.
   a. In the **Extension** drop-down list, select **Mobile Core**.
   b. In the **Condition Type** drop-down list, select **Data Element**.
   c. Enter a name for the condition.
   d. Next to the **Data Element** text field, click the cylinder icon and select the ECID that was created in the previous section. 
5. In the **Action** section, click **Add**. 
   a. In the **Extension** drop-down list, select Mobile Core.
   b. In the **Action Type** drop-down list, select **Send Postback**.
   c. In the **URL** text field, type a sample URL, for example, `https://my.company.com/launch?ecid=`.
   d. Enter a name for the action.
   e. Next to the **Data Element** text field, click the cylinder icon and select the ECID that was created in the previous section.
6. Click **Save**.

![create rule](../../.gitbook/assets/data-elements-create-rule.png)

### 3. Publish configuration

After the property is published, this new rule is made available for download by the applications that are configured for this property. For more information, see [Publish the configuration](https://aep-sdks.gitbook.io/docs/getting-started/create-a-mobile-property#publish-configuration) and [Configure the SDK with an Environment ID](https://aep-sdks.gitbook.io/docs/getting-started/initialize-the-sdk#configure-the-sdk-with-an-environment-id). When the application launches, this rule is triggered and, if the ECID exists in the SDK, a postback is sent to the URL with the ECID value.

## Additional information

Here is some additional information about the Rules Engine and the Signal extention:

- [Rules Engine](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine) 

  An overview and technical details of the Experience Platform Mobile SDK Rules Engine.

- [Signal extension and Rules Engine integration](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals/signals-extension-and-rules-engine-integration)

  This content provides an example of how to create rules to trigger actions in the Signals extension.



