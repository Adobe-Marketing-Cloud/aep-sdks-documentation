# Rules engine consequence detail definition

The Adobe Experience Platform Mobile SDK supports multiple types of rule consequences (also known as actions) that can be executed if the trigger event and the conditions are met. This page contains a detailed description of each rule consequence.

## Analytics consequence

This rule consequence is currently handled by the [Adobe Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) mobile extension.

| Friendly name   | Key         | Type   | Description                                                  |
| --------------- | ----------- | ------ | ------------------------------------------------------------ |
| Action          | action      | string | *(Optional)* If provided, this value will be used as the action parameter in a trackAction call. |
| State/Page name | state       | string | *(Optional)* If provided, this value will be used as the state parameter in a trackState call. |
| Context data    | contextdata | object | *(Optional)* Additional context data to be attached to the resulting Analytics request. The object should only have one level of depth, containing <string, string> key-value pairs. |

## In-App message consequence

This rule consequence is currently handled by the [Adobe Campaign](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) mobile extension.

| Friendly name              | Key          | Type   | Description                                                  |
| -------------------------- | ------------ | ------ | ------------------------------------------------------------ |
| In-App template            | template     | string | *(Required)* Determines the display method of the in-app message. Currently supported types are: fullscreen, alert and local. |
| Fullscreen message content | html         | string | *(Required for fullscreen-type messages)* Filename of the HTML content to load for a fullscreen in-app message. This file will be sourced from the same zip file the consequence was retrieved from, within the assets/ folder. The base path (assets/) should not be included in this value. |
| Remote assets              | remoteAssets | array  | *(Optional, only used by fullscreen-type messages)* Array of strings of remote assets that should be cached by the client. These should be full-url strings with HTTPS transport. |
| Message title              | title        | string | *(Required for alert message type)* String defining the title of the alert message. |
| Message content            | content      | string | *(Required for alert and local type messages)* String defining the content of the alert or local notification. |
| Confirm button text        | confirm      | string | *(Optional, only used by alert messages)* String defining the text on the 'confirm' button in the OS-operated dialog. |
| Cancel button text         | cancel       | string | *(Required for alert message type)* String defining the text for the 'cancel' button in the OS-operated dialog. |
| Confirmation URL           | url          | string | *(Optional, only used by alert messages in conjunction with 'confirm' key)* String defining the URL to trigger if the confirm button of an alert dialog is triggered. Typically used for deep-linking type scenarios, but can be used to trigger external sites and apps. |
| Wait time                  | wait         | number | *(Optional, only used by local notification message type)* Total number of seconds to delay the triggering of a local notification. Defaults to 0 (immediate). If a `date` is also provided in this detail, the wait field is ignored. |
| Fire date                  | date         | number | *(Optional, only used by local notification message type)* Represented as number of seconds since epoch, this field indicates a specific time to deliver this local notification. If provided, this field has precedence over the `wait` field. |
| Deep link                  | adb_deeplink | string | *(Optional, only used by local notification message type)* Deep link URL to attach to the payload of the notification, allowing users who click-through the notification to be redirected to the provided url. |
| Custom user data           | userData     | object | *(Optional, only used by local notification message type)* A custom dictionary of <key, value> pairs that will be attached to the payload of the notification. |
| Category                   | category     | string | *(Optional, only used by local notification message type)* A category ID for this notification. |
| Sound                      | sound        | string | *(Optional, only used by local notification message type)* The name of a custom sound to use when this notification is delivered. |

## Postback consequence

This rule is currently handled by the [Adobe Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals) mobile extension.

| Friendly name      | Key          | Type   | Description                                                  |
| ------------------ | ------------ | ------ | ------------------------------------------------------------ |
| Description URL    | templateurl  | string | *(Required)* Destination URL that the postback signal will be sent to. |
| Request body       | templatebody | string | *(Optional)* A string containing the post-body to be sent. If this value exists, the postback will be sent as a POST instead of a GET request. <br/>Note: The string should be appropriately json escaped if needed. |
| Content type       | contenttype  | string | *(Optional)* Used to set the Content-Type header for POST requests. If not supplied but a request body is found, the default will be `application/x-www-form-urlencoded` |
| Connection timeout | timeout      | number | *(Optional)* Timeout for network connection in seconds. The default value is 2 seconds. |

## Sync PII consequence

This rule is currently handled by the [Adobe Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals) mobile extension.

| Friendly name      | Key          | Type   | Description                                                  |
| ------------------ | ------------ | ------ | ------------------------------------------------------------ |
| Description URL    | templateurl  | string | *(Required)* Destination URL that the PII signal will be sent to. Must be HTTPS, non HTTPS urls will be ignored. |
| Request body       | templatebody | string | *(Optional)* base64 encoded blob containing the post body to be sent. If this value exists, the PII signal will be sent as a POST instead of a GET request. |
| Content type       | contenttype  | string | *(Optional)* Used to set the Content-Type header for POST requests. If not supplied but a request body is found, the default will be `application/x-www-form-urlencoded` |
| Connection timeout | timeout      | number | *(Optional)* Timeout for network connection in seconds. The default value is 2 seconds. |

## Open URL consequence

This rule is currently handled by the [Adobe Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals) mobile extension.

| Friendly name | Key  | Type   | Description                                                  |
| ------------- | ---- | ------ | ------------------------------------------------------------ |
| URL           | url  | string | *(Required)* URL that will be opened by the target platform. This may be a URL for a website, or a deeplink to an app. |

## Profile consequence

This rule is currently handled by the [Adobe Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile) mobile extension.

| Friendly name             | Key       | Type             | Description                                                  |
| ------------------------- | --------- | ---------------- | ------------------------------------------------------------ |
| Operation to perform      | operation | string           | *(Required)* Determines the type of operation to be performed on the profile. The supported operations are: <br/>- *write*: saves `value` into given `key` in shared state and local profile. If an associated value for key already exists, the existing value will be overwritten. <br/> - *delete*: removes `key` from Profile shared state and from local profile. |
| Device-side profile key   | key       | string           | *(Required)* Key within the device-side profile to perform the requested operation on. <br/>Note: This key will be accessible later through the shared state from the Profile extension. For more details, see [User profile shared state](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile/profiles-event-reference#shared-state). |
| Device-side profile value | value     | string or number | *(Required for write operations)* New value to write to key. |

## Attach data consequence

This rule is currently handled by the [Adobe Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) mobile extension.

| Friendly name | Key       | Type   | Description                                                  |
| ------------- | --------- | ------ | ------------------------------------------------------------ |
| Event data    | eventdata | object | *(Required)* Dictionary of <key, value> pairs to overlay on the triggering Event's EventData. For more details, see [Attach Data tutorial](https://aep-sdks.gitbook.io/docs/resources/user-guides/attach-data). |

