# Set up a mobile property

To create and configure a mobile property in [Experience Platform Launch](https://launch.adobe.com), complete the following steps:

{% hint style="info" %}
Having trouble creating a mobile property or need access to Experience Platform Launch? See [User Permissions](https://docs.adobelaunch.com/launch-reference/administration/user-permissions).
{% endhint %}

## Create a mobile property

1. Click **New Property**.
2. Type a name and select **Mobile** as the platform.

   If necessary, you can change the [**Privacy** ](../resources/privacy-and-gdpr.md#setting-privacy-status) and **HTTPS** settings later.

3. Click **Save** to create the mobile property.
4. Locate the new property in the displayed Properties list and open it.

{% hint style="danger" %}
The default privacy status is set to _opted in_ and might impact data collection. For more information, see [Privacy and GDPR](../resources/privacy-and-gdpr.md).
{% endhint %}

## Set up your extensions

1. In Experience Platform Launch, click the **Extensions** tab. The **Mobile Core** and **Profile** extensions are installed by default.
2. On the **Mobile Core** card, click **Configure**.

   ![](../.gitbook/assets/screen-shot-2018-10-02-at-5.02.05-pm-2.png)

3. Type your Experience Cloud Org ID.

   By default, this value is auto-populated using the currently signed-in Organization ID. This is a required identifier for your Experience Cloud Organization and is typically a 24-character, alphanumeric string followed by _@AdobeOrg_. If you need help finding it, contact your Adobe CSM or Customer Care.

4. \(Optional\) Provide your Experience Cloud ID Server.

   This is an optional server value that is used to send Visitor ID Service network requests to a custom endpoint. If this property is not set, the visitor identifiers sync requests are sent to _dpm.demdex.net_ when the `Identity` extension is registered.

5. Optionally, change the **Session Timeout** value.

   A default value of 300 seconds is already set. This timeout value indicates the number of seconds that must pass after a user backgrounds the app before a launch is considered to be a new Lifecycle session.

   a. Click **Save** to confirm your settings for **Mobile Core**.

   b. Click **Catalog** and install the extensions that you need.

{% hint style="info" %}
Not sure on what extensions you need? Check out the extensions in the _Using Mobile Extensions_ section.
{% endhint %}

## Publish the configuration

To create a library of changes and deploy the library to a **Development Environment**:

1. In the **Publishing** tab, under the **Development** section of the publishing workflow.

   click **Add New Library**.

2. Specify a name for the library and, from the **Environment** drop-down list, select a development environment .
3. Add the configuration changes to be deployed.
4. Click **Add All Changed Resources.**  To add only some changes, click **Add a Resource**. 
5. Click **Save & Build for Development**.   **Tip**: The library builds and is displayed under the **Development** section of the publishing workflow.
6. Click on the down arrow for the library and select **Submit for Approval**.

The configuration in the library is deployed to the Development environment and the library is displayed under the **Submitted** section of the publishing workflow.

{% hint style="info" %}
Testing can be done using the configuration in the Development environment. The library can later be deployed to the **Staging** and **Production** environments by using the rest of the publishing workflow. For more information, see Launch's [publishing states](https://docs.adobelaunch.com/getting-started-1/validate-and-publish#publish-to-production)**.**
{% endhint %}

## Watch the video

{% embed url="https://youtu.be/xBWYFUKAoyo" caption="Video: Creating Mobile Properties in Experience Platform Launch" %}

## Additional information

* To learn more about getting access to Launch, see [User Permissions](https://docs.adobelaunch.com/launch-reference/administration/user-permissions).
* To learn more about Experience Platform Launch's publishing workflows, watch this [video](https://www.youtube.com/embed/Pe-YSn26_xI).

## Get help

* To ask questions, visit the SDK [community forum](https://forums.adobe.com/community/experience-cloud/platform/launch/sdk).
* For immediate assistance, contact [Adobe Experience Cloud customer care](https://helpx.adobe.com/contact/enterprise-support.ec.html).

