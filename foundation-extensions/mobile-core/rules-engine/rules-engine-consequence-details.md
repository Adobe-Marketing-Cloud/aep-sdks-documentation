# Rules Engine consequence details

The Adobe Experience Platform Mobile SDK supports multiple types of rule consequences (also known as actions) that can be executed when the trigger event and the conditions are met. This section contains a detailed description of each rule consequence.

## Analytics consequence

This rule consequence is currently handled by the [Analytics](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-analytics) extension.

| Friendly name | Key | Type | Description |
| :--- | :--- | :--- | :--- |
| Action | action | string | _(Optional)_ If provided, this value will be used as the action parameter in a `trackAction` call. |
| State/Page name | state | string | _(Optional)_ If provided, this value will be used as the state parameter in a `trackState` call. |
| Context data | contextdata | object | _(Optional)_ Additional context data to be attached to the resulting Analytics request. The object should only have one level of depth that contains  key-value pairs. |

## In-App message consequence

This rule consequence is currently handled by the [Campaign](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-campaign-standard) extension.

| Friendly name | Key | Type | Description |
| :--- | :--- | :--- | :--- |
| In-App template | template | string | _(Required)_ Determines the display method of the In-App message. Currently supported types are `fullscreen`, `alert` and `local`. |
| Fullscreen message content | html | string | _(Required for fullscreen message type)_ Filename of the HTML content to load for a fullscreen In-App message. This file will be sourced from the same zip file the `assets/` directory from which the consequence was retrieved. The base path (`assets/`) should not be included in this value. |
| Remote assets | remoteAssets | array | _(Optional, only used by the fullscreen message type)_ Array of strings of remote assets that should be cached by the client. These should be full-URL strings with HTTPS transport. |
| Message title | title | string | _(Required for the alert message type)_ String that defines the title of the alert message. |
| Message content | content | string | _(Required for the alert and the local type message types)_ String that defines the content of the alert or local notification. |
| Confirm button text | confirm | string | _(Optional, only used by alert messages)_ String that defines the text on the **Confirm** button in the OS-operated dialog. |
| Cancel button text | cancel | string | _(Required for alert message type)_ String that defines the text for the **Cancel** button in the OS-operated dialog. |
| Confirmation URL | url | string | _(Optional, only used by alert messages with the **Confirm** key)_ String that defines the URL to trigger when the **Confirm** button in an alert dialog is triggered. Typically used in deep link scenarios but can also be used to trigger external sites and apps. |
| Wait time | wait | number | _(Optional, only used by the local notification message type)_ Total number of seconds to delay the triggering of a local notification. The default value is 0 (immediate). If a `date` is also provided, the wait field is ignored. |
| Fire date | date | number | _(Optional, only used by the local notification message type)_ Represented as the number of seconds since epoch, this field indicates a specific time to deliver this local notification. If provided, this field has precedence over the **wait** field. |
| Deep link | adb\_deeplink | string | _(Optional, only used by the local notification message type)_ Deep link URL to attach to the payload of the notification, which allows users who click-through the notification to be redirected to the provided URL. |
| Custom user data | userData | object | _(Optional, only used by the local notification message type)_ A custom dictionary of  pairs that will be attached to the payload of the notification. |
| Category | category | string | _(Optional, only used by the local notification message type)_ A category ID for this notification. |
| Sound | sound | string | _(Optional, only used by the local notification message type)_ The name of a custom sound to use when this notification is delivered. |

## Postback consequence

This rule is currently handled by the [Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals) extension.

| Friendly name | Key | Type | Description |
| :--- | :--- | :--- | :--- |
| Description URL | templateurl | string | _(Required)_ Destination URL to which the postback signal will be sent. |
| Request body | templatebody | string | _(Optional)_ A string that contains the POST body that will be sent. If this value exists, the postback is sent as a POST instead of as a GET request.  You must ensure that the string is appropriately json escaped. |
| Content type | contenttype | string | _(Optional)_ Used to set the Content-Type header for POST requests. If the header is not supplied, and a request body is found, the default is `application/x-www-form-urlencoded`. |
| Connection timeout | timeout | number | _(Optional)_ The timeout value for the network connection in seconds. The default value is 2 seconds. |

## Sync PII consequence

This rule is currently handled by the [Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals) extension.

| Friendly name | Key | Type | Description |
| :--- | :--- | :--- | :--- |
| Description URL | templateurl | string | _(Required)_ Destination URL to which the PII signal will be sent. Must be HTTPS, and non-HTTPS URLs will be ignored. |
| Request body | templatebody | string | _(Optional)_ A base64-encoded blob that contains the POST body to be sent. If this value exists, the PII signal will be sent as a POST instead of as a GET request. |
| Content type | contenttype | string | _(Optional)_ Used to set the Content-Type header for POST requests. If the header is not supplied, but a request body is found, the default is `application/x-www-form-urlencoded`. |
| Connection timeout | timeout | number | _(Optional)_ The timeout value for the network connection in seconds. The default value is 2 seconds. |

## Open URL consequence

This rule is currently handled by the [Signal](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/signals) extension.

| Friendly name | Key | Type | Description |
| :--- | :--- | :--- | :--- |
| URL | url | string | _(Required)_ URL that will be opened by the target platform. This might be a URL for a website or a deep link to an app. |

## Profile consequence

This rule is currently handled by the [Profile](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile) extension.

| Friendly name | Key | Type | Description |
| :--- | :--- | :--- | :--- |
| Operation to perform | operation | string | _(Required)_ Determines the type of operation to be performed on the profile. The following operations are supported:  - _write,_ which saves `value` in the given `key` in the shared state and the local profile.   If an associated value for the key already exists, the existing value will be overwritten.   - _delete,_ which removes `key` from the profile's shared state and the local profile. |
| Device-side profile key | key | string | _(Required)_ Key in the device-side profile on which the requested operation will be performed.  **Tip**: This key will be accessible later through the shared state from the Profile extension. For more details, see [User profile shared state](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/profile/profiles-event-reference#shared-state). |
| Device-side profile value | value | string or number | _(Required for write operations)_ New value to write to the key. |

## Attach data consequence

This rule is currently handled by the [Mobile Core](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core) extension.

| Friendly name | Key | Type | Description |
| :--- | :--- | :--- | :--- |
| Event data | eventdata | object | _(Required)_ Dictionary of  pairs to overlay on the triggering event's EventData. For more information, see [Attach Data tutorial](https://aep-sdks.gitbook.io/docs/resources/user-guides/attach-data). |

