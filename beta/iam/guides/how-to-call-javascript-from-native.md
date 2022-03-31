# Execute JavaScript code in an in-app message from native code

{% tabs %}
{% tab title="iOS" %}

You can execute JavaScript in an in-app message from native code by completing the following steps:

* [Implement and assign a `MessagingDelegate`](#implement-and-assign-a-messagingdelegate)
* [Obtain a reference to the `WKWebView`](#obtain-a-reference-to-the-wkwebview)
* [Call the JavaScript method](#call-the-JavaScript-method)

### Implement and assign a `MessagingDelegate`

To register a JavaScript event handler with a `Message` object, you will first need to implement and set a `MessagingDelegate`.

For more detailed instructions on implementing and using a MessagingDelegate, please read the [tutorial on using MessagingDelegate](./how-to-messaging-delegate.md).

### Obtain a reference to the `WKWebView`

In the `shouldShowMessage` function of the `MessagingDelegate`, get a reference to the `WKWebView` used by the message.  

#### Swift

```swift
func shouldShowMessage(message: Showable) -> Bool {
    // access to the whole message from the parent
    let fullscreenMessage = message as? FullscreenMessage
    let message = fullscreenMessage?.parent

    let messageWebView = message?.view as? WKWebView

    ...
}
```

### Call the JavaScript method

With a reference to the `WKWebView`, the instance method `evaluateJavaScript(_:completionHandler:)` can now be leveraged to call a JavaScript method.

Further details of this API are explained in the [Apple documentation](https://developer.apple.com/documentation/webkit/wkwebview/1415017-evaluateJavaScript) - the example below is provided for the purpose of demonstration:

#### Swift

```swift
func shouldShowMessage(message: Showable) -> Bool {
    // access to the whole message from the parent
    let fullscreenMessage = message as? FullscreenMessage
    let message = fullscreenMessage?.parent

    let messageWebView = message?.view as? WKWebView
    messageWebView?.evaluateJavaScript("startTimer();") { result, error in
        if error != nil {
            // handle error
            return
        }

        if result != nil {
            // do something with the result
        }
    }

    ...
}
```

{% endtab %}

{% tab title="Android" %}

You can execute JavaScript in an in-app message from native code by completing the following steps:

* [Implement and assign a `MessagingDelegate`](#android_messaging_delegate)
* [Obtain a reference to the `WebView`](#android_webview)
* [Call the JavaScript method](#android_call_javascript)

### Implement and assign a `MessagingDelegate`<a name="android_messaging_delegate"></a>

To register a JavaScript event handler with a `Message` object, you will first need to implement and set a `MessagingDelegate`.

For more detailed instructions on implementing and using a MessagingDelegate, please read the [tutorial on using MessagingDelegate](./how-to-messaging-delegate.md).

### Obtain a reference to the `WebView`<a name="android_webview"></a>

In the `shouldShowMessage` function of the `MessagingDelegate`, get a reference to the  `WebView` created for Javascript interactions.  

#### Java

```java
@Override
public boolean shouldShowMessage(FullscreenMessage fullscreenMessage) {
  // access to the whole message from the parent
  Message message = (Message) fullscreenMessage.getParent();
      
  WebView webView = message.view;
  
  ...
}
```

### Call the JavaScript method<a name="android_call_javascript"></a>

With a reference to the `WebView`, the instance method `public void evaluateJavascript(@NonNull String script, @Nullable ValueCallback<String> resultCallback)` can now be leveraged to call a JavaScript method.

Further details of this API are explained in the [Android documentation](https://developer.android.com/reference/android/webkit/WebView#evaluateJavascript(java.lang.String,%20android.webkit.ValueCallback%3Cjava.lang.String%3E)) - the example below is provided for the purpose of demonstration:

#### Java

```java
@Override
public boolean shouldShowMessage(FullscreenMessage fullscreenMessage) {
  // access to the whole message from the parent
  Message message = (Message) fullscreenMessage.getParent();
      
  WebView webView = message.view;
  // webview operations must be run on the ui thread
  webView.post(new Runnable() {
    @Override
    public void run() {
      webView.evaluateJavascript("startTimer()", new ValueCallback<String>() {
        @Override
        public void onReceiveValue(String s) {
          // do something with the content
        }
      });
    }
  });
  
  ...
}
```

{% endtab %}
{% endtabs %}
