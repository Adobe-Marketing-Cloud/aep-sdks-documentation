# Listening for Events

A common use case is to add an event listener to get notifications for events that occur in the Adobe Experience Platform SDK. The main location to add an event listener is in the `init` method, although you can add listeners by using other callbacks later. You can add the logic that you want executed when an event occurs, and for which you have a listener, in the `hear` method of your listener class.

When handling an event in the event listener, take into consideration that the `hear` method should take a maximum of 100ms to execute. This means that potentially long-running operations should be pushed to another thread (for example, network or file operations), as in the following examples.

Here are some additional rules to remember for event listeners:

* You can listen to an event by registering your listener class with an event source and an event type.  The Adobe Experience Platform SDKs will create an instance of your listener class and retain it as long as your extension is registered.
* When an event that you are listening for occurs, the `hear` method on the appropriate instance of your listener class will be called.
* You can register multiple listeners, but each listener instance only listens for one source/type pair.
* One listener class might be used to listen for multiple events, but you will need to check the details of the event you are passed on each call to the `hear` method.
* All registered listeners are released when the extension is unregistered.

## Creating your event listener

### **iOS**

1. In Xcode create a new file from the `Cocoa Touch Class` template and save it in your project. 
2. Name your class `MyExtensionListener`, and it should be a subclass to the `ACPExtensionListener` class.

   The `MyExtensionListener.m` file will contain your extension interface declaration and will import `ACPExtensionListener.h`. In the example below, the methods that are available for overriding are also displayed:

**MyExtensionListener.h**

```objective-c
#import "ACPExtensionListener.h"
#import "ACPExtensionEvent.h"

@interface MyExtensionListener : ACPExtensionListener
    - (void) hear:(ACPExtensionEvent *)event;
@end
```

3. At a minimum, you must provide an implementation for the hear method.  

**MyExtensionListener.m**

```objective-c
#import "MyExtensionListener.h"
#import "MyExtension.h"

@implementation MyExtensionListener 
    - (void) hear:(ACPExtensionEvent *)event {
		MyExtension* parentExtension = [self getParentExtension];
    	if (parentExtension == nil) {
        	NSLog(@"The parent extension was nil, skipping event");
        	return;
    	}

        [parentExtension handleEvent:event];
}

/**
 * Returns the parent extension that owns this listener
 */
- (MyExtension*) getParentExtension {
    MyExtension* parentExtension = nil;
    if ([[self extension] isKindOfClass:MyExtension.class]) {
        parentExtension = (MyExtension*) [self extension];
    }

    return parentExtension;
}

@end
```

### **Android**

Create a new Java class for your listener, extend the base class `ExtensionListener` and implement the required constructor and hear method. You can also override the `getParentExtension` method in order to retrieve your custom extension class instead of the base `Extension` class.

```java
package com.test.company;

import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.ExtensionListener;
import com.adobe.marketing.mobile.ExtensionApi;
import com.adobe.marketing.mobile.Event;

class MyListener extends ExtensionListener {
    protected MyListener(final ExtensionApi extension, final String type, final String source) {
        super(extension, type, source);
    }

    @Override
    public void hear(final Event event) {
        // run the event processing on its own executor in the parent extension class
        getParentExtension().handleConfigurationEvent(event);
    }

    @Override
    protected MyExtension getParentExtension() {
        return (MyExtension)super.getParentExtension();
    }
}
```

**Tip:** Create an executor in your `Extension` class for event processing and use it when one of your listeners is called. This way you do not have to worry about how long your event handler is taking.

```java
package com.test.company;

import android.util.Log;

import com.adobe.marketing.mobile.Event;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.ExtensionApi;
import com.adobe.marketing.mobile.ExtensionError;
import com.adobe.marketing.mobile.ExtensionErrorCallback;

import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class MyExtension extends Extension {
    private final Object executorMutex = new Object();
    private ExecutorService executor;

    public MyExtension(final ExtensionApi moduleApi) {
        super(moduleApi);

        ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
            @Override
            public void error(final ExtensionError extensionError) {
                // something went wrong, the listener couldn't be registered
            }
        };
        getApi().registerEventListener("com.adobe.eventType.configuration",
            "com.adobe.eventSource.requestContent", MyListener.class, errorCallback);
    }

    @Override
    public final String getName() {
        return "my.test.company";
    }

    @Override
    public final String getVersion() {
        return "1.0.0";
    }

    @Override
    public final void onUnregistered() {
        // extension unregistered successfully - perform cleanup
    }

    void handleConfigurationEvent(final Event event) {
        getExecutor().execute(new Runnable() {
            @Override
            public void run() {
                Log.d(getName(), String.format("Started processing new event of type %s and source %s", event.getType(), event.getSource()));
                // do your processing here
            }
        });
    }

    private ExecutorService getExecutor() {
        synchronized (executorMutex) {
            if (executor == null) {
                executor = Executors.newSingleThreadExecutor();
            }

            return executor;
        }
    }
}
```

