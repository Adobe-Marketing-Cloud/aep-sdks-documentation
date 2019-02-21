# Adobe Campaign Standard event reference

## Events handled

### Campaign Request Content  <a id="configuration-response-content"></a>

TThis event is a request to processes (shows) messages provided in the event data.

#### Data payload definition  <a id="data-payload-definition-1"></a>

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |

### EventHub Shared State  <a id="eventhub-shared-state"></a>



#### Data payload definition  <a id="data-payload-definition-2"></a>

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |

### Configuration Response Content  <a id="configuration-response-content"></a>

The data property in this event is used by each extension to modify its current settings. Each extension is responsible for reading out the part of the data property for which it is concerned.

#### Data payload definition  <a id="data-payload-definition-3"></a>

The Adobe Campaign Standard extension will read the following key from the configuration event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `__dev__campaign.server` | String | Yes | This contains the endpoint URL for the development environment Adobe Campaign Standard instance |
| `__dev__campaign.pkey` | String | Yes | This contains the identifier for a mobile app configured in development environment Adobe Campaign Standard |
| `__stage__campaign.server` | String | Yes | This contains the endpoint URL for the stage environment Adobe Campaign Standard instance |
| `__stage__campaign.pkey` | String | Yes | This contains the identifier for a mobile app configured in stage environment Adobe Campaign Standard |
| `campaign.server` | String | Yes | This contains the endpoint URL for the production environment Adobe Campaign Standard instance |
| `campaign.pkey` | String | Yes | This contains the identifier for a mobile app configured in production environment Adobe Campaign Standard |
| `campaign.mcias` | String | Yes | This contains the in-app messaging service URL endpoint |
| `campaign.timeout` | String | Yes | This contains the amount of time to wait for a response from in-app messaging service |
| `global.privacy` | Boolean | Yes | This contains the mobile privacy status settings |

{% hint style="info" %}
If `global.privacy` is changed to **optout**, linkage fields will be reset. All downloaded messages and rules will be erased.
{% endhint %}

### Request Identity  <a id="request-identity"></a>

This event is a request to set linkage fields from event data. The linkage fields are required to download personalized in-app messages.

#### Data payload definition  <a id="data-payload-definition-4"></a>

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |

### Request Reset  <a id="request-reset"></a>

This event is a request to reset the linkage fields. When the linkage fields are reset, all cached messages and rules will be erased.

#### Data payload definition  <a id="data-payload-definition-5"></a>

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |


### Lifecycle Response Content  <a id="lifecycle-response-content"></a>



#### Data payload definition  <a id="data-payload-definition-6"></a>

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |


## Events dispatched

### Campaign Response Content
This event is a response from the Adobe Campaign Standard extension contains the message interaction details (Viewed, Triggered or Clicked). 

#### Event details

| **Event Type** | **Event Source** | **Paired** |
| :--- | :--- | :--- |
| `com.adobe.eventType.campaign` | `com.adobe.eventSource.responseContent` | Yes |

#### Data payload definition


#### Event data example



