# Rules Engine technical details

## Key definitions

* A condition is a boolean equation that evaluates to `true` or `false`.

* A consequence is the action to be performed when the trigger is met and the condition\(s\) evaluates to `true`.

* A rule is a set of conditions and the associated consequence\(s\).

* A triggering event is the event that started the rule evaluation. 

  The Adobe Experience Platform Mobile SDK evaluates each rule configured in Experience Platform Launch for the current event that is processed by the Event Hub.

* Rules Engine is the system that processes the mobile rules that were configured in Experience Platform Launch and initiates the associated actions when the conditions are met.

* An asset is an opaque data blob that is needed by a specific consequence.

## Rules delivery

Rules delivery occurs by using a network request from the Experience Platform SDKs to a static endpoint that is defined as part of the SDK configuration. The rules file for each mobile property is hosted on https://assets.adobedtm.com.

This request is a conditional `GET` and occurs by default at the start of each new application session. In Experience Platform Launch, when the set of rules that were configured for a mobile property change, these changes will be picked up by the Experience Platform SDK in the next session or after the application is restarted.

## File format

Rules are delivered as a standard ZIP archive, which contains a `rules.json` file. This file consists of a root-level JSON object that contains the following elements:

| **Friendly name** | **Key** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| Version | `version` | number | *(Required)* Version number of the `rules.json` file format. Should be an integer that increments by 1 for each format change, and the initial version is 1. |
| Rules | `rules` | array | *(Required)* An array of rules objects. For more information, see [Rule object definition](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#rule-object-definition). |

## Rule object definition

| **Friendly name** | **Key** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| Condition | `condition` | object | *(Required)* Holds the definition for the base Condition object for this rule. Each Condition object can be a Group or a Matcher condition type. Group conditions contain a logic type and an array of condition objects. Matcher conditions contain a key, value, and a matcher type. There is one root-level condition for a rule, and this condition can have any number of nested conditions by using the group construct. For more information, see [Condition object definition](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-object-definition). |
| Action | `consequences` | array | *(Required)* Array of consequence objects, where each object contains the details for the associated consequence that are executed when the associated condition evaluates to `true`. For more information, see [Consequence object definition](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-object-definition). |

## Condition object definition

Each Condition has a condition type and a definition, and the contents of a condition's definition depends on its condition type.

A Group condition contains an array of conditions, which makes the conditions infinitely nestable.

### Condition object

| **Friendly name** | **Key** | **Type** | **Example** | **Description** |
| :--- | :--- | :--- | :--- | :--- |
| Condition type | `type` | string | `"type":"group"` | Indicates the type of the current condition. The value must be a valid string from the [Condition types](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#condition-types). |
| Definition | `definition` | object | `"definition": { "logic" : "and", "conditions" : [...] }` | Defines how the condition should be evaluated, and the contents of this object will be different depending on the condition type. |

### Condition types

| **Name** | **Value** | **Description** |
| :--- | :--- | :--- |
| Group | `group` | This condition is a container that holds additional conditions, and the logical evaluator that is used to process those conditions. |
| Matcher | `matcher` | This condition holds the key, matcher type, and value that should be evaluated. |

### Definition object 

#### Group condition type

| **Friendly name** | **Key** | **Type** | **Example** | **Description** |
| :--- | :--- | :--- | :--- | :--- |
| Logic type | `logic` | string | `"logic":"and"` | Must be a valid Logic type and indicates which logical operator should be used for the conditions that are defined in the definition's conditions array. |
| Conditions | `conditions` | array | `"conditions":[...]` | An array of Condition objects. |

#### Matcher condition type

{% hint style="info" %}

The keys that are used here are different than those used for In-App message matchers.

{% endhint %}

| **Friendly name** | **Key** | **Type** | **Example** | **Description** |
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

By default, keys and the associated values are sourced from the current event that is being processed by the Rules Engine. There are also some special key prefixes that can cause the values to be sourced from other locations that are known to the Experience Platform SDKs. 

To avoid collisions, special key prefixes always start with a `~` (tilde) to differentiate them from the standard event key names.

| **Key prefix** | **Example** | **Description** |
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

The consequences section of a rule lists the file names of each consequence object that should be performed when all of the conditions for that rule evaluate to `true`.

| **Friendly name** | **Key** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| Identifier | `id` | string | *(Required)* String that contains a unique identifier for this consequence.  `sha1`, or another guaranteed random value with a near-impossible chance of collisions, is recommended. |
| Consequence type | `type` | string | *(Required)* A Consequence Type from the [Consequences Type](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/rules-engine#consequence-types) table. |
| Consequence details | `detail` | object | *(Required)* JSON object that contains the details that are necessary to perform a consequence of the given type. |

## Consequence types

| **Name** | **Value** | **Description** | **Payload Definition** |
| :--- | :--- | :--- | :--- |
| Analytics | `an` | Sends data to Analytics | [Analytics consequence detail definition](rules-engine-consequence-details.md#analytics-consequence). |
| In-App Message | `iam` | In-App Message | [In-App consequence detail definition](rules-engine-consequence-details.md#in-app-message-consequence). |
| Postback | `pb` | Send Postback\(s\) to a third-party URL | [Postback consequence detail definition](rules-engine-consequence-details.md#postback-consequence). |
| PII | `pii` | Sync PII with an https URL | [Sync PII consequence detail definition](rules-engine-consequence-details.md#sync-pii-consequence). |
| Open URL | `url` | Passes the provided URL to be opened by the platform that is most commonly used for app deep linking. | [Open URL consequence detail definition](rules-engine-consequence-details.md#open-url-consequence). |
| Client Side Profile | `csp` | Create or delete operations against the client-side profile. | [Profile consequence detail definition](rules-engine-consequence-details.md#profile-consequence). |
| Attach Data | `add` | Attaches key-value pairs to the EventData of an existing Event | [Attach data consequence detail definition](rules-engine-consequence-details.md#attach-data-consequence). |

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

## Rules URL

The Rules Engine requires an endpoint URL to be configured in the configuration, which specifies the location from where rules should be fetched:

```text
{
   "rules.url" : "https://assets.adobedtm.com/example.zip"
}
```

The Adobe Experience Platform SDKs process the URL that points to a zipped rules collection, and this collection contains a `rules.json` file. After the rules are downloaded and extracted, the contents of this compressed file are stored in the cache.

## Configuration keys

| Key | Description |
| :--- | :--- |
| `rules.url` | URL that points to the remote file location that contains the rules that were configured for the Mobile SDKs. For more information, see [Rules URL](#rules-url). |
