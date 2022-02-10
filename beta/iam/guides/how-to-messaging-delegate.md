# Programmatically control the display of in-app messages

App developers can now implement a `MessagingDelegate` in order to be alerted when specific events occur during the lifecycle of an in-app message.

### Register the delegate with MobileCore

The `MobileCore` framework maintains an optional property that holds reference to the `MessagingDelegate`.

{% tabs %}
{% tab title="Swift" %}

```swift
/// defined in MobileCore.swift
@objc public static var messagingDelegate: MessagingDelegate?
```

Assuming that `InAppMessagingHandler` is a class that implements `MessagingDelegate`, execute the following code to set the delegate in `MobileCore`:

```swift
let myMessagingDelegate = InAppMessagingHandler()   

MobileCore.messagingDelegate = myMessagingDelegate
```

{% endtab %}

{% tab title="Java" %}

{% endtab %}
{% endtabs %}

### MessagingDelegate protocol

{% tabs %}
{% tab title="Swift" %}

The `MessagingDelegate` protocol, which is implemented in the `AEPServices` framework, is defined below:

```swift
/// UI Message delegate which is used to listen for current message lifecycle events
@objc(AEPMessagingDelegate)
public protocol MessagingDelegate {
    /// Invoked when the any message is displayed
    /// - Parameters:
    ///     - message: UIMessaging message that is being displayed
    @objc
    func onShow(message: Showable)

    /// Invoked when the any message is dismissed
    /// - Parameters:
    ///     - message: UIMessaging message that is being dismissed
    @objc
    func onDismiss(message: Showable)

    /// Used to find whether messages should be shown or not
    /// - Parameters:
    ///     - message: UIMessaging message that is about to get displayed
    /// - Returns: true if the message should be shown else false
    @objc
    func shouldShowMessage(message: Showable) -> Bool

    /// Called when `message` loads a URL
    /// - Parameters:
    ///     - url: the `URL` being loaded by the `message`
    ///     - message: the Message loading a `URL`
    @objc
    optional func urlLoaded(_ url: URL, byMessage message: Showable)
}
```

{% endtab %}

{% tab title="Java" %}

{% endtab %}
{% endtabs %}

### Using the Showable object in the protocol methods

{% tabs %}
{% tab title="Swift" %}

Each of the methods implemented in the `MessagingDelegate` will be passed a [`Showable`](https://github.com/adobe/aepsdk-core-ios/blob/main/AEPServices/Sources/ui/Showable.swift) object.  In the AEPMessaging SDK, the class implementing `Showable` is [`FullscreenMessage`](https://github.com/adobe/aepsdk-core-ios/blob/main/AEPServices/Sources/ui/fullscreen/FullscreenMessage.swift). A `FullscreenMessage` object is wrapped in the [`Message`](./../public-classes-enums.md) class, which is the primary way for the developer to interact with the message.

To get a reference to the `Message` object:

1. Convert the `Showable` message parameter to `FullscreenMessage`
1. Access the `parent` variable (note that `parent` is variable defined in `FullscreenMessage+Message.swift`, an extension in the AEPMessaging framework)

Below is an example of how to access the `Message` in the `onShow` delegate method:

```swift
func onShow(message: Showable) {
    let fullscreenMessage = message as? FullscreenMessage
    let message = fullscreenMessage?.parent
    print("message was shown \(message?.id ?? "undefined")")
}
```

{% endtab %}

{% tab title="Java" %}

{% endtab %}
{% endtabs %}

### Controlling when a message should be shown to the end user

{% tabs %}
{% tab title="Swift" %}

If a `MessagingDelegate` has been provided to `MobileCore`, the delegate's `shouldShowMessage` method will be called prior to displaying an in-app message for which the end user has qualified. The developer is responsible for returning `true` if the message should be shown, or `false` if the message should be suppressed.

Below is an example of when the developer may choose to suppress an in-app message due to the status of some other workflow within the app:

```swift
func shouldShowMessage(message: Showable) -> Bool {
    if someOtherWorkflowStatus == "inProgress" {
        return false
    }

    return true
}
```

Another option for the developer is to store a reference to the `Message` object, and call the `show()` method on it at a later time.

Continuing with the above example, the developer has stored the message that was triggered initially, and chooses to show it upon completion of the other workflow:

```swift
var currentMessage: Message?

func otherWorkflowFinished() {
    anotherWorkflowStatus = "complete"
    currentMessage?.show()
}

func shouldShowMessage(message: Showable) -> Bool {
    if someOtherWorkflowStatus == "inProgress" {        
        let fullscreenMessage = message as? FullscreenMessage

        // store the current message for later use
        currentMessage = fullscreenMessage?.parent

        return false
    }

    return true
}
```

{% endtab %}

{% tab title="Java" %}

{% endtab %}
{% endtabs %}

### Integrating the message into an existing UI

{% tabs %}
{% tab title="Swift" %}

If the developer would like to manually integrate the `View` that contains the UI for an in-app message, they can do so by accessing the `WKWebView` directly in a `MessagingDelegate` method.  

In the below example, the developer decides whether or not the in-app message should be directly integrated into their existing UI.  If so, they capture a reference to the message's `WKWebView` and return `false` to prevent the message from being shown by the SDK:

```swift
var inAppMessageView: WKWebView?

func shouldShowMessage(message: Showable) -> Bool {    
    if shouldIntegrateMessageDirectly {
        let fullscreenMessage = message as? FullscreenMessage
        let message = fullscreenMessage?.parent

        inAppMessageView = message?.view as? WKWebView

        return false
    }

    return true
}
```

{% endtab %}

{% tab title="Java" %}

{% endtab %}
{% endtabs %}

#### Further reading

* [More information on how to use the Message object](./../public-classes-enums.md)
* [Call native code from the Javascript of an in-app message](./how-to-call-native-from-javascript.md)
* [Execute Javascript code in an in-app message from native code](./how-to-call-javascript-from-native.md)
