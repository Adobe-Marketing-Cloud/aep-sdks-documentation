# Call native code from the Javascript of an in-app message

You can handle events from in-app message interactions natively within your application by completing the following steps:

* [Implement and assign a `MessagingDelegate`](#implement-and-assign-a-messagingdelegate)
* [Register a JavaScript handler for your In-App Message](#register-a-javascript-handler-for-your-in-app-message)
* [Post the JavaScript message from your In-App Message](#post-the-javascript-message-from-your-in-app-message)

### Implement and assign a `MessagingDelegate`

To register a JavaScript event handler with a `Message` object, you will first need to implement and set a `MessagingDelegate`.

For more detailed instructions on implementing and using a MessagingDelegate, please read the [tutorial on using MessagingDelegate](./how-to-messaging-delegate.md).

### Register a JavaScript handler for your In-App Message

{% tabs %}
{% tab title="iOS" %}

In the `shouldShowMessage` function of the `MessagingDelegate`, call [`handleJavascriptMessage(_:withHandler)`](./class-message.md#handlejavascriptmessage_withhandler) to register your handler.

The name of the message you intend to pass from the JavaScript side should be specified in the first parameter.

The below example shows a handler that dispatches an `inapp.interact` Experience Event natively when the JavaScript of the in-app message posts a `myInappCallback` message:

Swift

```swift
func shouldShowMessage(message: Showable) -> Bool {    
    let fullscreenMessage = message as? FullscreenMessage
    let message = fullscreenMessage?.parent

    // in-line handling of JavaScript calls
    message?.handleJavascriptMessage("myInappCallback") { content

        print("JavaScript body passed to native callback: \(content ?? "empty")")

        message?.track(content as? String, withEdgeEventType: .inappInteract)
    }

    return true
}
```

{% endtab %}

{% tab title="Android" %}

{% endtab %}
{% endtabs %}

### Post the JavaScript message from your In-App Message

{% tabs %}
{% tab title="iOS" %}

Now that the in-app message has been displayed, the final step is to post the JavaScript message.

Continuing from the previous example, the developer is going to post the `myInappCallback` message from their HTML, which will in turn call the handler previously configured:

HTML

```html
<html>
    <head>
        <script type="text/javascript">
            function callNative(action) {
                try {
                    // the name of the message handler is the same name that must be registered in native code.
                    // in this case the message name is "myInappCallback"
                    webkit.messageHandlers.myInappCallback.postMessage(action);
                } catch(err) {
                    console.log('The native context does not exist yet'); }
                }
            </script>
    </head>
    <body>
        <button onclick="callNative('native callbacks are cool!')">Native callback!</button>
    </body>
</html>
```

(The above HTML is not representative of a valid in-app message, and is intended only to demonstrate how to post the JavaScript message).

When the user clicks the button inside of this in-app message, the handler configured in the previous step will be called. The handler will send an Experience Event tracking the interaction, and print the following message to the console:

```
JavaScript body passed to native callback: native callbacks are cool!
```

{% endtab %}

{% tab title="Android" %}

{% endtab %}
{% endtabs %}
