# Updating the shared state

Extensions set a shared state by creating an event data that the extensions save by calling `setSharedEventState` from the `ACPExtensionApi` (iOS) / `ExtensionApi` (Android) interface. This interface is available through the `ACPExtension` (iOS) / `Extension` (Android) parent class. Extensions can only set their own state, so the name that is used is the same as your extension (for example, `com.exampleCompany.extension`). This name is also the name that other extensions need to use when requesting your shared state.

{% tabs %}
{% tab title="Android" %}
## Java

```java
@Override
public void hear(final Event event) {
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
            Log.d("MyListener", String.format("An error occurred while setting the shared state %d %s", extensionError.getErrorCode(), extensionError.getErrorName()));
        }
    };
    getApi().setSharedEventState(newEventData, event, errorCallback);
    ...
}
```
{% endtab %}

{% tab title="iOS" %}
## Objective-C

```objectivec
(void) hear: (nonnull ACPExtensionEvent*) event {
    // construct the data to be shared in a JSON format
    NSDictionary* newEventData =
    @{@"customData":@{
              @"customElement":@{
                      @"customInt":@125,
                      @"customString":@"example"
                      }
              }};
    NSError* error = nil;
    if (![self.extension.api setSharedEventState:newEventData event:event error:&error] && error) {
        NSLog(@"Error setting shared state %@:%ld", [error domain], [error code]);
    }
}
```
{% endtab %}
{% endtabs %}

