# Clearing a shared state

Shared states persist for the life of the application context, which results in the following potential concerns:

* Since data accumulates over time, you must manage the amount of data that you are saving. Currently, a rough guideline is that a maximum of 1000 shared state versions be saved, with each instance being a maximum of 10MB, and overall, a maximum of 1GB of memory consumed. These limits are evaluated over time and might change. To prevent poor app performance, if you exceed these limits, a violation might result in your extension being unregistered.
* If you are storing volatile or sensitive identifiers, you might want to ensure that the identifiers are cleaned up at certain stages, for example, when you unregister yourself.    

**Warning**: You cannot store a user’s personally identifiable information in the shared state.

To manage identifiers, an API is available that clears the existing shared state for your extension without impacting other extensions. The following examples shows you how to call this API in your `onUnregister` \(iOS\) / `onUnregistered` \(Android\) method.

{% tabs %}
{% tab title="Android" %}
## Android

```java
@Override
public void onUnregistered() {
    ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
        @Override
        public void error(final ExtensionError extensionError) {
            Log.d("MyExtension", String.format("An error occurred while clearing the shared states %d %s", extensionError.getErrorCode(), extensionError.getErrorName()));
        }
    };
    getApi().clearSharedEventStates(errorCallback);
}
```
{% endtab %}

{% tab title="Objective-C" %}
## iOS

```text
- (void) onUnregister {
    NSError* error = nil;
    if (![self.api clearSharedEventStates:&error] && error) {
        NSLog(@"Error clearing shared states for extension: %@ %ld", [error domain], [error code]);
    }
}
```
{% endtab %}
{% endtabs %}

