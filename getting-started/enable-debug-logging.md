# Enable debug logging

Debug logging is an optional, yet critical SDK feature. It helps you ensure that the SDK is working as intended. Below is a table that explains levels of logging available and when they may be used:

| Log Level | Description |
| :--- | :--- |
| Error | This log level provides the details about unrecoverable errors that occurred during SDK implementation. |
| Warning | In addition to the detail from _Error_ log level, _Warning_ provides error information during SDK integration. This log level might indicate that a request has been made to the SDK, but the SDK might be unable to perform the requested task. For example, this log level might be used when catching an unexpected, but recoverable, exception and printing its message. |
| Debug | In addition to detail from the _Warning_ log level, _Debug_ also provides high-level information about how the SDK processes network requests/responses data. |
| Verbose | In addition to detail from the _Debug_ level, _Verbose_ provides detailed, low-level information about how SDK processes database interactions and SDK events. |

To enable debug logging, use the following methods:

{% tabs %}
{% tab title="Android" %}
## Java

```java
MobileCore.setLogLevel(LoggingMode.DEBUG);
// MobileCore.setLogLevel(LoggingMode.VERBOSE);
// MobileCore.setLogLevel(LoggingMode.WARNING);
// MobileCore.setLogLevel(LoggingMode.ERROR);
```
{% endtab %}

{% tab title="iOS" %}
## Objective-C

```objectivec
[ACPCore setLogLevel:ACPMobileLogLevelDebug];
// [ACPCore setLogLevel:ACPMobileLogLevelVerbose];
// [ACPCore setLogLevel:ACPMobileLogLevelWarning];
// [ACPCore setLogLevel:ACPMobileLogLevelError];
```

## Swift

```swift
ACPCore.setLogLevel(ACPMobileLogLevel.debug)
// ACPCore.setLogLevel(ACPMobileLogLevel.verbose)
// ACPCore.setLogLevel(ACPMobileLogLevel.warning)
// ACPCore.setLogLevel(ACPMobileLogLevel.error)
```
{% endtab %}

{% tab title="React Native" %}
## Javascript

```jsx
ACPCore.setLogLevel(ACPMobileLogLevel.DEBUG);
ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
ACPCore.setLogLevel(ACPMobileLogLevel.WARNING);
ACPCore.setLogLevel(ACPMobileLogLevel.ERROR);
```
{% endtab %}
{% endtabs %}

