# Updating a Shared State that is Not Tied to an Event

Here, extensions can skip passing the `ACPExtensionEvent` \(iOS\) / `Event` \(Android\) parameter to the `setSharedEventState` method. The Adobe Cloud Platform SDKs will set the state to be the latest available state for this extension. This process ensures that new events will see this state, but events that are already in flight will have access to the older state if necessary.

## iOS

In the following example, the extension is setting a default state in the `init` method.

```objectivec
- (nullable instancetype) init {
    NSDictionary* newEventData = // construct some JSON
    @{@"customData":@{
        @"customElement":@{
              @"customInt":@(0xDEADBEEF),
            @"customString":@"test"
         }
    }};
    NSError error = nil; 
    if (![self.api setSharedEventState:newEventData event:nil error:&error]) {
        NSLog(@"Error setting default shared state %@:%ld", [error domain], [error code]);
    }
}
```

## Android

In the following example, the extension is setting a default state in constructor.

```java
MyExtension(final ExtensionApi extensionApi) {
        super(extensionApi);

        Map<String, Object> customElement = new HashMap<String, Object>();
        customElement.put("customInt", 125);
        customElement.put("customString", "example");
        Map<String, Object> customData = new HashMap<String, Object>();
        customData.put("customElement", customElement);
        Map<String, Object> newEventData = new HashMap<String, Object>();
        newEventData.put("customData", customData);
        ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
            @Override
            public void error(final ExtensionError extensionError) {
                Log.d("MyExtension", String.format("An error occurred while setting the shared state %d %s", extensionError.getErrorCode(), extensionError.getErrorName()));
            }
        };
        getApi().setSharedEventState(newEventData, null, errorCallback);
        ...
    }
```

