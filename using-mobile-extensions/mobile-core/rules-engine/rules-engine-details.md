# Rules Engine technical details

## Key definitions

* A condition is a boolean equation that evaluates to `true` or `false`.
* A consequence is the action to be performed when the trigger is met and the condition\(s\) evaluates to `true`.
* A rule is a set of conditions and the associated consequence\(s\).
* A triggering event is the event that started the rule evaluation. The Adobe Experience Platform Mobile SDK evaluates each rule configured in Adobe Launch for the current event processed by the Event Hub.
* Rules engine is the system that processes the mobile rules configured in Adobe Launch and triggers the associated actions if the conditions are met.
* An Asset is an opaque data blob that is needed by a specific consequence.

## Rules delivery

Rules delivery occurs by using a network request from the Experience Platform SDKs to a static endpoint that is defined as part of the SDK configuration. The rules file for each mobile property is hosted on https://assets.adobedtm.com.

This request is a conditional `GET` and occurs by default at the start of each new application session. This means that if there are any changes in Adobe Launch for the set of rules configured for a mobile property, those changes will be picked up by the Experience Platform SDK in the next session or after the application is restarted.

## File format

Rules and their associated assets are delivered as a standard ZIP archive, which uses the following format:

- `rules.json`
- `assets /`
  - `(asset)`
  - `(asset)`

The `rules.json` consists of a root-level JSON object that contains the following elements:

