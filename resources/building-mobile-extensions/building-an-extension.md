# Building an extension

## Prerequisites to building an extension

Before you build an extension, complete the following tasks:

* Ensure that you are using the Adobe Experience Platform SDKs.

  Extensions extend the behavior of these SDKs.

* Ensure that you can accomplish your goals only by using an extension.

  To determine your goals, think about the following questions:

  * Do you need access to data that is not already exposed via the Adobe Experience Platform SDKs?    
  * Do you need to be notified when messages will be sent, or data is being collected by the Adobe Experience Platform SDKs?   
  * Do you need to add data to or modify data for outgoing messages?    
  * Do you need to expose data to other extensions or to rules processing?

  If your answer to any of these questions is **yes**, build the extension.

* Ensure that you are using Objective-C on iOS or Java on Android.

  Extensions for iOS can currently only be built using Objective-C, and extensions on Android can currently only be built using Java.

* Ensure that you have already included the Adobe Experience Platform SDKs in your project.

## Implementing an Adobe Experience Platform SDK extension

To create a simple extension, complete the following procedures in the order in which they are listed:

### Create an extension class

The `ACPExtension`(iOS) or `Extension` (Android) class is the base class from which extensions must be derived. The `init` method (iOS) or the base `constructor` \(Android\) of your extension class is where you can extend the Adobe Experience Platform SDKs functionality by registering event listeners or by setting a default shared state that other modules can access.

#### Android

The `Extension` class has the following method that you must override:

