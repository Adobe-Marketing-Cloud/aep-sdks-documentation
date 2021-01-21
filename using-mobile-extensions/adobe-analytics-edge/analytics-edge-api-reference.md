# Analytics Edge API reference

{% hint style="warning" %}

The AEP Analytics Edge mobile extension is currently in BETA. Use of this extension is by invitation only. Please contact your Adobe Customer Success Manager to learn more.

{% endhint %}

## trackAction

To track mobile app actions in Adobe Analytics, implement the `trackAction` APIs from the Mobile Core extension. For more information, see [Track app actions](../mobile-core/mobile-core-api-reference.md#track-app-actions).

{% hint style="info" %}
`trackAction` reports the Action as an **event** and does not increment your page views in Analytics. The value is sent to Analytics by using the action variable \(`action=value`\).
{% endhint %}

{% tabs %}
{% tab title="Android" %}

#### Java

```java
// create a context data dictionary
Map<String, String> additionalContextData = new HashMap<>();
                                          
// add data
additionalContextData.put("exampleCustomKey", "exampleValue");

// send a tracking call
MobileCore.trackAction("Action Name", additionalContextData);
```

{% endtab %}

{% tab title="iOS" %}

#### Objective C

```objectivec
// create a context data dictionary
NSMutableDictionary *additionalContextData = [NSMutableDictionary dictionary];

// add data
[additionalContextData setObject:@"key" forKey:@"value"];

// send the tracking call
[AEPMobileCore trackAction:@"Action Name" data:additionalContextData];
```

#### Swift

```swift
// create a context data dictionary
let additionalContextData = ["key":"value"]

// send the trackAction call.
MobileCore.track(action: "Action Name", data: additionalContextData)
```

{% endtab %}
{% endtabs %}

## trackState

To track mobile app states in Adobe Analytics, implement the `trackState` APIs from the Mobile Core extension. For more information, see [Track app states](../mobile-core/mobile-core-api-reference.md#track-app-states-and-views).

{% hint style="info" %}
`trackState` reports the View State as **Page Name**, and state views are reported as **Page View** in Analytics. The value is sent to Analytics by using the page name variable \(`pagename=value`\).
{% endhint %}

{% tabs %}
{% tab title="Android" %}

#### Java

```java
// create a context data dictionary
Map<String, String> additionalContextData = new HashMap<>();
                                          
// add data
additionalContextData.put("exampleCustomKey", "exampleValue");

// send a tracking call
MobileCore.trackState("State Name", additionalContextData);
```

{% endtab %}

{% tab title="iOS" %}

#### Objective C

```objectivec
// create a context data dictionary
NSMutableDictionary *additionalContextData = [NSMutableDictionary dictionary];

// add data
[additionalContextData setObject:@"key" forKey:@"value"];

// send the tracking call
[AEPMobileCore trackState:@"State Name" data:additionalContextData];
```

#### Swift

```swift
// create a context data dictionary
let additionalContextData = ["key":"value"]

// send the trackState call.
MobileCore.track(state: "State Name", data: additionalContextData)
```

{% endtab %}
{% endtabs %}

## Unsupported API

If you are migrating from the Analytics to Analytics Edge extension, the following API are are no longer supported:

| Analytics API                                    | Details                                                      |
| ------------------------------------------------ | ------------------------------------------------------------ |
| clearQueue<br />getQueueSize<br />sendQueuedHits | The events batching and queuing are no longer supported in Analytics Edge as the hits are sent as soon as a network connection is available on the device. |
| getTrackingIdentifier                            | If you used AID in your previous implementations, the SDK will continue to read it and send it to Experience Edge; for new users the recommended unique identifier is the [ECID](../mobile-core/identity#visitor-tracking-between-an-app-and-the-mobile-web). |
| getVisitorIdentifier<br />setVisitorIdentifier   | If you used VID in your previous implementations, the SDK will continue to read it and send it to Experience Edge; for new users the recommended unique identifier is the [ECID](../mobile-core/identity#visitor-tracking-between-an-app-and-the-mobile-web). |

