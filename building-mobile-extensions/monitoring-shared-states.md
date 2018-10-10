# Monitoring Shared States

To monitor changes to a shared state, register an event listener by using `registerListener`. You will need to pass a `com.adobe.eventType.hub` event type and a `com.adobe.eventSource.sharedState` event source. This listener will now be called when the shared state changes. To check an extension’s or an internal module’s shared state, you must check the `stateowner` key in the event data.

In the example below, the listener that is being registered in the extension’s init method and the listener implementation where the shared state check is happening is shown. The extension is checking for changes to the `com.adobe.module.target` shared state.

## iOS

### **MyExtension.m**

```objectivec
- (nullable instancetype) init {
  NSError* error = nil;
if ([self.api registerListener: [MyExtensionListener class]
eventType:@"com.adobe.eventType.hub" eventSource:@"com.adobe.eventSource.sharedState" error:&error]) {  
    NSLog(@"MyExtensionListener was registered");
   }
    else {  
      NSLog(@"Error registering MyExtensionListener: %@ %d", [error domain], (int)[error code]);
    }
}
```

### MyExtensionListener.m

```objectivec
- (void) hear: (nonnull ACPExtensionEvent*) event {
  NSDictionary* eventDataDict = [self fromJson:[event eventData]];
  NSString* stateowner = [eventDataDict objectForKey:@"stateowner"];
  if ([stateowner isEqualToString:@"com.adobe.module.target"]) {  
    // do something with the updated target information
  }
}
```

## Android

### MyExtension.java

```java
MyExtension(final ExtensionApi extensionApi) {
    super(extensionApi);
    ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
        @Override
        public void error(final ExtensionError extensionError) {
            Log.e("MyExtension", String.format("An error occurred while registering MySharedStateListener %d %s", extensionError.getErrorCode(), extensionError.getErrorName()));
        }
    };

    getApi().registerEventListener("com.adobe.eventType.hub", "com.adobe.eventSource.sharedState", MySharedStateListener.class, errorCallback);
}
```

### MySharedStateListener.java

```java
@Override
public void hear(final Event event) {
    Map<String, Object> eventData = event.getEventData();
    if (eventData == null) {
        return;
    }

    String stateOwner = (String) eventData.get("stateowner");
    if ("com.adobe.module.target".equals(stateOwner)) {
        // do something with the updated target information
    }
}
```

