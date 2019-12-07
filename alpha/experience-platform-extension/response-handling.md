# Server response handling

For each Experience platform event sent through the Adobe Experience Platform mobile extension, one, multiple or no event handles can be returned from the Adobe solutions you have enabled. The event handle may contain information like: personalization data that can be used in the mobile application views, user profile updates, etc.

## Response handling

Each event handle returned by the server is handled by the AEP extension and dispatched as a new Mobile event to the extensions that are listening for it. 

If you integrated the Griffon extension in your mobile application you can view the events in your session at https://griffon.adobe.com/, filtering by `Response event` in the **Search Events** text box.

## Error handling

In the eventuality of an error encountered server side for the events being sent, the AEP extension logs an error/warning message to logcat with the received error message details. The same error message will be dispatched as a new error response event for the mobile extensions to handle. 

By using project Griffon, you can view the Error response events received in your session when filtering by `Error response event` in the **Search Events** text box in the session view.

