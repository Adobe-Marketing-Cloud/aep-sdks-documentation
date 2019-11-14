# Signal event reference

## Events handled

### Rules Engine Response Content

This event is used by the Signal extension to queue up and send network calls corresponding to the sync pii call or postback message.

This event is triggered by the Rules Engine when events and conditions are met.

#### Event details

| **Event Type**                  | **Event Source**                      | **Paired** | **Paired Event** |
| :------------------------------ | :------------------------------------ | :--------- | :--------------- |
| com.adobe.eventType.rulesengine | com.adobe.eventSource.responseContent | No         | -                |

#### Data payload definition

The key-value pairs in this event that corresponds to Postback and Sync PII:

| Key          | Friendly name      | Type   | Optional | Description                                                  |
| ------------ | ------------------ | ------ | -------- | ------------------------------------------------------------ |
| templateurl  | Description URL    | string | No       | Destination URL that the postback signal will be sent to.    |
| templatebody | Request body       | string | Yes      | A string containing the post-body to be sent. If this value exists, the postback will be sent as a POST instead of a GET request. Note: The string should be appropriately json escaped if needed. |
| contenttype  | Content type       | string | Yes      | Used to set the Content-Type header for POST requests. If not supplied but a request body is found, the default will be `application/x-www-form-urlencoded` |
| timeout      | Connection timeout | number | Yes      | Timeout for network connection in seconds. The default value is 2 seconds. |

The key-value pairs in this event that corresponds to Open URL:

| Key  | Friendly name | Type   | Optional | Description                                                  |
| ---- | ------------- | ------ | -------- | ------------------------------------------------------------ |
| url  | URL           | string | No       | URL that will be opened by the target platform. This may be a URL for a website, or a deeplink to an app. |

#### Event data example

Postback Message

```javascript
{
    "id"        : "9d40f5665d5bdbe96dcb3a24f4e4fe98d686a602",
    "type"      : "pb",
    "detail"    : {
        "templateurl"   : "https://www.endpoint.com/post/{%urlenc(~sdkver)%}",
        "templatebody"  : "{\"jsonkey\":\"jsonvalue\",\"sdkkey\":\"{%~sdkver%}\"}",
        "contenttype"   : "application/json",
        "timeout"       : 5
    }
}
```

#### Event data example

Open URL Request 

```
{
    ``"id"`        `: ``"48181acd22b3edaebc8a447868a7df7ce629920a"``,
    ``"type"`      `: ``"url"``,
    ``"detail"`    `: {
        ``"url"` `: ``"https://www.endpoint.com/{%~sdkver%}"
    ``}
}
```



### Configuration Response Content

This event is dispatched onto the event hub when a configuration change is processed.  This listener updates the privacy status if there is any change. 

#### Event details

| **Event Type**                    | **Event Source**                      | **Paired** | **Paired Event** |
| :-------------------------------- | :------------------------------------ | :--------- | :--------------- |
| com.adobe.eventType.configuration | com.adobe.eventSource.responseContent | No         | N/A              |

#### Data payload definition

Definition of the key/value pairs that this listener should look for global.privacy in this event data.

| Key       | Friendly name | Type                                                         | Optional | Description                                                  |
| --------- | ------------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| name      | Event Name    | string                                                       | No       | Name of event                                                |
| type      | Event Type    | string                                                       | No       | Type of event                                                |
| source    | Event Source  | string                                                       | No       | Source of event                                              |
| id        | Event ID      | string                                                       | No       | ID used for event                                            |
| eventData | Event Data    | [Event Data](https://wiki.corp.adobe.com/display/ADMSMobile/Event+Data) | No       | A map of key-value pairs representing configuration for all modules |
| timestamp | Time Stamp    | number                                                       | No       | Time (in seconds) since Jan 1, 1970                          |

Definition of the key-value pairs that will be present in the Event Data of the Configuration Response Content event.  

| Extension        | Key                                   | Value Type | Description                                                  |
| :--------------- | :------------------------------------ | :--------- | :----------------------------------------------------------- |
| Acquisition      | acquisition.appid                     | string     | Application ID assigned by Adobe Mobile Services             |
|                  | acquisition.server                    | string     | Server address for the fingerprinter                         |
| Analytics        | analytics.aamForwardingEnabled        | boolean    | If set to true, Analytics data collection servers will attempt to forward data to Audience Manager on the back end |
|                  | analytics.batchLimit                  | number     | Indicates to Analytics the number of hits that should be stored until they are all sent in succession |
|                  | analytics.offlineEnabled              | boolean    | If set to true, Analytics will store its data even while the device is offline |
|                  | analytics.referrerTimeout             | number     | Amount of time the Analytics module will wait for acquisition data prior to sending an install hit |
|                  | analytics.backdatePreviousSessionInfo | boolean    | If set to true, Analytics requests containing session info or crash events will be backdated to one second after the last hit was sent. If false, this data will be attached to the first hit of the subsequent session |
|                  | analytics.rsids                       | string     | Contains a comma-delimited list of report suites to which the Analytics data should be sent |
|                  | analytics.server                      | string     | Contains the server endpoint used to collect Analytics data for this customer's report suite |
| Audience Manager | audience.server                       | string     | Contains the server endpoint used to collect Audience Manager data |
|                  | audience.timeout                      | number     | Amount of time, in seconds, to wait for a response from Audience Manager before timing out |
| Campaign         | campaign.pkey                         | string     | App Identifier in the Campaign database                      |
|                  | campaign.server                       | string     | Contains the server endpoint used to communicate with Campaign |
| Global           | global.privacy                        | string     | Contains the default setting that the user has request with regards to data privacy |
|                  | global.ssl                            | boolean    | If set to true, network requests should be dispatched via HTTPS. If false, network requests should be dispatched via HTTP |
| Identity         | experienceCloud.org                   | string     | Experience Cloud Org Identifier                              |
|                  | experienceCloud.server                | string     | Custom endpoint to be used for Visitor ID Service network requests |
|                  | identity.adidEnabled                  | boolean    | If set to true, indicates that the SDK should expect a call to setAdvertisingIdentifier (removed v1.0.1) |
| Lifecycle        | lifecycle.sessionTimeout              | number     | Number of seconds since the user background the app that must pass in order for the subsequent app launch (or resume) to be considered a new lifecycle session |
| Rules Engine     | rules.url                             | string[]   | List of Rules endpoints (represented as strings), in order of preference |
| Target           | target.clientCode                     | string     | Special identifier given to the customer by the Target product. |
|                  | target.environmentId                  | string     | Indicates the Environment ID for the Target customer         |
|                  | target.timeout                        | string     | Amount of time, in seconds, to wait for a response from Target before timing out |

#### Event data example

Set Advertising Identifier request

```javascript
{
    "global.privacy": "true"
}
```

## Events dispatched

The Signal Extension does not dispatch any event.

