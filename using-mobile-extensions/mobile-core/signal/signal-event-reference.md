# Signal event reference

## Events handled

### Rules Engine Response Content

This event is used by the Signal extension to queue up and send network calls that correspond to the [sync pii consequence](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine/rules-engine-consequence-details#sync-pii-consequence) or postback message.

This event is triggered by the Rules Engine when the events and conditions are met.

#### Event details

| **Event Type**                  | **Event Source**                      | **Paired** | **Paired Event** |
| :------------------------------ | :------------------------------------ | :--------- | :--------------- |
| com.adobe.eventType.rulesengine | com.adobe.eventSource.responseContent | No         | -                |

#### Data payload definition

The key-value pairs in this event correspond to Postback and Sync PII:

| Key                  | Friendly name   | Type                | Optional | Description                               |
| -------------------- | --------------- | ------------------- | -------- | ----------------------------------------- |
| triggeredconsequence | Description URL | Map<String, Object> | Yes      | Triggered Consequence details in the map. |

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

Open URL Request with a deeplink URL

```
{
    ``"id"`        `: ``"48181acd22b3edaebc8a447868a7df7ce629920a"``,
    ``"type"`      `: ``"url"``,
    ``"detail"`    `: {
        ``"url"` `: ``"myApp://HomePage"
    ``}
}
```



### Configuration Response Content

This event is dispatched on the Event Hub when a configuration change is processed.  If a change occurs, the listener updates the privacy status. 

#### Event details

| **Event Type**                    | **Event Source**                      | **Paired** | **Paired Event** |
| :-------------------------------- | :------------------------------------ | :--------- | :--------------- |
| com.adobe.eventType.configuration | com.adobe.eventSource.responseContent | No         | N/A              |

#### Data payload definition

The Signal extension will read the following keys from the configuration event:

| Key            | Friendly name | Type                                                         | Optional | Description                                                  |
| -------------- | ------------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| name           | Event Name    | string                                                       | No       | Name of the event.                                           |
| type           | Event Type    | string                                                       | No       | Type of the event.                                           |
| source         | Event Source  | string                                                       | No       | Source of the event.                                         |
| id             | Event ID      | string                                                       | No       | ID used for the event.                                       |
| eventData      | Event Data    | [Event Data](https://aep-sdks.gitbook.io/docs/resources/user-guides/attach-data#what-are-sdk-events) | No       | A map of key-value pairs that represents the configuration for all the modules. |
| global.privacy | String        | String                                                       | No       | Contains the default setting that the user has requested with regards to data privacy. |
| timestamp      | Time Stamp    | number                                                       | No       | Time (in seconds) since Jan 1, 1970.                         |

#### Event data example

For a configuration change event:

```javascript
{
    "global.privacy": "true"
}
```

## Events dispatched and Shared State

The Signal extension does not dispatch an event and does not share any shared state.

