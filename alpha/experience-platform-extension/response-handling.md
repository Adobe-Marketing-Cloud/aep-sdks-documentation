# Server response handling

For each Experience Platform event that is sent through the Experience Platform Mobile extension, you can have no, or up to multiple, event handles returned from the Adobe solutions that you enabled. The event handle might contain information, such as personalization data, that can be used in the mobile application views, user profile updates, and so on.

## Response handling

Each event handle that is returned by the server is handled by the Experience Platform extension and is dispatched as a new mobile event to the extensions that are listening for it.

If you integrated the Griffon extension in your mobile application, to display the events in your session, go to <https://griffon.adobe.com/> and in **Search Events**, type `Response event`.

## Error handling

If a server-side error occurs, the Experience Platform extension logs an error/warning message to logcat with the details. This message is dispatched as a new error response event for the mobile extensions to handle.

In Project Griffon, you can view the error response events that were received for your session when you filter by the `Error response event`.

