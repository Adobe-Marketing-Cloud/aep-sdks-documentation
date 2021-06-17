# Extension logging

It is recommended that you use the Experience Platform SDK logging API to print a message from the extension code. The Experience Platform SDKs provide the `setLogLevel` API, which is used to set one of the following logging modes:

* VERBOSE
* DEBUG
* WARNING
* ERROR 

If the current logging mode is less than verbose, the message is not printed by the Experience Platform SDKs. When debugging and testing your extension, you can set the logging mode to verbose to see all the messages flowing through the Experience Platform SDK.

The Experience Platform SDK uses the extension name as the log tag for the Adobe extensions, so that the application developer can filter the logs for a mobile extension. A similar approach can be implemented by a partner extension as seen in the examples below:

{% tabs %}
{% tab title="Android" %}
**Java example**

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

{% tab title="iOS" %}
**Objective-C example**

```objectivec
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

## Additional information

To learn more, please read the [Mobile SDK logging documentation](../../foundation-extensions/mobile-core/mobile-core-api-reference.md#logging)

