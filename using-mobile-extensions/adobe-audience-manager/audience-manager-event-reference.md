# Audience Manager event reference

## Events handled

### Audience Manager Content Request

This event updates the profile for Audience Manager and is generated when the`audienceSignalWithData` API is called to send content to Audience Manager.

#### Event details

| **Event Type** | **Event Source** | **Paired** | **Paired Event** |
| :--- | :--- | :--- | :--- |
| `com.adobe.eventType.audienceManager` | `com.adobe.eventSource.requestContent` | Yes | ​[Audience Manager Content Response](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/adobe-audience-manager/events-dispatched-by-adobe-audience-manager#audience-manager-content-response)​ |

#### Data payload definition

Here are the key-value pairs in this event:

| **Key or Key Type** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `aamtraits` | String Map | No | The data payload contains the traits \(key-value pairs\) that were sent by the customer. |

### Audience Manager Identity Request

This event is a request to retrieve the visitor profile from Audience Manager and is generated when the parent application requests an audience visitor profile by using `audienceGetVisitorProfile`.

#### Event details

| Event Type | Event Source | Paired | Paired Event |
| :--- | :--- | :--- | :--- |
| `com.adobe.eventType.audienceManager` | `com.adobe.eventSource.requestIdentity` | Yes | ​[Audience Manager Identity Response](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/adobe-audience-manager/events-dispatched-by-adobe-audience-manager#audience-manager-identity-response)​ |

#### Data payload definition

There are no key-value pair for this event:

### Audience Manager Reset Request

This event clears the Audience Manager profile on the device and is generated when the `audienceReset` API is called to clear the Audience Manager profile.

#### Event details

| Event Type | Event Source | Paired | Paired Event |
| :--- | :--- | :--- | :--- |
| `com.adobe.eventType.audienceManager` | `com.adobe.eventSource.requestReset` | No | N/A |

#### Data payload definition

There are no key-value pairs in this event.

#### Hub shared state

Audience Manager listens for the configuration shared state events. For more information about shared state events, see [Shared states and events](https://aep-sdks.gitbook.io/docs/resources/building-mobile-extensions/shared-states-and-events).​

### Configuration Response Content

The Audience Manager extension listens for Configuration Content Response events to detect whether the privacy status was changed or the audience configuration was updated.

For more information about the this event, see [Configuration Response Content](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-event-reference#configuration-response-content)​.

### Lifecycle Response Content

This event is generated when there is a lifecycle session update such as a launch event, upgrade, and so on. The Audience Manager extension listens for the event and sends a new signal to Audience Manager with the lifecycle context data.

For more information about the this event, see [Lifecycle Response Content](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-event-reference#lifecycle-response-content).

### Analytics Response Content

Audience Manager listens for Analytics Response events, which are sent when audience forwarding is enabled, processes the events, and extracts the destinations where the new signals will be sent.

For more information about this event, see [Analytics Response Content](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics/analytics-event-reference#analytics-response-content).

## Events dispatched  <a id="audience-manager-content-response"></a>

### Audience Manager Content Response

The purpose of this event is to deliver the Audience Manager profile to the following:

* The original requester.
* A module that might be listening for updates.

The event is generated when a request is made to:

* Update the Audience manager profile.
* Retrieve the current Audience manager profile.

#### Event details

| **Event Type** | **Event Source** | **Paired** | **Paired Event** |
| :--- | :--- | :--- | :--- |
| `com.adobe.eventType.audienceManager` | `com.adobe.eventSource.responseContent` | Yes | ​[Audience Manager Content Request](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/adobe-audience-manager/events-handled-by-adobe-audience-manager#audience-manager-content-request)​ |

#### Data payload definition

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `aamprofile` | String Map | Yes | The Data payload contains the Customer key value pairs. The Data Payload is populated using the CV and CN values in the Audience Manager Stuff array. |

### Audience Manager Identity Response

The purpose of this event is to deliver the Audience Manager profile to:

* The original requester.
* Any module that might be listening for updates.

The event is generated when a request is made to update the Audience manager profile.

#### Event details

| **Event Type** | **Event Source** | **Paired** | **Paired Event** |
| :--- | :--- | :--- | :--- |
| `com.adobe.eventType.audienceManager` | `com.adobe.eventSource.responseIdentity` | Yes | ​[Audience Manager Identity Request](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/adobe-audience-manager/events-handled-by-adobe-audience-manager#audience-manager-identity-request)​ |

#### Data payload definition

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `aamprofile` | String Map | No | Audience Manager Visitor Profile |

## Shared states

MODULE\_NAME: `com.adobe.module.audience`

The shared state for this module is updated in the following scenarios:

* At Initialization After the module is initialized, it updates the shared state by reading the previously set value from persistence.
* With Audience Manager API calls The shared stare is updated when the `submitsignal` API is called.

| Key | Type | Description |
| :--- | :--- | :--- |
| `uuid` | String | The UUID assigned by the Audience server. |
| `aamprofile` | Dictionary/Map | The matching visitor profile segments associated with the user. |

