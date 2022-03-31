# Class - Message

The `Message` class contains the definition of an in-app message and controls its tracking via Experience Edge events.

`Message` objects are only created by the AEPMessaging extension, and passed as the `message` parameter in `MessagingDelegate` protocol methods.

## Public variables

### id

Identifier of the `Message`. This value matches the Message Execution ID assigned by Adobe Journey Optimizer (AJO) Campaign.

{% tabs %}
{% tab title="iOS" %}

#### Swift

```swift
public var id: String
```

{% endtab %}

{% tab title="Android" %}

#### Java

```java
public String id;
```

{% endtab %}
{% endtabs %}

### autoTrack

If set to `true` (default), Experience Edge events will automatically be generated when this `Message` is triggered, displayed, and dismissed.

{% tabs %}
{% tab title="iOS" %}

#### Swift

```swift
public var autoTrack: Bool = true
```

{% endtab %}

{% tab title="Android" %}

#### Java

```java
public boolean autoTrack = true;
```

{% endtab %}
{% endtabs %}

### view

Holds a reference to the message's `WKWebView` (iOS) or `WebView` (Android) instance, if it exists.

{% tabs %}
{% tab title="iOS" %}

#### Swift

```swift
public var view: UIView? {
    fullscreenMessage?.webView
}
```

{% endtab %}

{% tab title="Android" %}

#### Java

```java
public WebView view;
```

{% endtab %}
{% endtabs %}

## Public functions

### show

Signals to the UIService (in `AEPServices`) that the message should be shown.

If `autoTrack` is true, calling this method will result in an "inapp.trigger" Edge Event being dispatched.

{% tabs %}
{% tab title="iOS" %}

#### Swift

```swift
public func show()
```

{% endtab %}

{% tab title="Android" %}

#### Java

```java
public void show()
```

{% endtab %}
{% endtabs %}

### dismiss(suppressAutoTrack:)

Signals to the UIService that the message should be removed from the UI.

If `autoTrack` is true, calling this method will result in an "inapp.dismiss" Edge Event being dispatched.

{% tabs %}
{% tab title="iOS" %}

#### Swift

```swift
public func dismiss(suppressAutoTrack: Bool? = false)
```

###### Parameters

* *suppressAutoTrack* - if set to `true`, the "inapp.dismiss" Edge Event will not be sent regardless of the `autoTrack` setting.

{% endtab %}

{% tab title="Android" %}

#### Java

```java
public void dismiss(final boolean suppressAutoTrack)
```

###### Parameters

* *suppressAutoTrack* - if set to `true`, the "inapp.dismiss" Edge Event will not be sent regardless of the `autoTrack` setting.

{% endtab %}
{% endtabs %}

### track(_:withEdgeEventType:)

Generates and dispatches an Edge Event for the provided `interaction` and `eventType`.

{% tabs %}
{% tab title="iOS" %}

#### Swift

```swift
public func track(_ interaction: String?, withEdgeEventType eventType: MessagingEdgeEventType)
```

###### Parameters

