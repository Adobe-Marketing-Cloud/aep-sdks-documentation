# Rules Engine reference

## Key definitions

* **Asset** is an opaque data blob needed by a specific consequence.
* **Condition** is a condition is one boolean equation that evaluates to true or false.
* **Consequence** is the action to be performed if the condition\(s\) evaluate to true.
* **Rule** is a set of conditions and the associated consequence\(s\).

## File Format

Rules and their associated assets will be delivered as a standard ZIP archive, which uses the following format:

* `/`
* `rules.json`
* `assets /` 
* `(asset)`
* `(asset)`

## File Delivery

Delivery will happen by using a request from the Adobe Experience Platform SDKs to a list of static endpoints that are defined as part of the SDK configuration. The SDK supports token expansions on this endpoint, which allows the injection of ECIDs and property IDs into the request.

This request is a conditional `GET` and occurs by default at the start of each new session.

### rules.json format

The rules.json will consist of a root level json object that contains the following elements:

| **Friendly Name** | **Key** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| Version | version | number | **Required**. Version number of the rules.json file format. Should be an integer that increments by 1 for each format change, and the initial version will be 1. |
| Rules | rules | array | **Required**. An array of rules objects. For more information, see [Rule Object Definition](). |

## Rule Object Definition

| **Friendly Name** | **Key** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| Condition | condition | object | **Required**. Holds the definition for the base Condition object for this rule. Each Condition object has a type and can be a Group condition or a Matcher condition. Group conditions contain a logic type, and an array of condition objects. Matcher conditions contain a key, value, and matcher type.   There is one root level condition for a rule. This condition can have any number of nested conditions by using the group construct. For more information, see [Condition Object Definition](). |
| Action | consequences | array | **Required**. Array of Consequence Objects, each containing the details for the associated consequence that will be executed if the associated condition evalutes to `true`. For more information, see [Consequence Object Definition](). |

## Condition Object Definition

Each Condition has a Condition Type and a Definition, and the contents of a Condition's Definition depends on its Condition Type.

A Group-type condition contains an array of conditions, which makes the conditions infinitely nestable.

### Condition Object

| **Friendly Name** | **Key Value** | **Value Type** | **Example** | **Description** |
| :--- | :--- | :--- | :--- | :--- |
| Condition Type | type | string | `"type":"group"` | Indicates the type of the current condition.   The value must be a valid string from the Condition Types. |
| Definition | definition | object | `"definition": { "logic" : "and", "conditions" : [...] }` | Defines how the condition should be evaluated.   The contents of this object will be different depending on the condition type. |

### Condition Types

| **Name** | **Value** | **Description** |
| :--- | :--- | :--- |
| Group | group | This condition is a container, that will hold additional conditions, and the logical evaluator that is used to process those conditions. |
| Matcher | matcher | This condition holds the key, matcher type, and value that should be evaluated. |

### Definition Object \(Condition Type = "group"\)

| **Friendly Name** | **Key Value** | **Value Type** | **Example** | **Description** |
| :--- | :--- | :--- | :--- | :--- |
| Logic Type | logic | string | `"logic":"and"` | Must be a valid Logic Type.   Indicates which logical operator should be used for the Conditions that are defined in the Definition's Conditions array. |
| Conditions | conditions | array | `"conditions":[...]` | An array of Condition objects. |

### Definition Object \(Condition Type = "matcher"\)

**Tip**: The keys used here are different than those used for in-app message matchers.

| **Friendly Name** | **Key** | **Value Type** | **Example** | **Description** |
| :--- | :--- | :--- | :--- | :--- |
| Key | key | string | `"key":"key1"` | Key to get the value in question from the dictionary that is passed as a parameter to the rules processor. |
| Matches | matcher | string | `"matcher":"eq"` | Matcher type that determines the kind of evaluation to use between the two values. |
| Values | values | array | `"values":["value0", "value1"]` | List of values that will be compared \(using OR\) against the value in the parameter dictionary for the `"key"` key. |

### Logic Types

| **Name** | **Value** | **Description** |
| :--- | :--- | :--- |
| AND | and | For this definition to evaluate to `true`, all of its conditions must be true. |
| OR | or | For this definition to evaluate to `true`, only one of its conditions must be true. |

### Matcher Types

| **Name** | **Value** | **Application Type** |
| :--- | :--- | :--- |
| Equals | eq | string, number |
| Not Equals | ne | string, number |
| Exists | eq | string, number |
| Not Exists | ne | string, number |
| Greater Than | gt | number |
| Greater Than or Equals | ge | number |
| Less Than | lt | number |
| Less Than or Equals | le | number |
| Contains | co | string |
| Not Contains | nc | string |
| Starts With | sw | string |
| Ends With | ew | string |

