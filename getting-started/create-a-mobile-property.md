# Set up a mobile property

To create and configure a mobile property in [Launch](https://launch.adobe.com), complete the following steps: 

{% hint style="info" %}
Having trouble creating a mobile property or need access to Launch? See [User Permissions](https://docs.adobelaunch.com/launch-reference/administration/user-permissions).
{% endhint %}

## Create a new mobile property

1. Click **New Property**
2. Create a new property by providing a name and selecting **Mobile** as the platform.  

    If required, you can change [**Privacy** ](../resources/privacy-and-gdpr.md#setting-privacy-status) and **HTTPS** settings later.

3. Find the new property in the **Properties** list and click to open it.

## Set up your extensions

1. In Launch, click the **Extensions** tab.   
   The **Mobile Core** and **Profile** extensions are installed by default.  

   a. Click **Configure** on the **Mobile Core** card.

      ![](../.gitbook/assets/screen-shot-2018-10-02-at-5.02.05-pm%20%282%29.png)

   b. Provide your Experience Cloud Org ID.  
   
      By default, this value is auto-populated using the currently signed-in Organization ID.   This is a required identifier for your Experience Cloud Organization and is typically a 24-character, alphanumeric string followed by _@AdobeOrg_. If you need help finding it, contact your Adobe CSM or Customer Care.

   c. \(Optional\) Provide your Experience Cloud ID Server. 

      This is an optional server value that is used to send Visitor ID Service network requests to a custom endpoint.
   
   d. Optionally, change the **Session Timeout** value. 
   
     A default value of 300 seconds is already set. This timeout value indicates the number of seconds that must pass after a user backgrounds the app before a launch is considered to be a new Lifecycle session.

2. Click **Save** to confirm your settings for **Mobile Core**.
3. Click **Catalog** and install the extensions that you need.

{% hint style="info" %}
Not sure on what extensions you need? Check out the extensions in the **Using Mobile Extensions** section.
{% endhint %}

## Publish Configuration

To create a library of changes and deploy the library to a **Development Environment**:

1. In the **Publishing** tab, under the **Development** section of the publishing workflow.

   click **Add New Library**. 

2. Specify a name for the library and, from the **Environment** drop-down list, select a development environment .
3. Add the configuration changes to be deployed.
4. Click **Add All Changed Resources.** To add only some changes, click **Add a Resource**. 
5. Click **Save & Build for Development**.  **Tip**: The library builds and is displayed under the **Development** section of the publishing workflow.
6. Click on the down arrow for the library and select **Submit for Approval**.

The configuration in the library is deployed to the Development environment and the library is displayed under the **Submitted** section of the publishing workflow.

{% hint style="info" %}
Testing can be done using the configuration in the Development environment. The library can later be deployed to the **Staging** and **Production** environments by using the rest of the publishing workflow. For more information, see Launch's [publishing states](https://docs.adobelaunch.com/getting-started-1/validate-and-publish#publish-to-production)**.**
{% endhint %}

## Watch the Video

{% embed url="https://youtu.be/xBWYFUKAoyo" caption="Video: Creating Mobile Properties in Experience Platform Launch" %}

## Additional Information

* To learn more about getting access to Launch, see [User Permissions](https://docs.adobelaunch.com/launch-reference/administration/user-permissions).
* To learn more about Launch's publishing workflows, watch this [video](https://www.youtube.com/embed/Pe-YSn26_xI).

