# Lifecycle API reference

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

```text
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

```java
+ (void) lifecycleStart: (nullable NSDictionary<NSString*, NSString*>*) additionalContextData;
```

**Example**

```java
[ACPCore lifecycleStart:nil];
```

If you need to collect additional lifecycle data:

```text
[ACPCore lifecycleStart:@{@"state": @"appResume"}];
```

#### Swift

```text
// Swift
ACPCore.lifecycleStart(["state": "appResume"])
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```text
ACPCore.lifecycleStart({"lifecycleStart": "myData"});
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

```java
+ (void) lifecyclePause;
```

**Example**

```java
[ACPCore lifecyclePause];
```

#### Swift

```text
// Swift
ACPCore.lifecyclePause()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

```text
ACPCore.lifecyclePause();
```
{% endtab %}
{% endtabs %}

