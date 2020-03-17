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

```text
+ (void) lifecycleStart: (nullable NSDictionary<NSString*, NSString*>*) additionalContextData;
```

**Example**

```text
[ACPCore lifecycleStart:nil];
```

If you need to collect additional lifecycle data:

```text
[ACPCore lifecycleStart:@{@"state": @"appResume"}];
```

#### Swift

```swift
ACPCore.lifecycleStart(["state": "appResume"])
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

Note: Implementing Lifecycle via JavaScript may lead to inaccurate Lifecycle metrics, therefore we recommend implementing Lifecycle in native Android and iOS code. However, these APIs are still provided in JavaScript to support flexible Lifecycle implementations.

**Syntax**

```jsx
lifecycleStart(additionalContextData?: { string: string });
```

**Example**

```jsx
ACPCore.lifecycleStart({"lifecycleStart": "myData"});
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

> Note: Implementing Lifecycle via Dart may lead to inaccurate Lifecycle metrics, therefore we recommend implementing Lifecycle in native Android and iOS code. However, these APIs are still provided in Dart to support flexible Lifecycle implementations.

**Syntax**

```dart
Future<void> lifecycleStart (Map<String, String> contextData);
```

**Example**

```dart
FlutterACPCore.lifecycleStart({"lifecycleStart": "myData"});
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

```text
+ (void) lifecyclePause;
```

**Example**

```text
[ACPCore lifecyclePause];
```

#### Swift

```swift
ACPCore.lifecyclePause()
```
{% endtab %}

{% tab title="React Native" %}
#### JavaScript

> Note: Implementing Lifecycle via JavaScript may lead to inaccurate Lifecycle metrics, therefore we recommend implementing Lifecycle in native Android and iOS code. However, these APIs are still provided in JavaScript to support flexible Lifecycle implementations.

**Syntax**

```jsx
lifecyclePause();
```

**Example**

```jsx
ACPCore.lifecyclePause();
```
{% endtab %}

{% tab title="Flutter" %}
#### Dart

> Note: Implementing Lifecycle via Dart may lead to inaccurate Lifecycle metrics, therefore we recommend implementing Lifecycle in native Android and iOS code. However, these APIs are still provided in Dart to support flexible Lifecycle implementations.

**Syntax**

```dart
Future<void> lifecyclePause();
```

**Example**

```dart
FlutterACPCore.lifecyclePause();
```
{% endtab %}
{% endtabs %}

