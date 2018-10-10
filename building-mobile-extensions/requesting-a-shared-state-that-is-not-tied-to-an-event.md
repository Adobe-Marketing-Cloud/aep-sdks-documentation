# Requesting a Shared State that is Not Tied to an Event

Here, extensions can skip passing the `ACPExtensionEvent` \(iOS\) / `Event` \(Android\) parameter to the `getSharedEventState` method. If no state is available, the SDK returns the latest available shared state or a null value.

**Tip:** The caller must be careful to account for null values being passed back.

## iOS

```objectivec
- (void) onUnregister {
  NSString* configuration = [self.extension.api
  getSharedEventState:@"com.adobe.module.configuration" event:nil];
  if(configuration) {
    NSLog(@"The configuration when onUnregister was called was \n:%@", configuration);
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

