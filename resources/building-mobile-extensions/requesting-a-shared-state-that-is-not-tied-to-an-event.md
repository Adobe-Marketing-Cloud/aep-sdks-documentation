# Requesting a shared state that is not tied to an event

Here, extensions can skip passing the `ACPExtensionEvent` \(iOS\) / `Event` \(Android\) parameter to the `getSharedEventState` method. If no state is available, the SDK returns the latest available shared state or a null value.

**Tip:** The caller must be careful to account for null values being passed back.

## iOS

```text
- (void) onUnregister {
    NSError* error = nil;
    NSDictionary* configurationSharedState = [self.api getSharedEventState:@"com.adobe.module.configuration" event:nil error:&error];
    if (configurationSharedState) {
        NSLog(@"The configuration when onUnregister was called was \n:%@", configurationSharedState);
    }
}
```

## Android

```java
@Override
public void onUnregistered() {
    ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
        @Override
        public void error(final ExtensionError extensionError) {
            Log.e("MyExtension", String.format("An error occurred while retrieving the shared state for configuration %d %s", extensionError.getErrorCode(), extensionError.getErrorName()));
        }
    };

    Map<String, Object> configurationSharedState = getApi().getSharedEventState("com.adobe.module.configuration", null, errorCallback);
    Log.d("MyExtension", String.format("Latest configuration was: %s", configurationSharedState));
    ...
}
```

