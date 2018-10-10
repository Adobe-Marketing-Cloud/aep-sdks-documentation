# Dispatching Events from your Extension

Events can be used by extensions in the following scenarios:

* Triggering actions in the Adobe Cloud Platform SDKs.   Events are used by the extensions to signal when certain actions should take place, for example to send an Analytics ping. Extensions can send the same types of events that the Adobe Cloud Platform SDKs would send internally to trigger these actions.
* Triggering actions in another extension.     You might have multiple extensions in your application, and some may have their own events defined which will trigger actions.

## Create an Event for Dispatching

The `ACPExtensionEvent` \(iOS\) / `Event` \(Android\) class contains the event that is used by the internal event hub. You can construct an event at any time after the Adobe Cloud Platform SDKs has been initialized.

**Tip**: This event construction is usually completed in an event listener.

When constructing an event, errors might be returned for the following reasons:

* The data that was passed cannot be converted to a JSON representation.
* The type or source has been deprecated by Adobe.
* The type or source is not known \(for example, _com.adobe.eventType_ is used, but the prefix but is not known\).

In the example below, a custom event called `MyCustomEvent` is created with custom types and sources. The internal modules will not respond to an event like this because they will not be listening for it. You can add an event listener for this type and source to verify that it is working.

**iOS**

To create events in iOS, you must first import `ACPExtensionEvent.h`:

```text
import "ACPExtensionEvent.h"
NSError error = nil; 
NSDictionary eventData = @{
       @"id" : @"humblebumble",
    @"localTemp: @72.6F,
    @"pageClicks" : @237, 
    @"pageOrder" : @[@1,@2,@3,@4]
 };
 ACPExtensionEvent* newEvent = [ACPExtensionEvent extensionEventWithName:@"MyCustomEvent"
 type:@"com.myCompany.eventType.custom"
 source:@"com.myCompany.eventSource.custom" data:eventData
 error:&error];
 if (error) {
     NSLog(@"Error constructing new event %@:%ld", [error domain], [error code]);
}
```

#### Android

To create events in Android, you must first import `com.adobe.marketing.mobile.Event`:

```java
import com.adobe.marketing.mobile.Event;

...
List<Integer> pageOrder = new ArrayList<Integer>();
pageOrder.add(1);
pageOrder.add(2);
pageOrder.add(3);
Map<String, Object> eventData = new HashMap<String, Object>();
eventData.put("id", "clickid53");
eventData.put("localTemp", 72.6);
eventData.put("pageClicks", 23);
eventData.put("pageOrder", pageOrder);
Event newEvent = new Event.Builder("MyCustomEvent",             
                                   "com.myCompany.eventType.custom",
                                   "com.myCompany.eventSource.custom")
                                   .setEventData(eventData).build();
```

### Dispatch your Event

After creating your event, dispatch it by using the `ACPCore` \(iOS\) / `MobileCore` \(Android\) method `dispatchEvent`. A typical place to dispatch an event is in an event listener.

In some cases, you may need to dispatch an event from one of your public APIs or application methods in order to trigger an internal flow in your own extension or in other Adobe extension. In this case you can call `ACPCore` \(iOS\) / `MobileCore` \(Android\) method `dispatchEvent`.

#### iOS

```text
+ (void) loginButtonClicked: {

    // construct the event to dispatch (see above)
    Event newEvent = ...;

    // dispatch the event
    NSError* error = nil;
    if (![ACPCore dispatchEvent:newEvent error:&error]) {
        NSLog(@"Error dispatching event %@:%ld", [error domain], [error code]);
    }];

    // OR alternatively dispatch the event and get a response callback
    if (![ACPCore dispatchEventWithResponseCallback:newEvent responseCallback:^(ACPExtensionEvent* event _Nonnull){
        NSLog(@"I got a response to my event! %@", event.eventName);

    } error:&error]) {
        NSLog(@"Error dispatching event %@:%ld", [error domain], [error code]);
    }];

}
```

#### Android

```java
public void loginButtonClicked() {
    // construct the event to dispatch 
    Map<String, String> contextData = new HashMap<String, String>();
    contextData.put("username", "example@mail.com");
    contextData.put("dayofweek", "Monday");
    Map<String, Object> analyticsAction = new HashMap<String, Object>();
    analyticsAction.put("action", "clickLogin");
    analyticsAction.put("contextdata", contextData);
    Event analyticsEvent = new Event.Builder("Login click event",
                "com.adobe.eventType.generic.track",
                "com.adobe.eventSource.requestContent")
                .setEventData(analyticsAction).build();

    // dispatch the analytics event
    ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
        @Override
        public void error(final ExtensionError extensionError) {
            Log.e("loginButtonClicked", String.format("An error occurred while dispatching                 event %d %s", extensionError.getErrorCode(), extensionError.getErrorName()));
        }
    };
    MobileCore.dispatchEvent(analyticsEvent, errorCallback);
}
```

### Dispatch Paired Events

If you need to use a request `ACPExtensionEvent` \(iOS\) / `Event` \(Android\) as a trigger, and you have a callback to be called when the response paired event is sent, you can use the `dispatchEventWithResponseCallback` API from `ACPCore` \(iOS\) / `MobileCore` \(Android\). Then, the paired response event should be sent using the `dispatchResponseEvent` API.

**Tip:** Paired events are usually used for set/get operations where you need to be notified about a response event outside of your extension code.

Here is an example of how to implement this:

#### IOS

The iOS content is currently in progress.

#### Android

You can have this code in an application Activity or in one of your extensions public API classes:

```java
// how to dispatch a paired event with an associated response callback
ExtensionErrorCallback<ExtensionError> errorCallback = new         ExtensionErrorCallback<ExtensionError>() {
    @Override
    public void error(final ExtensionError errorCode) {
        Log.w("dispatchEventCallback", String.format("An error occurred when dispatching event, %s", errorCode.getErrorName()));
    }
};

AdobeCallback<Event> responseEventCallback = new AdobeCallback<Event>() {
    @Override
    public void call(final Event value) {
        Log.d("dispatchEventCallback", String.format("Response event received, type %s and source %s",
                                                     value.getType(), value.getSource()));
    }
};
Event event = new Event.Builder("dispatchEventWithResponseCallback", "com.myCompany.eventType.custom", "com.myCompany.eventSource.request").build();
MobileCore.dispatchEventWithResponseCallback(event, responseEventCallback, errorCallback);
...
```

Register a listener for this event type and source in MyExtension.java:

```java
// register a listener for a the request event type and source
protected MyExtension(ExtensionApi extensionApi) {
        super(extensionApi);

        getApi().registerEventListener("com.myCompany.eventType.custom", "com.myCompany.eventSource.request", MyListener.class, null);
}
...
```

Dispatch a response event when the request is received in the `hear` method of your Listener in MyListener.java:

```java
public class MyListener extends ExtensionListener {

    protected MyListener(final ExtensionApi extension, final String type, final String source) {
        super(extension, type, source);
    }

    @Override
    public void hear(Event event) {
        ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
            @Override
            public void error(final ExtensionError errorCode) {
                Log.w(getParentExtension().getName(), String.format("An error occurred when dispatching event, %s",
                        errorCode.getErrorName()));
            }
        };
        Event responseEvent = new Event.Builder("response event", "com.myCompany.eventType.custom", "com.myCompany.eventSource.response").build();

        // sending a paired response event for the request event
        MobileCore.dispatchResponseEvent(responseEvent, event, errorCallback);
    }

    @Override
    protected MyExtension getParentExtension() {
        return (MyExtension)super.getParentExtension();
    }

    ...
}
```