* *interaction* - a custom `String` value to be recorded in the interaction
* *eventType* - the [`MessagingEdgeEventType`](#enum-messagingedgeeventtype) to be used for the ensuing Edge Event

{% endtab %}

{% tab title="Android" %}

#### Java

```java
public void track(final String interaction, final MessagingEdgeEventType eventType)
```

###### Parameters

* *interaction* - a custom `String` value to be recorded in the interaction
* *eventType* - the [`MessagingEdgeEventType`](#enum-messagingedgeeventtype) to be used for the ensuing Edge Event

{% endtab %}
{% endtabs %}

### handleJavascriptMessage(_:withHandler:)

Adds a handler for named JavaScript messages sent from the message's `WKWebView`.

The parameter passed to `handler` will contain the body of the message passed from the `WKWebView`'s JavaScript.

For a full guide on how to use `handleJavascriptMessage`, read [Call native code from the Javascript of an in-app message](./guides/how-to-call-native-from-javascript.md).

{% tabs %}
{% tab title="iOS" %}

#### Swift

```swift
public func handleJavascriptMessage(_ name: String, withHandler handler: @escaping (Any?) -> Void)
```

###### Parameters

* *name* - the name of the message that should be handled by `handler`
* *handler* - the method or closure to be called with the body of the message created in the Message's JavaScript

{% endtab %}

{% tab title="Android" %}

#### Java

```java
public void handleJavascriptMessage(final String name, final AdobeCallback<String> callback)
```

###### Parameters

* *name* - the name of the message that should be handled by the `callback`
* *callback* - a callback which will be called with the body of the message created in the Message's JavaScript

{% endtab %}
{% endtabs %}

# Enum - MessagingEdgeEventType

Provides mapping to XDM EventType strings needed for Experience Event requests.

This enum is used in conjunction with the [`track(_:withEdgeEventType:)`](#track_withedgeeventtype) method of a `Message` object.

### Definition

{% tabs %}
{% tab title="iOS" %}

#### Swift

```swift
@objc(AEPMessagingEdgeEventType)
public enum MessagingEdgeEventType: Int {
    case inappDismiss = 0
    case inappInteract = 1
    case inappTrigger = 2
    case inappDisplay = 3
    case pushApplicationOpened = 4
    case pushCustomAction = 5

    public func toString() -> String {
        switch self {
        case .inappDismiss:
            return MessagingConstants.XDM.IAM.EventType.DISMISS
        case .inappTrigger:
            return MessagingConstants.XDM.IAM.EventType.TRIGGER
        case .inappInteract:
            return MessagingConstants.XDM.IAM.EventType.INTERACT
        case .inappDisplay:
            return MessagingConstants.XDM.IAM.EventType.DISPLAY
        case .pushCustomAction:
            return MessagingConstants.XDM.Push.EventType.CUSTOM_ACTION
        case .pushApplicationOpened:
            return MessagingConstants.XDM.Push.EventType.APPLICATION_OPENED
        }
    }
}
```

{% endtab %}

{% tab title="Android" %}

#### Java

```java
public enum MessagingEdgeEventType {
    IN_APP_DISMISS(0),
    IN_APP_INTERACT(1),
    IN_APP_TRIGGER(2),
    IN_APP_DISPLAY(3),
    PUSH_APPLICATION_OPENED(4),
    PUSH_CUSTOM_ACTION(5);

    final int value;

    MessagingEdgeEventType(final int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }

    @Override
    public String toString() {
        switch (this) {
            case IN_APP_DISMISS:
                return MessagingConstants.EventDataKeys.Messaging.IAMDetailsDataKeys.EventType.DISMISS;
            case IN_APP_INTERACT:
                return MessagingConstants.EventDataKeys.Messaging.IAMDetailsDataKeys.EventType.INTERACT;
            case IN_APP_TRIGGER:
                return MessagingConstants.EventDataKeys.Messaging.IAMDetailsDataKeys.EventType.TRIGGER;
            case IN_APP_DISPLAY:
                return MessagingConstants.EventDataKeys.Messaging.IAMDetailsDataKeys.EventType.DISPLAY;
            case PUSH_APPLICATION_OPENED:
                return MessagingConstants.EventDataKeys.Messaging.PushNotificationDetailsDataKeys.EventType.OPENED;
            case PUSH_CUSTOM_ACTION:
                return MessagingConstants.EventDataKeys.Messaging.PushNotificationDetailsDataKeys.EventType.CUSTOM_ACTION;
            default:
                return super.toString();
        }
    }
```

{% endtab %}
{% endtabs %}

### String values

Below is the table of values returned by calling the `toString` method for each case, which are used as the XDM `eventType` in outgoing experience events:

{% tabs %}
{% tab title="iOS" %}

| Case                  | String value                     |
|-----------------------|----------------------------------|
| inappDismiss          | `inapp.dismiss`                  |
| inappInteract         | `inapp.interact`                 |
| inappTrigger          | `inapp.trigger`                  |
| inappDisplay          | `inapp.display`                  |
| pushApplicationOpened | `pushTracking.applicationOpened` |
| pushCustomAction      | `pushTracking.customAction`      |

{% endtab %}

{% tab title="Android" %}

| Case                    | String value                     |
| ----------------------- | -------------------------------- |
| IN_APP_DISMISS          | `inapp.dismiss`                  |
| IN_APP_INTERACT         | `inapp.interact`                 |
| IN_APP_TRIGGER          | `inapp.trigger`                  |
| IN_APP_DISPLAY          | `inapp.display`                  |
| PUSH_APPLICATION_OPENED | `pushTracking.applicationOpened` |
| PUSH_CUSTOM_ACTION      | `pushTracking.customAction`      |

{% endtab %}
{% endtabs %}