### Matching and Retrieving Values by Keys

By default, keys and the associated values are sourced from the current event that is being processed by the Rules Engine. There are some special key prefixes that can cause the values to be sourced from other locations known to the Adobe Experience Cloud Platform SDKs.

To avoid collisions, special key prefixes always start with `~` to differentiate them from the standard event key names.

| **Key Prefix** | **Example** | **Description** |
| :--- | :--- | :--- |
| ~state. | ~state.sharedStateName/keyName | Reads the `keyName` from the shared state of the module that is stored in `sharedStateName`. |
| ~type | ~type | Reads `eventType` from the triggering event. |
| ~source | ~source | Reads `eventSource` from the triggering event. |
| ~timestampu | ~timestampu | Reads the current device time in epoch format \(seconds since epoch\). |
| ~sdkver | ~sdkver | Reads the current Adobe Experience Platform SDKs version string. |
| ~cachebust | ~cachebust | Generates a random number to be used for cache busting. |
| ~all\_url | ~all\_url | Contains all data in the Event object and is encoded in the `url` format. |
| ~all\_json | ~all\_json | Contains all data in the Event object that is encoded in the `json` format. |

## Simple Conditions:

**Conditions Example 1** represents the following logical condition:

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

**Conditions Example 2** is slightly more complex, and represents the following logical condition:

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

## Consequence Object Definition

The consequences section of a rule lists the file names of each consequence object that should be performed when the condition for that rule evaluates to `true`.

| **Friendly Name** | **Key    Value** | **Type** | **Description** |
| :--- | :--- | :--- | :--- |
| Identifier | id | string | String that contains a unique identifier for this consequence.  `sha1`, or another guaranteed random value with a near-impossible chance of collisions, is recommended. |
| Consequence Type | type | string | A Consequence Type from the [Consequences Type]() table. |
| Consequence Details | detail | object | JSON object that contains the details that are necessary to perform a consequence of the given type. |

## Consequence Types

| **Name** | **Value** | **Description** | **Payload Definition** |
| :--- | :--- | :--- | :--- |
| Analytics | an | Sends data to Analytics |  |
| In-App Message | iam | In-App Message | [In-App Consequence Detail Defintion]() |
| Postback | pb | Send Postback\(s\) | [Postback Consequence Detail Definition]() |
| PII | pii | Sync Pii | [Sync PII Consequence Detail Definition]() |
| Open URL | url | Passes the provided URL to be opened by the platform that is most commonly used for app deeplinking. | [Open URL Consequence Detail Definition]() |
| Callback | cb | Calls a customer-defined method. |  |
| Target | tar | Send a request to Target with location information to enrich the User's profile. |  |
| Audience Manager | aam | Send a request to Audience Manager with location information to enrich the User's profile. |  |
| Client Side Profile | csp | Create/Delete operations against the Client-Side Profile. | [Profile Consequence Detail Definition]() |
| Generate Event | event | Generate a raw event on the event hub. |  |

## rules.json Examples

**Example 1** in a set of rules that will only run when the event was as a result of an Analytics hit or a GPS location event.

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

If the conditions pass, the in-app message will be displayed \(first consequence\), and future display of the message will be prevented by writing/increamenting value to the client side profile:`(~state.com.adobe.module.userProfile/userprofiledata.48181acd22b3edaebc8a447868a7df7ce629920a-seen)` \(second consequence\), which will prevent the conditions from evaluating to `true` for future evaluations.

**Important**: In a production environment, you should attach the profile write consequence to an IAM result event, not to the show event. IAM consequences are first-one-wins, so multiple in-app messages are not displayed when multiple conditions are met across messages. The other consequences will still be performed.

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

The Adobe Experience Platform SDKs process the URLs based on the order in which they are specified. Both endpoints are URLs that point to a zipped rules collection that contains a _rules.json_ file, an asset folder that contains images, and HTMLs that are used by the rules.

After downloading and extracting rules, the contents of this compressed file are stored in the cache. To trigger an update/download of the rules, see [Rules Engine Methods in Android](https://github.com/jiabingeng/sdk-v5-docs/tree/ece930399ffb1a7605b3aa13ed0e6633c8a8a481/rules-engine/rules-api-in-android.md) or [Rules Engine Methods in iOS](https://github.com/jiabingeng/sdk-v5-docs/tree/ece930399ffb1a7605b3aa13ed0e6633c8a8a481/rules-engine/rules-api-in-ios.md).

## Configuration Keys

| Key | Description |
| :--- | :--- |
| rules.url | URL that points to the remote file location that contains the rules that were configured for the SDK. |

