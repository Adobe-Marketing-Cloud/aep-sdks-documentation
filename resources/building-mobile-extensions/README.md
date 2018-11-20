---
description: This information can help you understand how to build your own extension.
---

# Building mobile extensions

To support customer-specific features, and allow for the greatest flexibility, the goal is to provide an interface for customers to integrate with the Adobe Cloud Platform SDKs at a much lower level. This interface allows customers to define extensions, which are similar in capabilities to the extensions that Adobe Launch has written for our internal services. We are going to follow an open model, so that these extensions will have access to all of the events and data to which the Adobe Cloud Platform SDK code also has access.

Extensions allow customers to extend the Adobe Cloud Platform SDKs with their own code. This includes listening for and dispatching any event, reading the shared state of any registered extension, and sharing the state of the current extension. The application can use the extension to monitor for information that Adobe does not expose by default. It can also use the extension to modify Adobe Cloud Platform SDK internal operations, for example by adding additional data to messages that are sent or by sending data to other systems.

## Namespace Conventions

Components or data that are provided by Adobe must be clearly distinguished from the components or data that are provided by external parties. Inconsistent naming conventions impact module naming, event type, source names, and event data keys.

Here are the naming rules for extensions:

* The ADOBE\_PREFIX is com.adobe.
* The THIRDPARTY\_PREFIX is com. and com.adobe.\* is reserved for Adobe.
* Third parties must prefix their extension name and any custom event types or sources they create with the THIRDPARTY\_PREFIX followed by their company name.
* By convention, Adobe will not prefix shared state keys or eventdata keys. These names will be in the global namespace. example: “mid”.
* Adobe internal module names will follow the pattern ADOBE\_PREFIX.module.{moduleName}. 
* Adobe event types will follow the pattern .eventType.{eventType}. 
* Adobe event source will follow the pattern ADOBE\_PREFIX.eventSource.{eventSource}. 
* Shared state names \(not keys\) must equal the module name. 
* All constants will be named using lowerCamelCase, and cases will be normalized internally to make comparisons case-insensitive. For example, if you use **Com.Adobe.moDule.AnAlytiCS** it will be internally converted to **com.adobe.module.analytics.** An exception to this rule is that shared state names that are used in rules are compared in a **case-sensitive** manner. This means that when registering an extension, the actual case is retained internally, so that rule comparison can succeed.

**Important**: We strongly recommend that you use ASCII characters even if your company name contains non-ASCII characters.

## Extension Architecture

![](../../.gitbook/assets/external-module-layer-cake.png)

### Error Handling

When using an extension, you might get asynchronous or synchronous errors.

#### Synchronous Errors

Synchronous errors are caught outside the Adobe Cloud Platform SDK and might occur for the following reasons:

* When registering a class with the incorrect parent class.
* When passing empty strings to certain parameters.  Examples include an extension name, an event type, a shared state name, and so on.
* When passing malformed JSON data.Synchronous errors will be returned immediately on the same thread.   **Important**: In iOS, a `@false` value is returned to indicate an error and filling in an optional `NSError` out parameter.

#### Asynchronous Errors

Asynchronous errors are caught in the Adobe Cloud Platform SDKs but are rare. When they occur, the error is handled with a callback function, which might be called back on a different thread.

Asynchronous errors might occur for the following reasons:

* When registering an extension with a name that duplicates an internal module or a previously registered extension.
* When using a deprecated shared state name.
* When registration is attempted during extension shutdown.
* When an event is being dispatched while the extension is being shut down.
* When a callback from the Adobe Cloud Platform SDKs to the external code throws an exception.
* When an internal error occurs, or an unexpected exception is thrown.
* \(TBD\) When a timeout has been exceeded.

**Important**: In iOS, asynchronous errors are handled by using the `unexpectedError` method that is defined in the `ADBExtension` class.

