# Programmatically control the display of in-app messages

You can now implement a `MessagingDelegate` in order to be alerted when specific events occur during the lifecycle of an in-app message.

{% tabs %}
{% tab title="iOS" %}

### Register the delegate with MobileCore

The `MobileCore` framework maintains an optional property that holds reference to the `MessagingDelegate`.

#### Swift

```swift
/// defined in MobileCore.swift
@objc public static var messagingDelegate: MessagingDelegate?
```

Assuming that `InAppMessagingHandler` is a class that implements `MessagingDelegate`, execute the following code to set the delegate in `MobileCore`:

#### Swift

```swift
let myMessagingDelegate = InAppMessagingHandler()   

MobileCore.messagingDelegate = myMessagingDelegate
```

{% endtab %}

{% tab title="Android" %}

### Register the delegate with the Adobe Service Provider

The `ServiceProvider` class maintains an optional property that holds reference to the `FullscreenMessaageDelegate`.

#### Java

```java
// defined in public class ServiceProvider 
public void setMessageDelegate(FullscreenMessageDelegate messageDelegate)
```

#### Java

```java
CustomDelegate myMessagingDelegate = new CustomDelegate();
ServiceProvider.getInstance().setMessageDelegate(myMessagingDelegate);
```

{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="iOS" %}

### MessagingDelegate protocol (iOS)

The `MessagingDelegate` protocol, which is implemented in the `AEPServices` framework, is defined below:

#### Swift

```swift
/// UI Message delegate which is used to listen for current message lifecycle events
@objc(AEPMessagingDelegate)
public protocol MessagingDelegate {
    /// Invoked when any message is displayed
    /// - Parameters:
    ///     - message: UIMessaging message that is being displayed
    @objc
    func onShow(message: Showable)

    /// Invoked when any message is dismissed
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

{% tab title="Android" %}

### FullscreenMessageDelegate interface (Android)

The `FullscreenMessageDelegate` interface, which is implemented in the Android Messaging extension in the `MessagingDelegate` class, is defined below:

#### Java

```java
/**
 * Delegate for Messaging extension in-app message events.
 */
public interface FullscreenMessageDelegate {
	/**
	 * Invoked when the in-app message is displayed.
	 *
	 * @param message FullscreenMessage the in-app message being displayed
	 */
	void onShow(final FullscreenMessage message);

	/**
	 * Invoked when the in-app message is dismissed.
	 *
	 * @param message FullscreenMessage the in-app message being dismissed
	 */
	void onDismiss(final FullscreenMessage message);

	/**
	 * Used to determine if the in-app message should be shown.
	 *
	 * @param message FullscreenMessage the in-app message that is about to get displayed
	 */
	boolean shouldShowMessage(final FullscreenMessage message);

	/**
	 * Invoked when the in-app message is attempting to load a url.
	 *
	 * @param message FullscreenMessage the in-app message attempting to load the url
	 * @param url     String the url being loaded by the message
	 *
	 * @return True if the core wants to handle the URL (and not the fullscreen message view implementation)
	 */
	boolean overrideUrlLoad(final FullscreenMessage message, final String url);

