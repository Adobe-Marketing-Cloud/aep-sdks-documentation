# Requesting a shared state

Extensions request shared states by using the `ACPExtensionApi` \(iOS\) / `ExtensionApi` \(Android\) interface that is available in the `ACPExtension` \(iOS\) / `Extension` \(Android\) parent class. Extensions can request any of the publicly documented shared states, noting any prerequisites on timing. Generally, a shared state request occurs when an event listener and the event that was heard are passed when responding to an event listener callback. This ensures that the state that is returned is synchronized with other events in flight at the same time. When your extension dispatches its own events or updates, or its shared data in response to an event, this synchronization is becomes extremely important.

The following example shows a typical scenario where shared state is requested. A previously registered event listener is called, and the implementation gets the latest configuration shared state by passing the current event as context.

{% tabs %}
{% tab title="Android" %}
## Java

```java
@Override
public void hear(final Event event) {
    ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
        @Override
        public void error(final ExtensionError extensionError) {
            Log.e("MyListener", String.format("An error occurred while retrieving the shared state for configuration %d %s", extensionError.getErrorCode(), extensionError.getErrorName()));
        }
    };

    Map<String, Object> configurationSharedState = parentModule.getSharedEventState("com.adobe.module.configuration", event, errorCallback);
    Log.d("MyListener", String.format("The configuration when event %s was sent was: %s", event.getName(), configurationSharedState));
    ...
}
```
{% endtab %}

{% tab title="iOS" %}
## Objective-C

```objectivec
- (void) hear: (ACPExtensionEvent*) event {
    NSError* error = nil;
    NSDictionary* configurationSharedState = [[[self extension] api] getSharedEventState:@"com.adobe.module.configuration" event:event error:&error];
    if (configurationSharedState) {
        NSLog(@"The configuration when event \"%@\" was sent was:\n%@", event.eventName, configurationSharedState);
    }
}
```
{% endtab %}
{% endtabs %}

## Public shared state constants

An example of a shared state constant is `com.adobe.module.configuration`, which is available any time after start up.

**Example structure**

To see a sample configuration event data, please refer to the sample JSON file in the [Mobile Core extension configuration document](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/mobile-core/configuration#sample-configuration).

`com.adobe.module.identity` is available after receiving a shared state update event where `eventData["stateowner"]=com.adobe.module.identity`.

`com.adobe.module.target` is available after receiving a shared state update event where `eventData["stateowner"]=com.adobe.module.target`.

A shared state can be `nil` at some point in time, which means that it is in a pending state. When this occurs, a new shared state update event is sent when the shared state is updated with valid information. An example of this would be when a network request is sent, and you are waiting for the server response. To notify other extensions that the operation is not complete, an extension sets a `nil` shared state and then updates the state when the server response is received.

{% hint style="warning" %}
Do not request and rely on shared states that are not documented, because their implementation might change.
{% endhint %}

