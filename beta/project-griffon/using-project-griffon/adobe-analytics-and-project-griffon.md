# Adobe Analytics

## Overview

The integration with Adobe Analytics provides a richer view of SDK events to users debugging and validating their Adobe Analytics implementation. The view now shows lifecycle and action/state events sent to Adobe Analytics from the [Adobe Experience Platform SDK](../../../using-mobile-extensions/adobe-analytics/). The view also features "response" detail that provides information on how the events were processed after the application of each respective report suite's processing rules.

![](../../../.gitbook/assets/aa-loop.gif)

### Post-processed status

After the SDK makes a network request with Adobe Analytics, the status will tell you if Griffon was able to retrieve the post-processing information for the Adobe Analytics request.

| Status | Description |
| :--- | :--- |
| `Queued` | The network request is fetching the post-processing information. |
| `Processed` | The network request was successful, and the post-processing information is received. |
| `Delayed` | The maximum number of requests retries to fetch the post-processing information has been exceeded. |
| `Error` | An error caused the network request to fail. More details about the error are displayed in the event details view. |
| `Unauthorized` | The user does not have access to the Adobe Analytics report suite. |
| `Unavailable` | The Adobe Analytics request does not have a corresponding `AnalyticsResponse` event. |
| `No Debug Flag` | The current Adobe Analytics or Assurance SDK version might not support the Analytics Debugging feature. For more information, please read the [Troubleshooting guide](../troubleshoot-project-griffon.md#Adobe Analytics Debugging). |
| `Expired` | The `AnalyticsTrack` or `LifecycleStart` event is older than 24 hours. |

### Event details view

For an Analytics track event, the detailed view contains the following valuable parts:

* An originating SDK Analytics request event.
* OOTB meta and context data from the request, such as report suite ID, SDK extension versions, OOTB context data, and so on.
* Post-processed information on the Analytics event that contains the mapping of revars, evars, props, and so on.

## Using Project Griffon for Adobe Analytics

To get started, complete the following steps:

1. Ensure that you implemented the latest versions of the [Project Griffon](../set-up-project-griffon.md) and [Adobe Analytics](../../../using-mobile-extensions/adobe-analytics/) extensions.
2. Go to [https://experience.adobe.com/griffon](https://experience.adobe.com/griffon) \(**not** griffon.adobe.com\).
3. Connect your app to a Project Griffon session. For more information, see [Connect your device](https://app.gitbook.com/@aep-sdks/s/docs/beta/project-griffon/using-project-griffon#2-connect-your-device).
4. To view your events, select the **Adobe Analytics** view.

![](../../../.gitbook/assets/screen-shot-2020-01-13-at-12.04.14-pm.png)

