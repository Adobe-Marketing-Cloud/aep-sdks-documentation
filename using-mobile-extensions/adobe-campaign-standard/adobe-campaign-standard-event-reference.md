# Adobe Campaign Standard event reference

## Events handled

The following events are handled by the Adobe Campaign Standard extension:

### Campaign request

The Campaign request event is dispatched from the Event Hub when a Campaign rule is found to be true. For example, after the user launches the app, the "User has launched the app" rule will be true. A triggered consequences event is dispatched, which contains the data of the displayed local, alert, or full-screen message.

#### Payload definition

The following key-value pairs are present in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `triggeredconsequence` | Map | No | The triggered Campaign rule consequence. |

#### Example

The following example shows triggered consequence data.

```json
{
  "triggeredconsequence": {
    "assetsPath": "assets/path/",
    "id": "123",
    "detail": {
      "template": "local",
      "wait": 0,
      "userData": {
        "deliveryId": "123abc",
        "broadlogId": "456edf"
      },
      "title": "local example",
      "content": "local example text"
    },
    "type": "iam"
  }
}
```

### Configuration response

The data property in the configuration response event is used by each extension to modify its current settings. Each extension is responsible for parsing the relevant part of the data property.

#### Payload definition

The following key value pairs are supported for Adobe Campaign Standard extension when reading from the configuration event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `__dev__campaign.server` | String | Yes | This contains the endpoint URL for the development environment in the Adobe Campaign Standard instance. |
| `__dev__campaign.pkey` | String | Yes | This contains the identifier for a mobile app that was configured in the development environment in Adobe Campaign Standard. |
| `__stage__campaign.server` | String | Yes | This contains the endpoint URL for the staging environment in the Adobe Campaign Standard instance. |
| `__stage__campaign.pkey` | String | Yes | This contains the identifier for a mobile app that was configured in the staging environment in Adobe Campaign Standard. |
| `campaign.server` | String | No | This contains the endpoint URL for the production environment in the Adobe Campaign Standard instance. |
| `campaign.pkey` | String | No | This contains the identifier for a mobile app that was configured in the production environment in Adobe Campaign Standard. |
| `campaign.mcias` | String | No | This contains the in-app messaging service URL endpoint. |
| `campaign.timeout` | Integer | No | This contains the amount of time to wait for a response from the in-app messaging service. |
| `global.privacy` | Boolean | Yes | This contains the mobile privacy status settings. |
| `campaign.registrationDelay` | Integer | Yes | This contains the number of days to delay the sending of the next Adobe Campaign Standard registration request. |
| `campaign.registrationPaused` | Boolean | Yes | This contains the Adobe Campaign Standard registration request paused status. |

{% hint style="info" %}
After `global.privacy` is changed to **optout**, the linkage fields are reset. All downloaded messages and rules are erased, and no tracking request can leave the device.
{% endhint %}

{% hint style="danger" %}
The configuration setting to pause registration requests is provided for specific use cases only. The use of this configuration setting should be avoided when possible.
{% endhint %}

#### Example

```json
{
    "global.privacy":"optedin",
    "campaign.timeout":1,
    "campaign.mcias":"mcias-va7.cloud.adobe.io/mcias",
    "__dev__campaign.pkey":"",
    "__stage__campaign.pkey":"",
    "campaign.pkey":"",
    "__dev__campaign.server":"mcias.campaign-demo.adobe.com",
    "__stage__campaign.server":"mcias.campaign-demo.adobe.com",
    "campaign.server":"mcias.campaign-demo.adobe.com"
}
```

### Request identity

The request identity event is dispatched by the API to set linkageFields, which sets the linkage fields. It is used to download personalized in-app messages.

#### Payload definition

The following key-value pairs are supported in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `linkagefields` | Map | No | This map contains at least one of the linkage fields that are used to personally identify the logged in user. |

#### Example

```json
{ 
    "linkagefields": 
    { 
        "firstName":"john", 
        "lastName":"doe", 
        "age":30
    }
}
```

### Request reset

The request reset event is dispatched when users no longer want to use personalized in-app messages. After this event is received, Adobe Campaign Standard deletes all personalized messages and will only download generic messages.

#### Data payload

This event has no event data.

### Lifecycle response

The lifecycle response event is a response from the Lifecycle extension that notifies a client or extension about lifecycle context data in which the client or extension might be interested. The event is generated by the Lifecycle extension, and the API is called after a lifecycle start, stop, or pause.

#### Payload definition

The following key-value pairs are used in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `lifecyclecontextdata` | Map | No | The map that contains the stored lifecycle metrics. |

#### Example

```json
{    "lifecyclecontextdata": 
    {
        "installdate":"22/05/2014",        
        "hourofday":6,        
        "dayofweek":2,        
        "osversion":"iOS 12.3",        
        "appID":"contextDataValue",        
        "resolution":"600x1345",        
        "devicename":"iPhoneX",        
        "launchevent":"LaunchEvent",        
        "prevsessionlength":345,        
        "locale":"en-US",        
        "runmode":"Application",        
        "launches":42    
    },    
    "starttimestampmillis" :44,    
    "maxsessionlength":22
}
```

### Generic data OS

The generic data OS event is dispatched by the Core extension to the Event Hub when the `collectMessageInfo` API is invoked by the app developer to track local and push notification interactions.

#### Payload definition 

The following key-value pairs are used in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `deliveryId` | String | No | The string that contains the delivery ID of the message for which there were interactions. |
| `action` | String | No | The string that contains the message interaction ID. |
| `broadlogId` | String | No | The string that contains the broadlog ID of the message for which there were interactions. |

#### Event data example

```json
{
    "deliveryId": "1442de4",
    "action": "2",
    "broadlogId": "h1c1380"
}
```

## Events dispatched

The following events are dispatched by the Campaign Standard extension:

### Campaign response

The Campaign response event is a response from the Adobe Campaign Standard extension and contains the message interaction details: Viewed, Triggered or Clicked.

#### Event details

| **Event Type** | **Event Source** | **Paired** |
| :--- | :--- | :--- |
| `com.adobe.eventType.campaign` | `com.adobe.eventSource.responseContent` | Yes |

#### Payload definition

The following key-value pairs are used in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `a.message.id` | String | No | The message ID of the message that was triggered. |
| `a.message.triggered` | String ("1") | No | A flag that specifies a message triggered event. Only one type of message interaction exists in each Campaign response content event. |
| `a.message.viewed` | String ("1") | No | A flag that specifies a message viewed event. |
| `a.message.clicked` | String ("1") | No | A flag that specifies a message clicked event. |

#### Event data example

```json
{ "a.message.id": "12345678", "a.message.triggered": "1" }
{ "a.message.id": "12345678", "a.message.viewed": "1" }
{ "a.message.id": "12345678", "a.message.clicked": "1" }
```