## What can you do in your event handler?

Your listener has a reference to the parent extension that registered it. You can use this to centralize logic into your extension class and call into it from your listener. This also means you have access to the extension services API (`ACPExtensionApi` on iOS and `ExtensionApi` on Android) provided to the extension. This will allow you to manage your shared states or register additional listeners. You also have access to the core SDK (`ACPCore`(iOS) or `MobileCore` (Android). This will allow you to dispatch events and receive responses.

## Registering your event listener

You can register your listener class by using the init method as in the example below. In the `hear` method, you can access the registered extensions instance by using the extension property. This step can be useful to maintain state in your extension or when you need to access to the `ACPExtensionApi` interface that the extension can also access.

The following example calls the listeners hear method when a change to the Adobe Experience Platform SDKs configuration occurs.

### **iOS**

In iOS the event listeners are registered using the `registerListener` method of the `ACPExtensionApi` interface. You can access this interface by using the `api` property in `ACPExtension`.

**MyExtension.h**

```objective-c
#import "ACPExtension.h"
#import "ACPExtensionEvent.h"

@interface MyExtension : ACPExtension

- (void) handleEvent: (ACPExtensionEvent*) event;

@end
```
**MyExtension.m**

```objective-c
#import "MyExtension.h"
#import "MyExtensionListener.h"

@implementation MyExtension 

- (instancetype) init {
    if (self = [super init]) {
        NSError *error = nil;
        
        // register a listener for configuration events
        if ([self.api registerListener:[MyExtensionListener class]
                             eventType:@"com.adobe.eventType.hub"
                           eventSource:@"com.adobe.eventSource.sharedState"
                                 error:&error]) {
            NSLog(@"MyExtensionListener successfully registered for Event Hub Shared State events");
        } else if (error) {
            NSLog(@"An error occured while registering MyExtensionListener, error code: %ld", [error code]);
        }
    }
    
    return self;
}

- (nullable NSString *) name {
    return @"my.company";
}

- (NSString *) version {
    return @"1.0.0";
}

- (void) onUnregister {
    [super onUnregister];
    // extension unregistered successfully - perform cleanup
}

- (void) handleEvent: (ACPExtensionEvent*) event {
    // process event
}
@end
```

### **Android**

Event listeners in Android are registered using the `registerEventListener` method of the `ExtensionApi` interface. You can access this interface by using the `getApi` method in `Extension`. This example show registering the listener from your extension contructor.

```java
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.ExtensionApi;

public class MyExtension extends Extension {

    public MyExtension(final ExtensionApi moduleApi) {
        super(moduleApi);

        ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
            @Override
            public void error(final ExtensionError extensionError) {
                // something went wrong, the listener couldn't be registered
            }
        };
        getApi().registerEventListener("com.adobe.eventType.hub",
                "com.adobe.eventSource.sharedState", MyListener.class, errorCallback);
    }

    @Override
    public final String getName() {
        return "my.company";
    }

    @Override
    public final String getVersion() {
        return "1.0.0";
    }

    @Override
    public final void onUnregistered() {
        // extension unregistered successfully - perform cleanup
    }
}
```

## Registering a Wildcard Listener

If you need to listen for all the events received and broadcasted by the Event Hub, you can register a wildcard listener by using the `registerWildcardListener` API.

**Important**: The `hear` method of this listener can be called often, and you should not do intensive processing on the same thread. We strongly recommended that you use your own thread executor for any processing that you do in this listener. This way, the Event Hub is not blocked, and the listener is not unregistered if it takes too long.

### **iOS**

```objective-c
#import "MyExtension.h"
#import "MyExtensionWildcardListener.h"

@implementation MyExtension

-(instancetype) init {
    if (self = [super init]) {        
        NSError* error = nil;
        if ([[self api] registerWildcardListener:[MyExtensionWildcardListener class] 
                                             error:&error]) {
            NSLog(@"MyExtensionWildcardListener successfully registered");
        } else if (error) {
            NSLog(@"An error occurred while registering MyExtensionWildcardListener, error code: %ld", [error code]);
        }
    }

    return self;
}
```

### **Android**

```java
import com.adobe.marketing.mobile.*;

public class MyExtension extends Extension {

    public MyExtension(final ExtensionApi moduleApi) {
        super(moduleApi);

        ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
            @Override
            public void error(final ExtensionError extensionError) {
                // something went wrong, the listener couldn't be registered
            }
        };
        getApi().registerWildcardListener(MyListener.class, errorCallback);
    }

    ...
}
```