| **Friendly Name** | **Key** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| Version | `version` | number | \(Required\) Version number of the `rules.json` file format. Should be an integer that increments by 1 for each format change, and the initial version is 1. |
| Rules | `rules` | array | \(Required\) An array of rules objects. For more information, see [Rule object definition](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#rule-object-definition). |

## Rule object definition

| **Friendly Name** | **Key** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| Condition | `condition` | object | **\(**Required\) Holds the definition for the base Condition object for this rule. Each Condition object has a type and can be a Group or a Matcher condition. Group conditions contain a logic type and an array of condition objects. Matcher conditions contain a key, value, and matcher type.   There is one root-level condition for a rule, and this condition can have any number of nested conditions by using the group construct. For more information, see [Condition object definition](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-object-definition) |
| Action | `consequences` | array | \(Required\) Array of consequence objects, where each object contains the details for the associated consequence that are executed when the associated condition evaluates to `true`. For more information, see [Consequence object definition](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-object-definition). |

## Condition object definition

Each Condition has a condition type and a definition, and the contents of a condition's definition depends on its condition type.

A Group condition contains an array of conditions, which makes the conditions infinitely nestable.

### Condition object

| **Friendly Name** | **Key Value** | **Value Type** | **Example** | **Description** |
| :--- | :--- | :--- | :--- | :--- |
| Condition Type | `type` | string | `"type":"group"` | Indicates the type of the current condition. The value must be a valid string from the [Condition types](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#condition-types). |
| Definition | `definition` | object | `"definition": { "logic" : "and", "conditions" : [...] }` | Defines how the condition should be evaluated. The contents of this object will be different depending on the condition type. |

### Condition types

| **Name** | **Value** | **Description** |
| :--- | :--- | :--- |
| Group | `group` | This condition is a container, that holds additional conditions, and the logical evaluator that is used to process those conditions. |
| Matcher | `matcher` | This condition holds the key, matcher type, and value that should be evaluated. |

### Definition object 

#### Group condition type

| **Friendly Name** | **Key Value** | **Value Type** | **Example** | **Description** |
| :--- | :--- | :--- | :--- | :--- |
| Logic Type | `logic` | string | `"logic":"and"` | Must be a valid Logic Type. Indicates which logical operator should be used for the Conditions that are defined in the Definition's Conditions array. |
| Conditions | `conditions` | array | `"conditions":[...]` | An array of Condition objects. |

#### Matcher condition type

{% hint style="info" %}

The keys used here are different than those used for in-app message matchers.

{% endhint %}

| **Friendly Name** | **Key** | **Value Type** | **Example** | **Description** |
| :--- | :--- | :--- | :--- | :--- |
| Key | `key` | `string` | `"key":"key1"` | Key to get the value from the dictionary that is passed as a parameter to the rules processor. |
| Matches | `matcher` | `string` | `"matcher":"eq"` | Matcher type that determines the kind of evaluation to use between the two values. |
| Values | `values` | `array` | `"values":["value0", "value1"]` | List of values that are compared \(using OR\) against the value in the parameter dictionary for the `"key"` key. |

### Logic types

| **Name** | **Value** | **Description** |
| :--- | :--- | :--- |
| AND | `and` | For this definition to evaluate to `true`, all of its conditions must be true. |
| OR | `or` | For this definition to evaluate to `true`, only one of its conditions must be true. |

### Matcher types

| **Name** | **Value** | **Application Type** |
| :--- | :--- | :--- |
| Equals | `eq` | string, number |
| Not Equals | `ne` | string, number |
| Exists | `ex` | no value required |
| Not Exists | `nx` | string, number |
| Greater Than | `gt` | number |
| Greater Than or Equals | `ge` | number |
| Less Than | `lt` | number |
| Less Than or Equals | `le` | number |
| Contains | `co` | string |
| Not Contains | `nc` | string |
| Starts With | `sw` | string |
| Ends With | `ew` | string |

### Matching and retrieving values by keys

By default, keys and the associated values are sourced from the current event that is being processed by the Rules Engine. There are some special key prefixes that can cause the values to be sourced from other locations known to the Experience Platform SDKs. 

To avoid collisions, special key prefixes always start with `~` (tilde) to differentiate them from the standard event key names.

| **Key Prefix** | **Example** | **Description** |
| :--- | :--- | :--- |
| `~state.` | `~state.sharedStateName/keyName` | Reads the `keyName` from the shared state of the module that is stored in `sharedStateName`. |
| `~type` | `~type` | Reads `eventType` from the triggering event. |
| `~source` | `~source` | Reads `eventSource` from the triggering event. |
| `~timestampu` | `~timestampu` | Reads the current device time in epoch format \(seconds since epoch\). |
| `~timestampz` | `~timestampz` | Reads the current device time in ISO 8601 data elements and interchange format. |
| `~sdkver` | `~sdkver` | Reads the current Adobe Experience Platform SDKs version string. |
| `~cachebust` | `~cachebust` | Generates a random number to be used for cache busting. |
| `~all_url` | `~all_url` | Contains all data in the Event object and is encoded in the `url` format. |
| `~all_json` | `~all_json` | Contains all data in the Event object that is encoded in the `json` format. |

## Simple conditions

**Conditions example 1** represents the following logical condition:

```text
(key1 == value1)
```

Here is the example:

```text
  "conditions": [
    {
        "type" : "matcher",
        "definition" : {
            "key" : "key1",
            "matcher" : "eq",
            "values" : ["value1"]
        }
    }
]
```

**Conditions example 2** is slightly more complex and represents the following logical condition:

```text
(key1 == value1 || key1 == value2) || (key2 != value3 && key2 != value4)
```

Here is the example:

```text
    {
        "type" : "group",
        "definition" : {
            "logic" : "or",
            "conditions" : [
                {
                    "type" : "matcher",
                    "definition" : {
                        "key" : "key1",
                        "matcher" : "eq",
                        "values" : ["value1", "value2"]
                    }
                },
                {
                    "type" : "group",
                    "definition" : {
                        "logic" : "and",
                        "conditions" : [
                            {
                                "type" : "matcher",
                                "definition" : {
                                    "key" : "key2",
                                    "matcher" : "ne",
                                    "values" : ["value3"]
                                }
                            },
                            {
                                "type" : "matcher",
                                "definition" : {
                                    "key" : "key2",
                                    "matcher" : "ne",
                                    "values" : ["value4"]
                                }
                            }
                        ]
                    }
                }
            ]
        }
    }
```

## Consequence object definition

The consequences section of a rule lists the file names of each consequence object that should be performed when all the conditions for that rule evaluate to `true`.

| **Friendly Name** | **Key    Value** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| Identifier | `id` | string | (Required) String that contains a unique identifier for this consequence.  `sha1`, or another guaranteed random value with a near-impossible chance of collisions, is recommended. |
| Consequence Type | `type` | string | (Required) A Consequence Type from the [Consequences Type](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-types) table. |
| Consequence Details | `detail` | object | (Required) JSON object that contains the details that are necessary to perform a consequence of the given type. |

## Consequence types

| **Name** | **Value** | **Description** | **Payload Definition** |
| :--- | :--- | :--- | :--- |
| Analytics | `an` | Sends data to Analytics | Analytics event consequence detail definition |
| In-App Message | `iam` | In-App Message | In-App consequence detail definition |
| Postback | `pb` | Send Postback\(s\) | Postback consequence detail definition |
| PII | `pii` | Sync PII | Sync PII consequence detail definition |
| Open URL | `url` | Passes the provided URL to be opened by the platform that is most commonly used for app deeplinking. | Open URL consequence detail definition |
| Client Side Profile | `csp` | Create or delete operations against the client-side profile. | Profile consequence detail definition |
| Attach Data | `add` | Attaches key-value pairs to the EventData of an existing Event | Attach data consequence detail definition |

### Consequence detail definition 

#### Analytics consequence

| Friendly name   | Key          | Type   | Description                                                  |
| --------------- | ------------ | ------ | ------------------------------------------------------------ |
| Action          | action       | string | (Optional) If provided, this value will be used as the action parameter in a trackAction call. |
| State/Page Name | state        | string | (Optional) If provided, this value will be used as the state parameter in a trackState call. |
| Context Data    | context data | object | (Optional) Additional context data to be attached to the resulting Analytics request. The object should only have one level of depth, containing <string, string> key-value pairs. |

#### In-App message consequence

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

#### Postback consequence

| Friendly name      | Key          | Type   | Description                                                  |
| ------------------ | ------------ | ------ | ------------------------------------------------------------ |
| Description URL    | templateurl  | string | *(Required)* Destination URL that the postback signal will be sent to. |
| Request body       | templatebody | string | *(Optional)* A string containing the post-body to be sent. If this value exists, the postback will be sent as a POST instead of a GET request. Note: The string should be appropriately json escaped if needed. |
| Content type       | contenttype  | string | *(Optional)* If this value exists the postback will be sent as a POST instead of a GET request. If not supplied but a request body is found, the default will be `application/x-www-form-urlencoded` |
| Connection timeout | timeout      | number | *(Optional)* Timeout for postback connection in seconds. The default value is 2 seconds. |

#### Sync PII consequence



#### Open URL consequence

#### Profile consequence

#### Attach data consequence

| Friendly name | Key       | Type   | Description                                                  |
| ------------- | --------- | ------ | ------------------------------------------------------------ |
| Event data    | eventdata | object | *(Required)* Dictionary of <key, value> pairs to overlay on the triggering Event's EventData. |



## rules.json examples

**Example 1** is a set of rules that will only run when the event was as a result of an Analytics hit or a GPS location event.

The conditions array is set up with the following logic:

```text
 ((key1 == value1 || key1 == value2) || (key2 != value3 && key2 != value4)) && (key3 == value5 || key3 == value6)
```

If the conditions pass, an in-app message triggered:

```text
{
"version" : 1,
"rules" : [
    {
        "condition" : {
            "type" : "group",
            "definition" : {
                "logic" : "and",
                "conditions" : [
                    {
                        "type" : "group",
                        "definition" : {
                            "logic" : "or",
                            "conditions" : [
                                {
                                    "type" : "matcher",
                                    "definition" : {
                                        "key" : "key1",
                                        "matcher" : "eq",
                                        "values" : ["value1", "value2"]
                                    }
                                },
                                {
                                    "type" : "group",
                                    "definition" : {
                                        "logic" : "and",
                                        "conditions" : [
                                            {
                                                "type" : "matcher",
                                                "definition" : {
                                                    "key" : "key2",
                                                    "matcher" : "ne",
                                                    "values" : ["value3"]
                                                }
                                            },
                                            {
                                                "type" : "matcher",
                                                "definition" : {
                                                    "key" : "key2",
                                                    "matcher" : "ne",
                                                    "values" : ["value4"]
                                                }
                                            }
                                        ]
                                    }
                                }
                            ]
                        }
                    },
                    {
                        "type" : "matcher",
                        "definition" : {
                            "key" : "key3",
                            "matcher" : "eq",
                            "values" : ["value5", "value6"]
                        }
                    },
                    {
                        "type" : "matcher",
                        "definition" : {
                            "key" : "~type",
                            "matcher" : "eq",
                            "values" : ["com.adobe.eventType.location", "com.adobe.eventType.analytics"]
                        }
                    }
                ]
            }
        },        
        "consequences" : [
            {
                "id"        : "48181acd22b3edaebc8a447868a7df7ce629920a",
                "type"        : "iam",
                "detail"      : {
                    "template"    : "fullscreen",
                    "html"        : "48181acd22b3edaebc8a447868a7df7ce629920a.html"
                }
            }
        ]
    }
]
}
```

**Example 2** uses the client-side profile to implement a _show once_ style of in-app message. The conditions array is set up with the following logic:

`((key3 == value5 || key3 == value6) && (~state.com.adobe.module.userProfile/userprofiledata.48181acd22b3edaebc8a447868a7df7ce629920a-seen does not exist))`

If the conditions pass, the in-app message is displayed \(first consequence\), and future displays of the message are prevented by writing/incrementing value to the client-side profile:`(~state.com.adobe.module.userProfile/userprofiledata.48181acd22b3edaebc8a447868a7df7ce629920a-seen)` \(Second consequence\) prevents the conditions from evaluating to `true` for future evaluations.

**Important**: In a production environment, attach the profile write consequence to an IAM result event, not to the show event. IAM consequences are _first-one-wins_, so multiple in-app messages are not displayed when multiple conditions are met across messages. The other consequences are still performed.

```text
{
    "version" : 1,
    "rules" : [
        {
            "condition" : {
                "type" : "group",
                "definition" : {
                    "logic" : "and",
                    "conditions" : [
                        {
                            "type" : "matcher",
                            "definition" : {
                                "key" : "key3",
                                "matcher" : "eq",
                                "values" : ["value5", "value6"]
                            }
                        },
                        {
                            "type" : "matcher",
                            "definition" : {
                                "key"       : "~state.com.adobe.module.userProfile/userprofiledata.48181acd22b3edaebc8a447868a7df7ce629920a-seen",
                                "matcher"   : "nx"
                            }
                        }
                    ]
                }
            },     
            "consequences" : [
                {
                    "id"        : "48181acd22b3edaebc8a447868a7df7ce629920a",
                    "type"      : "iam",
                    "detail"    : {
                        "template"  : "fullscreen",
                        "html"      : "48181acd22b3edaebc8a447868a7df7ce629920a.html"
                    }
                },
                {
                    "id"        : "9d40f5665d5bdbe96dcb3a24f4e4fe98d686a602",
                    "type"      : "csp",
                    "detail"    : {
                        "operation" : "write",
                        "key"       : "48181acd22b3edaebc8a447868a7df7ce629920a-seen",
                        "value"     : "yes"
                    }
                }
            ]
        }
    ]
}
```

## Rules URLs

Since the Rules Engine can support multiple end-point URLs from where to fetch rules, the URLs are prioritized based on the following scheme:

```text
{
   "rules.url" : [
        "https://url/endpoint1",
        "https://url/endpoint2",
        ..
    ]
}
```

The Adobe Experience Platform SDKs process the URLs based on the order in which they are specified. Both endpoints are URLs that point to a zipped rules collection that contains a `rules.json` file, an asset folder that contains images, and HTMLs that are used by the rules. After the rules are downloaded and extracted, the contents of this compressed file are stored in the cache.

## Configuration keys

| Key | Description |
| :--- | :--- |
| `rules.url` | URL that points to the remote file location that contains the rules that were configured for the SDK. |



