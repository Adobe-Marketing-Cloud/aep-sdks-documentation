# Custom Validation

## Overview

You may use the Custom Validation feature to quickly and easily write a JavaScript function to validate events in a Project Griffon session.

## Getting Started

To use this view, complete the following steps:

1. [Setup Project Griffon](../set-up-project-griffon.md)
2. [Create](./#creating-sessions) and [connect](./#connecting-to-a-session) to a Project Griffon session
3. In the **Home** view, select **Validation Scripts**

![Custom Validation](../../../.gitbook/assets/validation_menu.png)

## Writing a Validation Function

This feature allows you to write a function to validate events in your Project Griffon session. The function should expect an array of Project Griffon events and should return:

* A boolean \(true or false\) OR
* An object that contains a `status` property with an _optional_ array of event UUIDs

### Event Definition

| Key | Type | Description |
| :--- | :--- | :--- |
| `uuid` | String | Universally unique identifier for the event. |
| `timestamp` | Number | Timestamp from the device when the event was sent from the SDK. |
| `eventNumber` | Number | Used to order when the event was sent. This key is useful when events have the same timestamp. |
| `vendor` | String | Vendor identification string in the reverse domain name format \(for example, com.adobe.griffon\). |
| `type` | String | Used to denote the type of event. |
| `payload` | Object | Defines the data for the event and contains unique and common properties. Some common properties include `ACPExtensionEventSource and ACPExtensionEventType`. |
| `annotations` | Array | An array of annotation objects. |

### Annotation Definition

| Key | Type | Description |
| :--- | :--- | :--- |
| `uuid` | String | Universally unique identifier for the annotation. |
| `type` | String | Used to denote the type of annotation and is usually the name of the plugin \(for example, analytics\). |
| `payload` | Object | Defines the data that should supplement the event. For Adobe Analytics, this is where the post-processed hit data is contained. |

### Returning Validation Results

To execute the code in the code editor, click **Validate**. The function should return a boolean \(true or false\) or an object that contains a status property and optionally an array of event UUIDs.

| Key | Type | Description |
| :--- | :--- | :--- |
| `status` | boolean | Indicates whether the events being evaluated are valid \(true\) or invalid \(false\). |
| `events` | Array | \(Optional\) An array of event UUIDs. If provided with an invalid status, an event list displays the relevant events. |

![](../../../.gitbook/assets/griffon-custom-validation-invalid.png)

## Script Management

When the view is first loaded, it provides an empty function with JSDoc comments that define how the function accepts the events parameter with the expected return output. Currently, the view allows you to manage several validation scripts by leveraging the browser's cache.

You can create a new validation script by editing the existing script’s name in the drop-down list. To save or delete the script, click **Save** or **Delete**.

![](../../../.gitbook/assets/griffon-custom-validation-save.png)

## Troubleshooting

If an error occurs in the JavaScript code editor, an `ERROR` status is displayed, and the reason for the error is output to the browser's developer console.

Additionally, you can also reach out to our team on our Slack Channel at [https://projectgriffon.slack.com/](https://projectgriffon.slack.com/)

