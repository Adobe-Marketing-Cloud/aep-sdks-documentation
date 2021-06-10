# Interacting with rules

Rules are defined in the Experience Platform Launch interface and can include data elements, events, conditions, and actions provided by extensions.

## Publishing rules support for Experience Platform Launch

Your extension should publish the rules support that it provides to Experience Platform Launch. You can provide this support through the `extension.json` file in your extensions base directory.

### Publishing supported data elements

Data elements can be supported by publishing the shared state keys that you want to use in a rule. For more information, see the Launch documentation on [data element types](https://developer.adobelaunch.com/extensions/reference/data-element-types/).

```json
  "dataElements": [
    {
      "displayName": "My Custom Value",
      "name": "customValue",
      "schema": {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "type": "object",
        "allOf": [{
          "$ref": "https://assets.adobedtm.com/activation/reactor/schemas/1.0/extension-definitions-mobile.json#/definitions/dataElement"
        }]
      },
    }
  ]
```

### Publishing supported conditions

Conditions can be supported by publishing the shared state keys or events that you want to use in a rule. For more information, see the Launch documentation on [condition types](https://developer.adobelaunch.com/extensions/reference/condition-types/).

```json
    "events":[
    {
      "displayName": "My Custom Event",
      "name": "triggerEvent",
      "schema": {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "type": "object",
        "allOf": [{
          "$ref": "https://assets.adobedtm.com/activation/reactor/schemas/1.0/extension-definitions-mobile.json#/definitions/events"
        }]
      }
    }],
    "conditions":[
    {
      "displayName": "My Custom Condition",
      "name": "triggerCondition",
      "schema": {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "type": "object",
        "allOf": [{
          "$ref": "https://assets.adobedtm.com/activation/reactor/schemas/1.0/extension-definitions-mobile.json#/definitions/conditions"
        }]
      }
    }]
```

### Publishing supported actions

Conditions can be supported by publishing the events that you want to use in a rule. For more information, see the Launch documentation on [action types](https://developer.adobelaunch.com/extensions/reference/action-types/).

```json
    "actions": [
    {
      "displayName": "My Custom Action",
      "name": "com.myCompany.eventType.doSomeWork",
      "schema": {
        "$schema": "http://json-schema.org/draft-04/schema#",
        "type": "object",
        "properties": {},
        "allOf": [{
          "$ref": "https://assets.adobedtm.com/activation/reactor/schemas/1.0/extension-definitions-mobile.json#/definitions/consequence"
        }]
      },
    }]
```

## Supporting rules at runtime

You should provide support for the events, actions, and conditions that you published to Experience Platform Launch at runtime.

### Publishing a shared state `condition` at runtime

A shared state that was published by your extension can be used as a `condition` when configuring a rule in Experience Platform Launch. To learn how you can publish a shared state, see the [updating the shared state document](https://aep-sdks.gitbook.io/docs/resources/building-mobile-extensions/updating-the-shared-state).

### Dispatching an event `condition` at runtime

An event that was dispatched by your extension can be used as a `condition` when configuring a rule in Experience Platform Launch. To learn how you can dispatch an event, see the [dispatching events from your extension document](https://aep-sdks.gitbook.io/docs/resources/building-mobile-extensions/dispatching-events-from-your-extension).

### Handling an event `action` at runtime

For an event that your extension registered, a listener for can be used as an `action` when configuring a rule in Experience Platform Launch. To learn how you can register a listener for your events, see the [listening for events document](https://aep-sdks.gitbook.io/docs/resources/building-mobile-extensions/event-listeners).