* `getName`, which returns the name of the extension.

  Extension developers must prefix their extension names with the company name (for example, `com.myCompany.myExtension`). For more information about the naming constraints, see the [namespace conventions section](./#namespace-conventions). The name that you use to register **cannot** conflict with other registered extensions or Adobe internal modules.

The name that you use to register cannot conflict with other registered extensions or Adobe internal modules. The extension name is considered case insensitive by the Mobile SDK.

{% hint style="info" %}
All Adobe module names are prefixed with `com.adobe.module` and are considered reserved.
{% endhint %}

The `Extension` class has the following methods that you can optionally override and a member that provides access to the Event Hub:

* `getVersion`: Returns a version string for your extension.  The version string is only used for logging and is currently not validated for formatting.
* `onUnregistered`: Allows your extension to complete the cleanup that is required when the Adobe Experience Platform SDK unregisters your extension. Unregistration typically happens when you shutdown the app, but it can also occur when an extension is behaving badly. Examples of the extension behaving badly include taking too long to handle a callback or throwing an exception.
* `onUnexpectedError`: Allows you log additional information when the Adobe Experience  Platform SDK encounters an error that could not be returned immediately from a call into the Adobe Experience Platform SDK.   An example is an exception that is thrown on a worker thread. The exceptions are rare after your extension has been correctly implemented, but the exceptions might occur during development.
* `getApi`: Allows the extension developer to interact with the Event Hub to do various tasks including registering event listeners and managing the shared state. This method can be used at any time after the extension registration is complete. It may also be used by your listeners by calling  `super.getParentExtension().getApi()`.

{% hint style="info" %}
The `Extension` class provides access to the `ExtensionApi` interface through the `getApi` member.
{% endhint %}

#### Android code example

```java
import com.adobe.marketing.mobile.*;
class MyExtension extends Extension {

    public MyExtension(final ExtensionApi extensionApi) {
        super(extensionApi);
    }

    @Override
    public String getName() {
        return "my.company.com";
    }

    @Override
    public void onUnregistered() {
        // this method will be called when the extension is unregistered from the 
        // Event Hub in order for you to perform the necessary cleanup
    }
}
```

#### iOS

The `ACPExtension` class has the following method that you must override:

* `name`: Returns the name of the extension.  
  Extension developers must prefix their extension names with the company name (for example, `com.myCompany.myExtension`). For more information about the naming constraints, please read the [namespace conventions section](./#namespace-conventions). The name that you use to register **cannot** conflict with other registered extensions or Adobe internal modules.
  
  {% hint style="info" %}
  All Adobe module names are prefixed with `com.adobe.module` and are considered reserved.
  {% endhint %}

The `ACPExtension` class has the following methods that you can optionally override and a member that provides access to the Event Hub:

* `version`: Returns a version string for your extension. The version string is only used for logging and is currently not validated for formatting.
* `onUnregister`: Allows your extension to complete the cleanup that is required when the Adobe Experience Platform SDK unregisters your extension. Unregistration typically happens at app shutdown but can also occur when an extension is behaving badly. Examples of the extension behaving badly include taking too long to handle a callback or throwing an exception.
* `unexpectedError`: Allows you log additional information when the Adobe Experience Platform SDKs encounter an error that could not be returned immediately from a call into the SDK. An example is an exception that is thrown on a worker thread. The exceptions are rare after your extension has been correctly implemented, but the exceptions may occur during development.
* `api`: Allows the extension developer to interact with the Event Hub to do tasks such as registering event listeners and managing shared state.

  This method can be used at any time during or after init has been called on your extension. It may also be used by your listeners by using the extension member.

{% hint style="info" %}
The `ACPExtension` class provides access to the `ACPExtensionApi` interface through the API member.
{% endhint %}

#### iOS code example

1. In Xcode, create a new file from the `Cocoa Touch Class` template and save it in your project.
2. Name this class `MyExtension` and ensure that this class is a member of `ACPExtension`.

The methods that are available for overriding are displayed in the following example:

**MyExtension.h**

```objectivec
#import "ACPExtension.h"

@interface MyExtension : ACPExtension
- (nullable NSString*) name;
- (nullable NSString*) version;
- (void) unexpectedError: (nonnull NSError*) error;
- (void) onUnregister;
@end
```

1. Provide an implementation for the `init` and `name` methods.

**MyExtension.m**

```text
#import "MyExtension.h"

@implementation MyExtension
- (nullable NSString*) name {
    return @"com.myCompany.myExtension";
}

- (instancetype) init {
    if (self = [super init]) {
        // register your listeners here
    }

    return self;
}
@end
```

1. If you override the `init` method, call the default implementation of `onUnregister`.

```text
- (void) onUnregister {
    [super onUnregister];
    // your cleanup code goes here
}
```

1. Review the error message that was logged by the default implementation of `unexpectedError`.

```text
- (void) unexpectedError:(NSError *)error {
    [super unexpectedError];
     // your error handling code goes here
}
```

### Registering your extension

After creating your extension class, you can register it by using the `ACPCore` (iOS) or `MobileCore` (Android) method `registerExtension`. During registration, the extension class that you passed will be used by the Adobe Experience Platform SDKs to create an instance of your extension that will be retained until your extension is unregistered.

{% hint style="info" %}
Registration can be completed any time after the app is launched.
{% endhint %}

{% tabs %}
{% tab title="Android" %}
#### Android

The best place to register your extension on Android is in the `onCreate` method of your activity.

{% hint style="info" %}
Some registration errors, such as sending a null extension class as parameter, are synchronous and occur immediately. Other errors, like undefined names, name conflicts, or type checking issues, might occur asynchronously and are reported through the `onUnexpectedError` callback before the extension is unregistered.
{% endhint %}

```java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.ExtensionError;
import com.adobe.marketing.mobile.ExtensionErrorCallback;
...
@Override
public void onCreate() {
    super.onCreate();
    MobileCore.setApplication(this);

    ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
        @Override
        public void error(final ExtensionError extensionError) {
            Log.e("Extensions", String.format("An error occurred while registering the MyCustomExtension %d %s", extensionError.getErrorCode(), extensionError.getErrorName()));
            }
        };
    if (!MobileCore.registerExtension(MyCustomExtension.class, errorCallback)) {
        Log.e("Extensions", "Failed to register the MyCustomExtension extension");
    }

    ...
    MobileCore.start(null);
}
```
{% endtab %}

{% tab title="Objective-C" %}
#### iOS

The best place to register your extension on iOS is in your AppDelegate's `application:didFinishLaunchingWithOptions:` method.

{% hint style="info" %}
Some registration errors, such as undefined names, name conflicts, or type checking issues, occur immediately. Other errors might occur asynchronously and are reported through the `unexpectedError` callback before the extension is unregistered.
{% endhint %}

```objectivec
#import "ACPCore.h"
#import "MyExtension.h"

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSError *error = nil;
    if ([ACPCore registerExtension:[MyExtension class] error:&error]) {
        NSLog(@"MyExtension was registered");
    } else {
        NSLog(@"Error registering MyExtension: %@ %d", [error domain], (int)[error code]);
    }

    ... // register other extensions
    [ACPCore start:^{
        dispatch_async(dispatch_get_main_queue(), ^{
            // SDK was initialized
         });
    }];
    return YES;
}

@end
```
{% endtab %}
{% endtabs %}

#### Unregistering your extension

If your extension does not need to be active at all times, you can unregister your extension by using `unregisterExtension` from the `ACPExtensionApi` (iOS\ / `ExtensionApi` (Android). This process allows you to have more granular resource control, but the listeners that you registered will be unregistered. If you overrode `onUnregister`, you should see a call into your implementation that allows you to clean up resources before the instance is released.

{% hint style="info" %}
If you retained a reference to the extension instance (for example by storing `self` or `this` in a static variable), this is where you should clean it up.
{% hint style="info" %}

{% tabs %}
{% tab title="Android" %}
#### Example

```java
getApi().unregisterExtension();
```
{% endtab %}

{% tab title="Objective-C" %}
#### Example

```text
[self.api unregisterExtension];
```
{% endtab %}
{% endtabs %}

