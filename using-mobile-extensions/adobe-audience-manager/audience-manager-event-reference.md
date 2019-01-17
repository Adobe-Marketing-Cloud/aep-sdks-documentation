# Audience Manager event reference

## Events Handled

### Audience Manager Content Request

This event updates the profile for Audience Manager and is generated when the`audienceSignalWithData` API is called to send content to Audience Manager.

#### Event Details

| **Event Type** | **Event Source** | **Paired** | **Paired Event** |
| :--- | :--- | :--- | :--- |
| com.adobe.eventType.audienceManager | com.adobe.eventSource.requestContent | Yes | ​[Audience Manager Content Response](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/adobe-audience-manager/events-dispatched-by-adobe-audience-manager#audience-manager-content-response)​ |

#### Data Payload Definition

Here are the key-value pairs in this event:

| **Key or Key Type** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| aamtraits | String Map | No | The data payload will contain the traits \(key-value pairs\) that were sent by the customer. |

### Audience Manager Identity Request

This event is a request to retrieve the visitor profile from Audience Manager and is generated when the parent application requests audience visitor profile by using the public interface`audienceGetVisitorProfile`

#### Event Details

| Event Type | Event Source | Paired | Paired Event |
| :--- | :--- | :--- | :--- |
| com.adobe.eventType.audienceManager | com.adobe.eventSource.requestIdentity | Yes | ​[Audience Manager Identity Response](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/adobe-audience-manager/events-dispatched-by-adobe-audience-manager#audience-manager-identity-response)​ |

#### Data Payload Definition

There are no key-value pair for this event:

### Audience Manager Reset Request

This event clears the Audience Manager profile on the device and is generated when the `audienceReset` API is called to clear the Audience Manager profile.

#### Event Details

| Event Type | Event Source | Paired | Paired Event |
| :--- | :--- | :--- | :--- |
| com.adobe.eventType.audienceManager | com.adobe.eventSource.requestReset | No | N/A |

#### Data Payload Definition

There are no key-value pairs in this event.

#### Hub Shared State

Audience extension listens for the Configuration Shared State events.

For more details about the Shared State events, see [Events Dispatched by SDK Core - Hub Shared State](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/sdk-core/events-dispatched-by-sdk-core#hub-shared-state)​

### Configuration Content Response

The Audience Manager extension listens for Configuration Content Response events to detect whether the privacy status was changed or the audience configuration was updated.

For more details about the this event, see [Events Dispatched by SDK Core - Configuration Response Content](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/sdk-core/events-dispatched-by-sdk-core#configuration-response-content)​

### Lifecycle Content Response

The Audience Manager extension listens for the Lifecycle Content Response event that is generated when there is a lifecycle session update such as a launch event, upgrade, and so on, and sends a new signal to Audience Manager with the lifecycle context data.

For more details about the this event, see [Events Dispatched by Lifecycle - Lifecycle Response Content](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/lifecycle/events-dispatched-by-lifecycle#lifecycle-data-content-response).

### Analytics Content Response

Audience Manager listens for Analytics Response events, which are sent when audience forwarding is enabled, processes the events, and extracts the destinations where the new signals will be sent.

For more details about this event, see [Events Dispatched by Analytics - Analytics Response Content](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/adobe-analytics/events-dispatched-by-adobe-analytics#analytics-content-response).



## Events Dispatched <a id="audience-manager-content-response"></a>

### Audience Manager Content Response

The purpose of this event is to:

* Deliver the Audience Manager profile to the original requester.
* Deliver the Audience Manager profile to any module that might be listening for updates.

The event is generated in the following scenarios:

* When a request is made to update the Audience manager profile.
* When a request is made to retrieve the current Audience manager profile.

#### Event Details

| **Event Type** | **Event Source** | **Paired** | **Paired Event** |
| :--- | :--- | :--- | :--- |
| com.adobe.eventType.audienceManager | com.adobe.eventSource.responseContent | Yes | ​[Audience Manager Content Request](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/adobe-audience-manager/events-handled-by-adobe-audience-manager#audience-manager-content-request)​ |

#### Data Payload Definition

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| aamprofile | String Map | Yes | The Data payload will contain the Customer key value pairs. The Data Payload will be populated using the CV and CN values in the Audience Manager Stuff array. |

### Audience Manager Identity Response

The purpose of this event is to:

* Deliver the Audience Manager profile to the original requester.
* Deliver the Audience Manager profile to any module that might be listening for updates.

The event is generated in the following scenarios:

* When a request is made to update the Audience manager profile.

#### Event Details

| **Event Type** | **Event Source** | **Paired** | **Paired Event** |
| :--- | :--- | :--- | :--- |
| com.adobe.eventType.audienceManager | com.adobe.eventSource.responseIdentity | Yes | ​[Audience Manager Identity Request](https://docs.adobelaunch.com/extension-reference/mobile/build-your-own-extension/events/adobe-audience-manager/events-handled-by-adobe-audience-manager#audience-manager-identity-request)​ |

#### Data Payload Definition

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| aamprofile | String Map | No | Audience Manager Visitor Profile |

## Shared States

MODULE\_NAME: `com.adobe.module.audience`

Shared state for this module is updated on the following occasions:

* **On Initialization:** After the module is initialized, it will update the shared state by reading the previously set value from persistence.
* **On Audience Public API Calls:** The Shared stare is updated when the `submitsignal` API is called.

| Key | Type | Description |
| :--- | :--- | :--- |
| uuid | String | The UUID assigned by the Audience server |
| aamprofile | Dictionary/Map | The matching visitor profile segments associated with the user |

