# Handle URL clicks from an in-app message

When a link is clicked in an in-app message, the `FullscreenMessageDelegate` is responsible for handling behavior.

If the scheme used in the link **is not** `adbinapp://`, the link will open in the containing WebView (default behavior).

If the scheme used in the link **is** `adbinapp://`, the following behavior may occur:

* The in-app message is dismissed
* An interaction event is sent to Experience Edge
* The URL will be opened by the OS, potentially resulting in:
  * The link being opened by the device's default web browser
  * Opening of a deeplink

### Dismiss the in-app message

In order for the SDK to remove the view containing an in-app message from the UI, the clicked link must have a host of `dismiss`.

The example below is a link that will dismiss the current in-app message:

```
adbinapp://dismiss
```

### Send a message interaction event to Experience Edge

Adding a URL variable named `interaction` will cause the SDK to send an Experience Event to the Adobe Experience Edge.

The example below will dismiss the current in-app message and send an `inapp.interact` event to edge with an action of `imageLiked`:

```
adbinapp://dismiss?interaction=imageLiked
```

### Open a link from the URL

If the value for a URL variable named `link` contains a valid URL, the SDK will open the link using the OS-defined API.

##### Open location in the default web browser

If the provided URL does not contain a custom scheme, the URL will be loaded in the device's default web browser.  

The example below will dismiss the current in-app message, send an `inapp.interact` event to edge with an action of `adobe`, and open the adobe.com website in mobile Safari (the default browser on the user's iOS device):

```
adbinapp://dismiss?interaction=adobe&link=https://adobe.com
```

##### Open a deeplink

If the provided URL contains a custom scheme, the app that handles the custom scheme will be launched.

The example below will dismiss the current in-app message, then launch an app owned by the same developer which handles the scheme `myAppScheme`:

```
adbinapp://dismiss?link=myAppScheme://deeplinked
```
