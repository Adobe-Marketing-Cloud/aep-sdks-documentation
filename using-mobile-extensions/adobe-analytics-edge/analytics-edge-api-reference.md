# Analytics Edge API reference

{% hint style="warning" %}
The AEP Analytics Edge mobile extension is currently in BETA. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more.
{% endhint %}

The `trackAction` API documentation can be seen at [trackAction.](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/251c4c8375daded0e48c732d8ae80925e919a201/using-mobile-extensions/mobile-core/mobile-core-api-reference/README.md#track-app-actions)

The `trackState` API documentation can be seen at [trackState.](https://github.com/Adobe-Marketing-Cloud/aep-sdks-documentation/tree/251c4c8375daded0e48c732d8ae80925e919a201/using-mobile-extensions/mobile-core/mobile-core-api-reference/README.md#track-app-states-and-views)

## Unsupported API

If you are migrating from the Analytics to Analytics Edge extension, the following API are are no longer supported:

| Analytics API | Details |
| :--- | :--- |
| clearQueue getQueueSize sendQueuedHits | The events batching and queuing are no longer supported in Analytics Edge as the hits are sent as soon as a network connection is available on the device. |
| getTrackingIdentifier | If you used AID in your previous implementations, the SDK will continue to read it and send it to Experience Edge; for new users the recommended unique identifier is the [ECID](../mobile-core/identity/#visitor-tracking-between-an-app-and-the-mobile-web). |
| getVisitorIdentifier setVisitorIdentifier | If you used VID in your previous implementations, the SDK will continue to read it and send it to Experience Edge; for new users the recommended unique identifier is the [ECID](../mobile-core/identity/#visitor-tracking-between-an-app-and-the-mobile-web). |