	/**
	 * Invoked when the in-app message failed to be displayed.
	 */
	void onShowFailure();
}
```

{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="iOS" %}

### Using the Showable object in the protocol methods

Each of the methods implemented in the `MessagingDelegate` will be passed a [`Showable`](https://github.com/adobe/aepsdk-core-ios/blob/main/AEPServices/Sources/ui/Showable.swift) object. In the AEPMessaging SDK, the class implementing `Showable` is [`FullscreenMessage`](https://github.com/adobe/aepsdk-core-ios/blob/main/AEPServices/Sources/ui/fullscreen/FullscreenMessage.swift). A `FullscreenMessage` object is wrapped in the [`Message`](./../public-classes-enums.md) class, and is your primary way to interact with the message.

To get a reference to the `Message` object:

1. Convert the `Showable` message parameter to `FullscreenMessage`
1. Access the `parent` variable (note that `parent` is variable defined in `FullscreenMessage+Message.swift`, an extension in the AEPMessaging framework)

An example of how to access the `Message` in the `onShow` delegate method can be seen below:

#### Swift

```swift
func onShow(message: Showable) {
    let fullscreenMessage = message as? FullscreenMessage
    let message = fullscreenMessage?.parent
    print("message was shown \(message?.id ?? "undefined")")
}
```

{% endtab %}

{% tab title="Android" %}

### Retrieving the Message object from the implemented interface methods

The user interface methods (except for `onShowFailure()`) in a `FullscreenMessageDelegate` implementation will be passed an `AEPMessage` object. An `AEPMessage` object is the Android Core implementation of the `FullscreenMessage` interface. It contains a reference to the parent `Message` class and is your primary way to interact with the message.

A reference to the `AEPMessage` object can be obtained by calling `fullscreenMessage.getParent()` . An example of how to access the `Message` in the `onShow` delegate method can be seen below:

#### Java

```java
@Override
public void onShow(FullscreenMessage fullscreenMessage) {
  Message message = (Message) fullscreenMessage.getParent();
  System.out.println("message was shown: " + message.id);
}
```

{% endtab %}
{% endtabs %}

### Controlling when a message should be shown to the end user

{% tabs %}
{% tab title="iOS" %}

If a `MessagingDelegate` has been provided to `MobileCore`, the delegate's `shouldShowMessage` method will be called prior to displaying an in-app message for which the end user has qualified. You are responsible for returning `true` if the message should be shown, or `false` if the message should be suppressed.

An example of when you may choose to suppress an in-app message due to the status of some other workflow within the app can be seen below:

#### Swift

```swift
func shouldShowMessage(message: Showable) -> Bool {
    if someOtherWorkflowStatus == "inProgress" {
        return false
    }

    return true
}
```

Another option is to store a reference to the `Message` object, and call the `show()` method on it at a later time.

Continuing with the above example, after you have stored the message that was triggered initially, you can choose to show it upon completion of the other workflow:

#### Swift

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

{% tab title="Android" %}

If a custom  `FullscreenMessageDelegate` has been set in the `ServiceProvider`, this delegate's `shouldShowMessage` method will be called prior to displaying an in-app message for which the end user has qualified. You are responsible for returning `true` if the message should be shown, or `false` if the message should be suppressed.

An example of when you may choose to suppress an in-app message due to the status of some other workflow within the app can be seen below:

#### Java

```java
@Override
public boolean shouldShowMessage(FullscreenMessage fullscreenMessage) {
   if (someOtherWorkflowStatus == "inProgress") {
        return false;
    }
    return true;
}
```

Another option is to store a reference to the  `FullscreenMessage` object, and call the `show()` method on it at a later time.

Continuing with the above example, after you have stored the message that was triggered initially, you can choose to show it upon completion of the other workflow:

#### Java

```java
Message currentMessage = null;
String anotherWorkflowStatus;

public void otherWorkflowFinished() {
    anotherWorkflowStatus = "complete";
    currentMessage.show();
}

@Override
public boolean shouldShowMessage(FullscreenMessage fullscreenMessage) {
   if (someOtherWorkflowStatus.equals("inProgress")) {
     // store the current message for later use
     currentMessage = (Message) fullscreenMessage.getParent();
     return false;
   }
  
  return true;
}
```

{% endtab %}
{% endtabs %}

### Integrating the message into an existing UI

{% tabs %}
{% tab title="iOS" %}

If you would like to manually integrate the `View` that contains the UI for an in-app message, you can do so by accessing the `WKWebView` directly in a `MessagingDelegate` method.  

In the example below, you can decide whether or not the in-app message should be directly integrated into your existing UI. If so, you capture a reference to the message's `WKWebView` and return `false` to prevent the message from being shown by the SDK:

#### Swift

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

{% tab title="Android" %}

If you would like to manually integrate the `View` that contains the UI for an in-app message, you can do so by accessing the `WebView` directly in a `MessagingDelegate` method.  

In the example below, you can decide whether or not the in-app message should be directly integrated into your existing UI. If so, you capture a reference to the message's `WebView` and return `false` to prevent the message from being shown by the SDK:

#### Java

```java
private Message currentMessage = null;
private boolean shouldIntegrateMessageDirectly = true;
private MessageWebView inAppMessageView;

@Override
public boolean shouldShowMessage(FullscreenMessage fullscreenMessage) {
  if (shouldIntegrateMessageDirectly) {
    this.currentMessage = (Message) fullscreenMessage.getParent();
    
    // cast to MessageWebView to access the startInAppMessage function
    inAppMessageView = (MessageWebView) currentMessage.getWebView();
    
    return false;
  }
  
  return true;
}
```

{% endtab %}
{% endtabs %}

#### Further reading

* [More information on how to use the Message object](./../public-classes-enums.md)
* [Call native code from the JavaScript of an in-app message](./how-to-call-native-from-javascript.md)
* [Execute JavaScript code in an in-app message from native code](./how-to-call-javascript-from-native.md)
