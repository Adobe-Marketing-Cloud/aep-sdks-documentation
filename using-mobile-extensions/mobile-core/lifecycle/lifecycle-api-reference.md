# Lifecycle API reference

## Version of the Lifecycle extension

The `extensionVersion()` API returns the version of the Lifecycle extension that is registered with the Mobile Core extension.

To get the version of the Lifecycle extension, use the following code sample:

{% tabs %}
{% tab title="Android" %}
#### Java

```java
String lifecycleExtensionVersion = Lifecycle.extensionVersion();
```
{% endtab %}

{% tab title="iOS" %}
**Objective C**

```objectivec
NSString *lifecycleExtensionVersion = [AEPMobileLifecycle extensionVersion];
```

**Swift**

```swift
let lifecycleExtensionVersion  = Lifecycle.extensionVersion
```
{% endtab %}
{% endtabs %}

## Lifecycle Start

You can use this API to start a new lifecycle session or resume a previously paused lifecycle session. If a previously paused session timed out, then a new session is created. If a current session is running, then calling this method does nothing.

### lifecycleStart <a id="lifecycleStart"></a>

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void lifecycleStart(final Map<String, String> additionalContextData);
```

**Example**

```java
MobileCore.lifecycleStart(null);
```

If you need to collect additional lifecycle data:

```java
contextData.put("myapp.category", "Game");
MobileCore.lifecycleStart(additionalContextData);
```

{% hint style="warning" %}
This method should be called from the Activity onResume method.
{% endhint %}
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

**Syntax**

```swift
@objc(lifecycleStart:)
static func lifecycleStart(additionalContextData: [String: Any]?) 
```

**Example**

```objective-c
[AEPMobileCore lifecycleStart:nil];
```

If you need to collect additional lifecycle data:

```objective-c
[AEPMobileCore lifecycleStart:@{@"contextDataKey": @"contextDataVal"}];
```

#### Swift

```swift
MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
```
{% endtab %}
{% endtabs %}

### Lifecycle Pause

Use this API to pause or stop the collection of lifecycle data.

### lifecyclePause <a id="lifecyclePause"></a>

{% tabs %}
{% tab title="Android" %}
#### Java

**Syntax**

```java
public static void lifecyclePause()
```

**Example**

```java
MobileCore.lifecyclePause();
```
{% endtab %}

{% tab title="iOS" %}
#### Objective-C

**Syntax**

```swift
@objc(lifecyclePause)
static func lifecyclePause()
```

**Example**

```objective-c
[AEPMobileCore lifecyclePause];
```

#### Swift

```swift
MobileCore.lifecyclePause()
```
{% endtab %}


{% endtabs %}

