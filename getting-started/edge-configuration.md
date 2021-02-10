# Configure the Edge

For mobile data collection via the Adobe Experience Platform Edge Network, the configuration of the Experience Platform Mobile SDK is now split between two workflows within [Experience Platform Launch](https://launch.adobe.com):

{% hint style="warning" %}
To create an Edge configuration, your organization must be provisioned for this feature in Adobe Experience Platform Launch. Please contact your Adobe Customer Success Manager \(CSM\) to be added to the _allow list_.
{% endhint %}

{% hint style="info" %}
The Edge configuration tool is available to customers on the _allow list_ regardless whether they use Experience Platform Launch for web tag management or to manage mobile app configuration.

Users will require _Develop_ permissions in Experience Platform Launch. See the [User Permissions](https://docs.adobe.com/content/help/en/launch/using/reference/admin/user-permissions.html) article in the Experience Platform Launch documentation for more details.
{% endhint %}

1. Create an Edge configuration - The Edge configuration contains settings for Adobe solutions and services and is setup server-side \(instead of client-side\). The Edge configuration is identified to the Mobile SDK by edgeConfigId \(via the Edge Network Extension\).
2. Setting up a mobile property - As previously done, users will need to create and setup a mobile property and add the Adobe Experience Platform Edge Network extension \(and other extensions as needed\) to obtain install instructions and the client environment ID.

To create a new Edge Configuration follow the steps below:

1. In the browser, navigate to [Adobe Experience Platform Launch](https://experience.adobe.com/launch) and login with your credentials.
2. From the left panel, choose **Edge Configuration** from the dropdown \(instead of **Client Side**\).
3. Click **New Edge Configuration** \(located on top right\)
4. Set a name for the configuration and click **Save**.

![Creating an Edge Configuration in Adobe Experience Platform Launch](../.gitbook/assets/screen-shot-2021-02-02-at-12.42.57-pm%20%281%29.png)

1. In the next screen, toggle on **Adobe Experience Platform** and:
   1. Select the appropriate **Sandbox** from the dropdown
   2. Choose the appropriate **Event Dataset** as previously created
2. Once you have made your selections click `Save`.

![Configuring your Edge Configuration in Adobe Experience Platform Launch](../.gitbook/assets/screen-shot-2021-02-02-at-12.44.31-pm.png)

In the resulting summary screen, you will see that three environments have been created for your Edge Configuration. If needed, each environment can be edited individually with different configuration parameters.

Make note of the listed, Launch Edge Configuration **Environment ID**s, as these values will be referenced when you setup the mobile property in the next step.

![Environment IDs for your Edge Configuration](../.gitbook/assets/screen-shot-2021-02-02-at-12.45.55-pm.png)

For additional information on Edge Configurations in Experience Platform Launch, see the [reference guide](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/edge-configuration.html).

