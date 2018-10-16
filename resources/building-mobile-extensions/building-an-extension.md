# Building an Extension

## Prerequisites to Building an Extension

Before you build an extension, complete the following tasks:

* Ensure that you are using the Adobe Cloud Platform SDKs.

  Extensions extend the behavior of these SDKs.

* Ensure that you can accomplish your goals only by using an extension.

  To determine your goals, think about the following questions:

  * Do you need access to data that is not already exposed via the Adobe Experience Cloud Platform SDKs?    
  * Do you need to be notified when messages will be sent, or data is being collected by the Adobe  Cloud Platform SDKs?   
  * Do you need to add data to or modify data for outgoing messages?    
  * Do you need to expose data to other extensions or to rules processing?

  If your answers to any of these questions is yes, build the extension.

* Ensure that you are using Objective-C on iOS or Java on Android.

  Extensions for iOS can currently only be built using Objective-C, and extensions on Android can currently only be built using Java.

* Ensure that you have already included the Adobe Cloud Platform SDKs in your project.

## Implementing an Adobe Cloud Platform SDK Extension

To create a simple extension, complete the following procedures in the order in which they are listed:

### A. **Create an Extension Class**

The `ACPExtension`\(iOS\) or `Extension` \(Android\) class is the base class that any extensions must derive from. The `init` method \(iOS\) or the base `constructor` \(Android\) of your extension class is where you will have the opportunity to extend the Adobe Cloud Platform SDKs functionality by registering event listeners, or by setting a default shared state that other modules can access.

#### **iOS**

The `ACPExtension` class has the following method that you must override:

* `name`, which returns the name of the extension.  
  Extension developers must prefix their extension names with the company name \(for example, _com.myCompany.myExtension_\). For more information about the naming constraints, see [Namespace Conventions](./#namespace-conventions). The name that you use to register cannot conflict with other registered extensions or Adobe internal modules.

  **Tip**: All Adobe module names are prefixed with com.adobe.module and are considered reserved.

The `ACPExtension` class has the following methods that you can optionally override and a member that provides access to the Event Hub:

* `version`, which returns a version string for your extension.    The version string is only used for logging and is currently not validated for formatting. 
* `onUnregister`, which allows your extension to complete the cleanup that is required when the Adobe Cloud Platform SDK unregisters your extension.    Unregistration typically happens at app shutdown but can also occur when an extension is behaving badly. Examples of the extension behaving badly include taking too long to handle a callback or by throwing an exception.
* `unexpectedError`, which allows you log additional information when the Adobe Cloud Platform SDKs encounter an error that could not be returned immediately from a call into the SDK.    An example is an exception that is thrown on a worker thread. The exceptions are rare after your extension has been correctly implemented, but the exceptions might occur during development.
* `api` , allows the extension developer to interact with the Event Hub to register event listeners, manage shared state, and so on.  This method can be used at any time during or after init has been called on your extension. It may also be used by your listeners by using the extension member.        **Tip**: The ACPExtension class provides access to the `ACPExtensionApi` interface through the API member.  

#### **iOS code example**

1. In Xcode, create a new file from the `Cocoa Touch Class` template and save it in your project.
2. Name this class `MyExtension` and ensure that this class is a member of `ACPExtension`.

**Tip**: In the example below, the methods that are available for overriding are displayed.

**MyExtension.h**

```objectivec
import "ACPExtension.h"
@interface MyExtension: ACPExtension {}
   (void) unexpectedError: (nonnull NSError*) error;
   (void) onUnregister;
@end
```

1. At a minimum, you must provide an implementation for the `init` and `name` methods.

   **MyExtension.m**

   ```text
    #import "MyExtension.h"
    @implementation MyExtension
     - (nullable NSString*) name {
        return @"com.myCompany.myExtension";
      }
     - (instancetype) init {
       if (self= [super init]) {
       // your extension code goes here
       }
        return self;
      }
    @end
   ```

2. The default implementation of onUnregister must be called if you decide to override the `init` method.

   ```objectivec
       - (void) onUnregister
        [super onUnregister];
        // your extension code goes here
        }
   ```

3. The default implementation of `unexpectedError` will log an error message using `NSLog`.

   ```objectivec
    - (void) unexpectedError {
    [super unexpectedError];
    //your detailed logging code goes here
    }
   ```

#### **Android**

The `Extension` class has the following method that you must override:

* `getName`, which returns the name of the extension.

  Extension developers must prefix their extension names with the company name \(for example, _com.myCompany.myExtension_\). For more information about the naming constraints, see Namespace Conventions. The name that you use to register cannot conflict with other registered extensions or Adobe internal modules.

**Tip**: All Adobe module names are prefixed with _com.adobe.module_ and are considered reserved.

* `onUnregistered`, which allows your extension to complete the cleanup that is required when the Adobe Cloud Platform SDK unregisters your extension.  Unregistration typically happens at app shutdown but can also occur when an extension is behaving badly. Examples of the extension behaving badly include taking too long to handle a callback or by throwing an exception.

The `Extension` class has the following methods that you can optionally override and a member that provides access to the Event Hub:

* `getVersion`, which returns a version string for your extension. The version string is only used for logging and is currently not validated for formatting.
* `onUnexpectedError`, which allows you log additional information when the Adobe Experience Cloud Platform SDK encounters an error that could not be returned immediately from a call into the Adobe Cloud Platform SDK.  An example is an exception that is thrown on a worker thread. The exceptions are rare after your extension has been correctly implemented, but the exceptions might occur during development.
* `getApi` , allows the extension developer to interact with the Event Hub to register event listeners, manage shared state, and so on.

  This method can be used at any after the extension registration is complete. It may also be used by your listeners by using the extension member.

**Tip**: The `Extension` class provides access to the `ExtensionApi` interface through the `getApi` member.

#### **Android code example**

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

### B. **Registering your Extension**

After creating your extension class, you can register it by using the `ACPCore` method `registerExtension`. Some registration errors, such as undefined names, name conflicts, or type checking issues, occur immediately. Other errors might occur asynchronously and are reported through the `unexpectedError` callback before the extension is unregistered.

**Tip**: Registration can be completed any time after the app is launched.

During registration, the extension class that you passed will be used by the Adobe Cloud Platform SDKs to create an instance of your extension that will be retained until your extension is unregistered.

#### iOS

A convenient place to register your extension on iOS is in your AppDelegate's `application:didFinishLaunchingWithOptions:` method.

```objectivec
#import <ACPCore_iOS/ACPCore_iOS.h>
#import "MyExtension.h"

@implementation AppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSError *error = nil;
    if ([ACPCore registerExtension:[MyExtension class] error:&error]) {
        NSLog(@"MyExtension was registered");
    } else {
        NSLog(@"Error registering MyExtension: %@ %d", [error domain], (int)[error code]);
    }
}

@end
```

#### **Android**

A convenient place to register your extension on Android is in the `onCreate` method of your activity.

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
}
```

### C. **Unregistering your Extension**

If your extension does not need to be active at all times, you can unregister your extension by using `unregisterExtension` in the `ACPExtensionApi`. This process allows you to have more granular resource control, but the listeners that you registered will be unregistered. If you overrode `onUnregister`, you should see a call into your implementation that allows you to clean up resources before the instance is released.

**Tip**: If you retained a reference to the extension instance \(for example by storing `self` or `this` in a static variable\), this is where you should clean it up.

