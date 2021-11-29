# Adobe Analytics

## Configure the Analytics extension in Adobe Experience Platform Launch

1. In Experience Platform Launch, click the **Extensions** tab.
2. On the **Catalog** tab, locate the **Adobe Analytics** extension, and click **Install**.
3. Type the extension settings. For more information, please read the [configure the Analytics Extension section](./#configure-the-analytics-extension).
4. Click **Save**.
5. Follow the publishing process to update SDK configuration.

![Workflow overview for Experience Platform Launch, the Mobile SDK, and Adobe Analytics](../../.gitbook/assets/group-7.png)

### Configure the Analytics extension

![Adobe Analytics Extension Configuration](../../.gitbook/assets/mobile-analytics-configuration.png)

#### Analytics company

![Adobe Analytics Company](../../.gitbook/assets/mobile-analytics-company.png)

If you have access to more than one Analytics company, a select menu will appear, allowing you to choose which company you want to use. If you only have access to one Analytics company, this select menu will not appear.

Once you select an Analytics company, the list of report suites associated with that company will appear in the report suites section.

#### Report suites

{% hint style="info" %}
To learn how to find report suite IDs, please read the documentation on [report suites](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/report-suites-admin.html).
{% endhint %}

Select one or more mobile-enabled report suite identifiers from the combo box to which the Analytics data should be sent. Only report suite identifiers that belong to a company and that are enabled for mobile can be selected. For information on how to enable mobile for your report suite, see the [mobile management documentation](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/mobile-management.html).

To narrow the search for a report suite identifier, type a string in the combo box text field. After a valid report suite identifier has been selected, this identifier appears in a tag below the combo box. To remove a report suite ID, click on the X next to the ID you want to remove. Report suite IDs can also be configured for the Development and Staging environments.

#### Tracking server

{% hint style="info" %}
To learn what a tracking server is and how to find it, please read the documentation on [tracking servers](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackingserver.html).
{% endhint %}

The tracking server is the tracking domain that all the Analytics requests should be made.

#### **Offline enabled**

{% hint style="info" %}
To learn more about offline tracking, please read the documentation on [offline tracking](https://experienceleague.adobe.com/docs/analytics/implementation/vars/config-vars/trackoffline.html).
{% endhint %}

When the **Offline Enabled** checkbox is selected, Analytics hits are queued when your device is offline and are sent later when your device is back online. To use offline tracking, ensure that your report suite is timestamp enabled.

{% hint style="danger" %}
If your report suite is timestamp enabled, the checkbox must be selected. If your report suite is not timestamped enabled, leave the checkbox unselected. If this setting is not configured correctly, data will be lost.

If you are not sure whether your report suite is timestamp enabled, contact Customer Care.
{% endhint %}

{% hint style="info" %}
If you currently send Mobile SDK data to a report suite that also collects data from web JavaScript, you may need to set up a separate report suite for mobile data or include a custom timestamp on all JavaScript hits that use the `s.timestamp` variable. For more information, please contact Customer Care.
{% endhint %}

#### Audience Manager forwarding

{% hint style="info" %}
For more information about Analytics server-side forwarding to Audience Manager, see the documentation on [Analytics sever-side forwarding](./#server-side-forwarding-with-audience-manager).
{% endhint %}

If you set up Analytics server-side forwarding to Audience Manager, select the **Audience Manager Forwarding** checkbox. When this checkbox is selected, all SDK requests to Analytics servers are sent with an expected response code of **10**. This step ensures that Analytics traffic is forwarded to Audience Manager and that the Audience Manager User Profile is correctly updated in the SDK.

#### Backdate previous session info

{% hint style="warning" %}
Select the **Backdate Previous Session Info** checkbox **only** if you have timestamp-enabled report report suites.
{% endhint %}

When you select this checkbox, the SDK backdates the end-of-session lifecycle information so that this information can be attributed into its correct session. Session information currently consists of crashes and session length.

The SDK also backdates the session information hit to one second after the last hit of the previous session. This means that crashes and session data will correlate with the correct date on which they occurred. One hit is backdated each time a new launch of the application is occurs.

For example, if you select the checkbox, Lifecycle session information or crash events are backdated to one second after the last hit was sent. If you do not select the checkbox, Lifecycle data is attached to the first hit of the subsequent session.

If this option is disabled, Mobile SDK attaches the session information to the current lifecycle.

#### Batch limit

This setting creates a threshold number of hits to be sent in consecutive calls. For example, if you type or select "10", each Analytics hit before the 10th hit is stored in the queue. When the 10th hit comes in, all 10 hits are sent to Analytics in the order in which they were generated.

{% hint style="info" %}
If you set a value greater than 0, ensure that the **Offline Enabled** checkbox is also selected.
{% endhint %}

The default value for this setting is 0, which means that hit batching is disabled, and all hits are immediately sent to Analytics as they are generated.

#### Launch hit delay

The number of seconds to wait before Analytics launch hits are sent from the SDK. Ensure that this setting is set at 5 seconds or greater when using acquisition functionality from the [Mobile Services](../adobe-analytics-mobile-services/) extension.

## Add Analytics to your application

{% tabs %}
{% tab title="Android" %}
### Java

1. Add the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) and Analytics extensions to your project using the app's Gradle file.

   ```java
    implementation 'com.adobe.marketing.mobile:sdk-core:1.+'
    implementation 'com.adobe.marketing.mobile:analytics:1.+'
   ```

2. Import the Analytics extension in your application's main activity.

   ```java
    import com.adobe.marketing.mobile.*;
   ```
{% endtab %}
{% endtabs %}

## Register Analytics with Mobile Core

{% tabs %}
{% tab title="Android" %}
### Java

The following sample shows how to set up methods that call the [setApplication\(\)](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#setapplication) method in the `onCreate()` method:

```java
public class MobileApp extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.configureWithAppID("yourAppId");
        try {
            Analytics.registerExtension(); //Register Analytics with Mobile Core
            Identity.registerExtension();
            MobileCore.start(null);
        } catch (Exception e) {
            //Log the exception
         }
    }
}
```

{% hint style="info" %}
Analytics depends on the Identity extension and is automatically included in Core by Maven. When manually installing the Analytics extension, ensure that you add the `identity-1.x.x.aar` library to your project.
{% endhint %}
{% endtab %}
{% endtabs %}

## Send Lifecycle metrics to Analytics

To automatically report on the application lifecycle details in Analytics, ensure that you properly configure the lifecycle data collection. For more information, see the documentation on [Lifecycle metrics](../../foundation-extensions/mobile-core/lifecycle/).

## Send app states and actions to Analytics

To track mobile app states and actions in Adobe Analytics, implement the [trackAction](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#trackaction) and [trackState](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#trackstate) APIs from the Mobile Core extension. For more information, see the [track app actions](../../foundation-extensions/mobile-core/mobile-core-api-reference.md#track-app-actions) and [track app states](../../foundation-extensions/mobile-core/mobile-core-api-reference.md#track-app-states-and-views) tutorials.

{% hint style="info" %}
[trackState](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#trackstate) reports the view state as the **Page Name**, and state views are reported as **Page View** in Analytics. The value is sent to Analytics by using the page name variable \(`pagename=value`\).

[trackAction](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/mobile-core-api-reference#trackaction) reports the Action as an **event** and does not increment your page views in Analytics. The value is sent to Analytics by using the action variable \(`action=value`\).
{% endhint %}

## Integrations with Adobe Experience Platform solutions and services

### Analytics for Adobe Target \(A4T\)

To see the performance of your Target activities for some segments, you can set up the Analytics extension for Target \(A4T\) cross-solution integration by enabling the A4T campaigns. This integration allows you to use Analytics reports to examine your results. If you use Analytics as the reporting source for an activity, all reporting and segmentation for that activity is based on Analytics data collection. For more information, see [Target](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html).

### Server-side forwarding with Audience Manager

To enable the ability to share Analytics data with Audience Manager, in the Experience Platform Launch UI, select the **Audience Manager Forwarding** checkbox. For more information, go to [Audience Manager](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-audience-manager).

### Audio and video analytics

For more information about collecting audio and video analytics, please read the documentation on [Media Analytics for audio and video](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/).

## Event serialization

Event serialization is not supported by processing rules. To set serialized events directly on the hits sent to Analytics, use the following syntax in context data parameters:

{% tabs %}
{% tab title="Android" %}
### Java

**Syntax**

```java
cdata.put("&&events", "event1:12341234");
```

**Example**

```java
//create a context data dictionary
HashMap cdata = new HashMap<String, Object>();

// add events
cdata.put("&&events", "event1:12341234");

// send a tracking call - use either a trackAction or TrackState call.
// trackAction example:
MobileCore.trackAction("Action Name", cdata);
// trackState example:
MobileCore.trackState("State Name", cdata);
```
{% endtab %}
{% endtabs %}

The following video shows you how to use [trackState](../../foundation-extensions/mobile-core/mobile-core-api-reference.md#track-app-states-and-views) APIs to send data to Adobe Analytics.

{% embed url="https://video.tv.adobe.com/v/26260/?quality=12" caption="" %}

## Configuration keys

To update the SDK configuration programmatically, use the following information to change your Analytics configuration values.

| Key | Required | Description | Data Type |
| :--- | :--- | :--- | :--- |
| analytics.server | Yes | See [Tracking Server](./#tracking-server) | String |
| analytics.rsids | Yes | See [Report Suites](./#report-suites). Multiple report suite IDs can be comma separated with no space in- between. For example: "rsids" : "rsid" "rsids" : "rsid1,rsid2" | String |
| analytics.batchLimit | No | See [Batch Limit](./#batch-limit) | Integer |
| analytics.aamForwardingEnabled | No | See [Audience Manager Forwarding](./#audience-manager-forwarding) | Boolean |
| analytics.offlineEnabled | No | See [Offline Enabled](./#offline-enabled) | Boolean |
| analytics.backdatePreviousSessionInfo | No | See [Backdate Previous Session Info](./#backdate-previous-session-info). | Boolean |

### Update Analytics configuration

{% tabs %}
{% tab title="Android" %}
#### Java

**Example**

```java
HashMap<String, Object> data = new HashMap<String, Object>();
data.put("analytics.server", "sample.analytics.tracking.server");
data.put("analytics.rsids", "rsid1,rsid2");
data.put("analytics.batchLimit", 10);
data.put("analytics.offlineEnabled", true);

MobileCore.updateConfiguration(data);
```
{% endtab %}
{% endtabs %}

For more information, see the [configuration API reference](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration/configuration-api-reference).

