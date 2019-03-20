# Logging from an extension

We recommend using the Mobile SDK logging API in order to print any message from the Extension code. The Mobile SDK provides to the application developers the `setLogLevel`  API which is used for setting the Mobile SDK logging mode: VERBOSE, DEBUG, WARNING and ERROR. If current logging mode is less verbose, then the message will not be printed out by the Mobile SDK. When debugging and testing your extension, you or the application developer can make the logging more verbose in order to see all the messages flowing through the Mobile SDK.

Mobile SDK uses the extension name as log tag for the Adobe extensions in order to be easier for the application developer to filter the logging for a particular mobile extension. A similar approach can be implemented by any partner extension as in the examples below:

{% tabs %}
{% tab title="Android" %}
#### Example

```java
final String extensionName = "com.example.MyExtension";
...
ExtensionErrorCallback<ExtensionError> errorCallback = new ExtensionErrorCallback<ExtensionError>() {
    @Override
    public void error(final ExtensionError errorCode) {
        MobileCore.log(LoggingMode.WARNING, extensionName, String.format("An error occurred while registering extension, %s",
                                                                                     errorCode.getErrorName()));
    }
};
MobileCore.registerExtension(MyExtension.class, errorCallback);
```
{% endtab %}

{% tab title="Objective-C" %}
#### Example

```objective-c
NSString* extensionName = @"com.example.MyExtension";
...
    
NSError *error = nil;
if ([ACPCore registerExtension:[MyExtension class] error:&error]) {
    [ACPCore log:ACPMobileLogLevelDebug tag:extensionName message:@"MyExtension was successfully registered"];
} else {
    [ACPCore log:ACPMobileLogLevelWarning tag:extensionName message:@"An error occurred while attempting to register MyExtension"];
}
```
{% endtab %}
{% endtabs %}

## Additional Information

Read more about Mobile SDK Logging [here](../../using-mobile-extensions/mobile-core/mobile-core-api-reference.md#logging)