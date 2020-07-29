# Response handling

For each Experience Platform event that is sent through the Experience Platform Mobile extension, you can have zero or more event handles returned from the Adobe solutions that you enabled. The event handle might contain information, such as personalization data, that can be used in the mobile application views, user profile updates, and so on.

## Response handling

Each event handle that is returned by the server is handled by the Experience Platform extension and is dispatched as a new mobile event to the extensions that are listening for it.

If you integrated the [Project Griffon extension](https://aep-sdks.gitbook.io/docs/beta/project-griffon) in your mobile application, to display the events in your session, go to [https://experience.adobe.com/griffon](https://experience.adobe.com/griffon) and in **Search Events**, type `Response event`.

## Error handling

If a server-side error occurs, the Experience Platform extension logs an error/warning message with the error or warning details. For example:

```text
E/AdobeExperienceSDK: NetworkResponseHandler - Received event error for request id (d9058d43-34a9-45f3-815e-b28065185f64), error details:
{
    "code": "global:1",
    "message": "Missing config for configId=testError"
}
```

The message is also dispatched as a new error response event for the mobile extensions to handle.

In Project Griffon, you can view the error response events that were received for your session when you filter by the `Error response event`.

