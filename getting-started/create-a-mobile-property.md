# Set up a mobile property

A property is a container that you fill with extensions, rules, data elements, and libraries. To use these resources, you need to create and configure a mobile property in [Adobe Experience Platform Launch](https://launch.adobe.com). You will typically create a mobile property for each mobile application you want to manage.

## Before you start

Before you can set up your mobile property, complete the following prerequisites:

### Set up groups and users

Launch is fully integrated with your Adobe ID. User permissions are managed through the Admin Console with other Adobe products and solutions from the Creative Cloud, Document Cloud, and Experience Cloud.

For detailed instructions on how to create groups and add users for Launch, see [user permissions](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=en).

### Log in to Experience Platform Launch

After Experience Platform Launch rights have been added to your Adobe ID, log in to Launch. You can do this by going to [https://experience.adobe.com/\#/data-collection](https://experience.adobe.com/#/data-collection) or by logging in to the [Experience Cloud](https://experiencecloud.adobe.com), navigating to the Activation page, and selecting Launch.

## Create a mobile property

1. Log in to Experience Platform Launch.
2. On the main page, review the list of existing mobile and web properties.
3. Click **New Property**.
4. Type a name for the property and select **Mobile** as the platform.

   If necessary, you can change the [**Privacy**](../resources/privacy-and-gdpr.md#setting-privacy-status) setting later.

5. Click **Save** to create the mobile property.
6. Search for the property you just created and click it to open it.

{% hint style="danger" %}
The default privacy status is set to _opted in_ and might impact data collection. For more information, see [Privacy and GDPR](../resources/privacy-and-gdpr.md).
{% endhint %}

![Setting default privacy status](../.gitbook/assets/createmobileprop.png)

## Install your extensions

An extension is an integration built by Adobe or an Adobe partner that adds new options you can use in your apps. By default, all new mobile properties come with the Mobile Core and Profile extensions installed.

The Mobile Core extension provides a robust default set of functionality, including lifecycle events and conditions. The Profile extension allows storing of data into a client-side profile. Additional functionality for Analytics, Target, and so on will come from extensions that you install from the catalog. For more information, see the document on [adding a new extension](https://experienceleague.adobe.com/docs/experience-platform/tags/ui/extensions/overview.html?lang=en#add-a-new-extension).

## Set up your extensions

1. In Experience Platform Launch, on the details page for your mobile property, click the **Extensions** tab.

   The **Mobile Core** and **Profile** extensions are installed by default.

2. On the **Mobile Core** card, click **Configure** to open the extensions detail page.

   ![](../.gitbook/assets/screen-shot-2018-10-02-at-5.02.05-pm-2.png)

3. Check your Experience Cloud Org ID.

   By default, this value is auto-populated using the currently signed-in Organization ID. This is a required identifier for your Experience Cloud Organization and is typically a 24-character, alphanumeric string followed by _@AdobeOrg_. If you need help finding it, contact your Adobe CSM or Customer Care.

4. \(Optional\) Provide your Experience Cloud ID Server.

   This is an optional server value that is used to send Visitor ID Service network requests to a custom endpoint. If this property is not set, the visitor identifiers sync requests are sent to _dpm.demdex.net_ when the `Identity` extension is registered.

5. \(Optional\) Change the **Session Timeout** value.

   A default value of 300 seconds is already set. This timeout value indicates the number of seconds that must pass after a user backgrounds the app before a launch is considered to be a new Lifecycle session.

6. Click **Save** to confirm your settings for **Mobile Core**.

## Publish the configuration

Before the mobile application can access the configuration, it needs published to an environment. For now, we need to publish the Mobile Core and Profile extension configurations.

To deploy your configuration to a development environment for testing:

1. In Experience Platform Launch, on your mobile property's details page, click the **Publishing Flow** menu.
2. Under the **Development** section of the publishing workflow, click **Add New Library**.
3. Specify any name for the library **Name**.
4. From the **Environment** drop-down list, select Development as the environment.
5. Click **Add All Changed Resources** to add the configuration changes to be deployed. You will see the Mobile Core and Profile extensions listed as changes to be published.
6. Click **Save & Build for Development**.

   The library builds and is displayed under the **Development** section of the publishing workflow.

7. On the library card, click the ellipsis \(...\) to see a dropdown list.
8. Select **Submit for Approval** and then **Submit**.

The library of changes are then published to the Development environment and the library is displayed under the **Submitted** section of the publishing workflow.

{% hint style="info" %}
Testing can be done using the configuration in the Development environment. The library can later be deployed to the **Staging** and **Production** environments by using the rest of the publishing workflow. For more information, see the documentation on [publishing in Launch](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html?lang=en).
{% endhint %}

Now that you published your configuration, get the Adobe Experience Platform SDK for your application. For more information, see tutorial on [getting the Experience Platform SDKs](get-the-sdk.md).

## Watch the video

{% embed url="https://youtu.be/xBWYFUKAoyo" caption="Video: Creating Mobile Properties in Experience Platform Launch" %}

## Additional information

* To learn more about getting access to Launch, see the [user permissions](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/manage-permissions.html) document.
* To learn more about Experience Platform Launch's publishing workflows, watch this [video](https://www.youtube.com/embed/Pe-YSn26_xI).

## Get help

* To ask questions, visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk).
* For immediate assistance, contact [Adobe Experience Cloud customer care](https://experienceleague.adobe.com/?support-solution=General#support).

