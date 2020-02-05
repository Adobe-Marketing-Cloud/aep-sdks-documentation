# Register extensions and starting Core

Besides Mobile Core, all Adobe Experience Platform SDK extensions provide a `registerExtension` API. This API registers the extension with Mobile Core. After an extension is registered, it can dispatch and listen for events. You are required to register each of your extensions before making API calls and failing to do so will lead to undefined behavior.

After you register the extensions you want to use, call the `start` API in Core. This step is required to boot up the SDK for event processing.

The following code snippets demonstrate how to initialize the SDK when using the Identity, Signal, Lifecycle, and Analytics extensions:

{% tabs %}
{% tab title="Android" %}
### Java

```java
try {
    Identity.registerExtension();
    Lifecycle.registerExtension();
    Signal.registerExtension();
    Analytics.registerExtension();
    } catch (Exception e) {
       //Log the exception
    }
}
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

```objectivec
[ACPIdentity registerExtension];
[ACPLifecycle registerExtension];
[ACPSignal registerExtension];
[ACPAnalytics registerExtension];
[ACPCore start:nil];
```

### Swift

```swift
ACPIdentity.registerExtension()
ACPLifecycle.registerExtension()
ACPSignal.registerExtension()
ACPAnalytics.registerExtension()
ACPCore.start(nil)
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

```jsx
import {ACPCore, ACPLifecycle, ACPIdentity, ACPSignal, ACPMobileLogLevel} from '@adobe/react-native-acpcore';

initSDK() {
    ACPCore.setLogLevel(ACPMobileLogLevel.VERBOSE);
    ACPCore.configureWithAppId("PASTE_ENVIRONMENT_ID_HERE");
    ACPLifecycle.registerExtension();
    ACPIdentity.registerExtension();
    ACPSignal.registerExtension();
    ACPCore.start();
}
```
{% endtab %}
{% endtabs %}

