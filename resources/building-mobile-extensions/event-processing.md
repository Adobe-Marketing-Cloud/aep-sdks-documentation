# Event processing

An event is composed of the following components:

* A name, which is used for debugging
* An event type, which defines what kind of event this is and determines who is notified when this event occurs
* An event source, which is where the event originated and is used to determine who is notified when this event occurs
* Event data, which is the structured data that is associated with this particular event. This data is retrievable as a JSON blob
* Versioning information, which is used to synchronize a group of events with the associated shared data, is not directly exposed to extensions. This information is implicitly used when getting shared states

{% hint style="info" %}
Extensions use the `ACPExtensionEvent` (iOS) / `Event` (Android) class to create events and dispatch them to the Mobile SDK event hub to trigger the extension business logic or to retrieve data.
{% endhint %}

The event type and event source that are associated with the received event can be in lower case because the Mobile SDK compares the type and the source as case insensitive values. When you check the event type and event source of the event, you should use the ignore case string comparison.

The following list shows some examples of potential events:

* The Experience Platform SDK configuration changed
* Data was requested by the application
* Data was collected by the application
* An action was requested by the application
* Data was requested by an extension or internal module in response to another event

Events are closely tied to shared states, which also have versions. This is why events can be passed when requesting a shared state. This process ensures that the state that is retrieved matches the event that is associated with this state. This also means that events can be associated with each other, and as a result, these events share the same versioning information.

## Event hub

The event hub is the core data structure to which the SDK extensions and other components are tied, and it maintains the following data:

* A list of registered extensions and internal modules
* A list of registered event listeners
* A shared state database

The event hub is responsible for receiving events that are dispatched by the application, by the extensions, and processing events and dispatching these events to registered listeners. The event hub is accessed from the application and from the extensions by using the `MobileCore` API that is exposed in the SDK. The application dispatches events indirectly, by calling API methods that cause events to be dispatched in the Experience Platform SDKs. The extensions and internal modules dispatch events directly by calling into the event hub.

![](../../.gitbook/assets/event-dispatch-flow-1280-6560ee4b-0.png)

## Order of event processing

The lifecycle of an event is as follows:

1. The event is created and dispatched by the extension or application.
2. The event is received by the event hub.
3. The event is compared against the registered event listeners.  
4. In parallel, the event is passed to every listener that matches.

