# Adobe Campaign Standard event reference

## Events handled

The following events are handled by the Campaign Standard extension:

### Campaign Request Content <a id="campaign-request-content"></a>

This event is dispatched from the Event Hub when a Campaign rule is found to be true. For example, after the user launches the app, the _"User has launched the app"_ rule is found to be true. A triggered consequences event is dispatched, which contains the data of the displayed local, alert, or full-screen message.

#### Data payload definition <a id="data-payload-definition-1"></a>

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `triggeredconsequence` | Map | No | The triggered Campaign rule consquence. |

#### Event data example

triggered consequence data

```text
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

### Configuration Response Content <a id="configuration-response-content"></a>

The data property in this event is used by each extension to modify its current settings. Each extension is responsible for reading out the part of the data property for which it is concerned.

#### Data payload definition <a id="data-payload-definition-3"></a>

The Adobe Campaign Standard extension reads the following key from the configuration event:

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
| `campaign.registrationDelay` | Integer | Yes | This contains the number of days to delay the sending of the next Adobe Campaign Standrd registration request. |
| `campaign.registrationPaused` | Boolean | Yes | This contains the Adobe Campaign Standard registration request paused status. |

{% hint style="info" %}
After `global.privacy` is changed to **optout**, the linkage fields are reset. All downloaded messages and rules are erased, and no tracking request can leave the device.
{% endhint %}

{% hint style="danger" %}
The configuration setting to pause registration requests is provided for specific use cases only. The use of this configuration setting should be avoided when possible.
{% endhint %}

#### Event data example

```text
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

### Request Identity <a id="request-identity"></a>

This event is dispatched by the API to setLinkageFields, which sets the linkage fields. It is used to download personalized in-app messages.

#### Data payload definition <a id="data-payload-definition-4"></a>

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `linkagefields` | Map | No | This map contains at least one of the linkage fields that are used to personally identify the user who is logged in. |

#### Event data example

```text
{ 
    "linkagefields": 
    { 
        "firstName":"john", 
        "lastName":"doe", 
        "age":30
    }
}
```

### Request Reset <a id="request-reset"></a>

This event is dispatched when users no longer want to use personalized in-app messages. After this event is received, Campaign deletes all personalized messages and downloads only generic messages again.

#### Data payload definition <a id="data-payload-definition-5"></a>

This event has no event data.

### Lifecycle Response Content <a id="lifecycle-response-content"></a>

This event is a response from the Lifecycle extension to notify a client/extension about lifecycle context data in which the extension/client might be interested. The event is generated by the Lifecycle extension, and the API is called after a lifecycle start, stop, or pause.

#### Data payload definition <a id="data-payload-definition-6"></a>

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `lifecyclecontextdata` | Map | No | The map that contains the stored lifecycle metrics. |

#### Event data example

```text
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

### Generic Data OS <a id="generic-data-os"></a>

This event is dispatched by the Core extension to the Event Hub when the `collectMessageInfo` API is invoked by the app developer to track local and push notification interactions.

#### Data payload definition <a id="data-payload-definition-7"></a>

Here are the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `deliveryId` | String | No | The string that contains the delivery ID of the message for which there were interactions. |
| `action` | String | No | The string that contains the message interaction ID. |
| `broadlogId` | String | No | The string that contains the broadlog ID of the message for which there were interactions. |

#### Event data example

```javascript
{
  "deliveryId": "1442de4",
  "action": "2",
  "broadlogId": "h1c1380"
}
```

## Events dispatched

The following events are dispatched by the Campaign Standard extension:

### Campaign Response Content

This event is a response from the Adobe Campaign Standard extension and contains the message interaction details (Viewed, Triggered or Clicked).

#### Event details

| **Event Type** | **Event Source** | **Paired** |
| :--- | :--- | :--- |
| `com.adobe.eventType.campaign` | `com.adobe.eventSource.responseContent` | Yes |

#### Data payload definition

Here is the definition of the key-value pairs in this event:

| **Key** | **Value Type** | **Optional** | **Description** |
| :--- | :--- | :--- | :--- |
| `a.message.id` | String | No | Message ID of the message that was triggered. |
| `a.message.triggered` | String ("1") | No | Flag that specifies a message triggered event. Only one type of message interaction exists in each Campaign response content event. |
| `a.message.viewed` | String ("1") | No | Flag that specifies a message viewed event. |
| `a.message.clicked` | String ("1") | No | Flag that specifies a message clicked event. |

#### Event data example

```text
{ "a.message.id": "12345678", "a.message.triggered": "1" }
{ "a.message.id": "12345678", "a.message.viewed": "1" }
{ "a.message.id": "12345678", "a.message.clicked": "1" }
```

