# Requesting a shared state

Extensions request shared states by using the `ACPExtensionApi` \(iOS\) / `ExtensionApi` \(Android\) interface that is available in the `ACPExtension` \(iOS\) / `Extension` \(Android\) parent class. Extensions can request any of the publicly documented shared states, noting any prerequisites on timing. Generally, a shared state request occurs when an event listener, and the event that was heard, are passed when responding to an event listener callback. This ensures that the state that is returned is synchronized with other events in flight at the same time. When your extension dispatches its own events or updates, or its shared data in response to an event, this synchronization is becomes extremely important.

The example below shows a typical scenario where shared state is requested. A previously registered event listener is called, and the implementation gets the latest configuration shared state by passing the current event as context.

{% tabs %}
{% tab title="Android" %}
### Android

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

{% tab title="Objective-C" %}
### iOS

```text
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

Here is the shared state constant:

`com.adobe.module.configuration`, which is available any time after start up.

**Example structure**

To see a configuration event data example, go to [Sample JSON file](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/sdk-core/sample-json-file).

`com.adobe.module.identity`, which is available after receiving a shared state update event where `eventData["stateowner"]=com.adobe.module.identity`.

`com.adobe.module.target`, which is available after receiving a shared state update event where `eventData["stateowner"]=com.adobe.module.target`.

A shared state can be `nil` at some point in time, which means that it is in a pending state. When this occurs, a new shared state update event is sent when the shared state is updated with valid information. For example, when a network request is sent, and you are waiting for the server response. To notify other extensions that the operation is not complete, an extension sets a `nil` shared state and then updates the state when the server response is received.

**Important**: Do not request and rely on shared states that are not documented, because their implementation might change.

