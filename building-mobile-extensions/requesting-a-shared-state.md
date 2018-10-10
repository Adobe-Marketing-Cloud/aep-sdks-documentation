# Requesting a Shared State

Extensions request shared states by using the `ACPExtensionApi` \(iOS\) / `ExtensionApi` \(Android\) interface that is available in the `ACPExtension` \(iOS\) / `Extension` \(Android\) parent class. Extensions can request any of the publicly documented shared states, noting any prerequisites on timing. Generally, a shared state request occurs when an event listener, and the event that was heard, are passed when responding to an event listener callback. This ensures that the state you get back is synchronized with other events in flight at the same time. When your extension dispatches its own events or updates its shared data in response to an event, this synchronization is becomes extremely important.

The example below shows a typical scenario where shared state is requested. In this scenario, a previously registered event listener is called, and the implementation gets the latest configuration shared state passing the current event as context.

### iOS

```objectivec
- (void) hear: (nonnull ACPExtensionEvent*) event {
  NSString* configuration = [self.extension.api getSharedEventState:@"com.adobe.module.configuration" event:event];
  if(configuration) {
    NSLog(@"The configuration when event \"%@\" was sent was:\n%@", [event eventName], configuration);
  }
}
```

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

## Public Shared State Constants

Here is a list of the publically shared state constants and when they are available:

`com.adobe.module.configuration`, which is available any time after start up.

**Example Structure**

See the configuration event data example here: [Sample JSON file](https://launch.gitbook.io/marketing-mobile-sdk-v5-by-adobe-documentation/sdk-core/sample-json-file)

`com.adobe.module.identity`, which is available after receiving a shared state update event where `eventData["stateowner"]=com.adobe.module.identity`.

`com.adobe.target`, which is available after receiving a shared state update event where `eventData["stateowner"]=com.adobe.module.target`.

**Important**: Do not request and rely on any shared states that are not documented, because their implementation might change.

