# Requesting a shared state

Extensions request shared states by using the `ACPExtensionApi` \(iOS\) / `ExtensionApi` \(Android\) interface that is available in the `ACPExtension` \(iOS\) / `Extension` \(Android\) parent class. Extensions can request any of the publicly documented shared states, noting any prerequisites on timing. Generally, a shared state request occurs when an event listener, and the event that was heard, are passed when responding to an event listener callback. This ensures that the state you get back is synchronized with other events in flight at the same time. When your extension dispatches its own events or updates its shared data in response to an event, this synchronization is becomes extremely important.

The example below shows a typical scenario where shared state is requested. In this scenario, a previously registered event listener is called, and the implementation gets the latest configuration shared state passing the current event as context.

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

```objective-c
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

## Public Shared State Constants

Here is a list of the publically shared state constants and when they are available:

`com.adobe.module.configuration`, which is available any time after start up.

**Example Structure**

See the configuration event data example here: [Sample JSON file](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/sdk-core/sample-json-file)

`com.adobe.module.identity`, which is available after receiving a shared state update event where `eventData["stateowner"]=com.adobe.module.identity`.

`com.adobe.module.target`, which is available after receiving a shared state update event where `eventData["stateowner"]=com.adobe.module.target`.

**Note**: A shared state can be `nil` at some point in time, which means that it is in a pending state. If this case occurs, a new shared state update event will be sent when the shared state was updated with valid information.

For example, while sending a network request and waiting for the server response, in order to notify other extensions that the operation is not complete, an extension will set a `nil` shared state and then update it when the server response is received.

**Important**: Do not request and rely on any shared states that are not documented, because their implementation might change.

