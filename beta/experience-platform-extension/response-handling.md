# Response handling

For each Experience event that is sent through the AEP Edge extension, there can be zero or more event handles returned from the Adobe solutions that you enabled. The response event handle contains relevant information, such as personalization data, that can be used in the mobile application views, user profile updates, and so on.

## Response handling

Each event handle that is returned by the Experience Edge Network is handled by the AEP Edge extension and it is dispatched as a new mobile SDK event.

To see these events in a [Project Griffon session](https://experience.adobe.com/griffon%20), in **Search Events** type `Response event`.

## Error handling

If a server-side error occurs, the Edge extension logs an error/warning message with the error or warning details. For example:

```text
E/AdobeExperienceSDK: NetworkResponseHandler - Received event error for request id (d9058d43-34a9-45f3-815e-b28065185f64), error details:
{
    "code": "global:1",
    "message": "Missing config for configId=testError"
}
```

The message is also dispatched as a new error response event for the mobile extensions to handle.

To see these events in a [Project Griffon session](https://experience.adobe.com/griffon%20), in **Search Events** type `Error response event`.

