# Assurance API reference

## extensionVersion

Returns the current version of the AEPAssurance extension

{% tabs %}
{% tab title="Android" %}
### Java

### Syntax

```java
public static String extensionVersion()
```

### Example

```java
Assurance.extensionVersion()
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

### Syntax

```objectivec
+ (nonnull NSString*) extensionVersion;
```

### Example

```objectivec
[AEPAssurance extensionVersion];
```

### Swift

### Example

```swift
AEPAssurance.extensionVersion()
```
{% endtab %}
{% endtabs %}

## startSession

The `startSession` API needs to be called to begin a AEPAssurance session. When called, SDK displays a PIN authentication overlay to begin a session.

{% hint style="info" %}
You may call this API when the app launches with a url \(see code snippet below for sample usage\)
{% endhint %}

{% tabs %}
{% tab title="Android" %}
This API is optional for Android.

Android does not require this API to be called. When the `registerExtension` API is called, Assurance extension registers the app lifecycle handlers which automatically pick up any deep links and use them to start the session.

### Java

### Syntax

```java
public static void startSession(final String url)
```

### Example

```java
 Assurance.startSession(url);
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

### Syntax

```objectivec
+ (void) startSession: (NSURL* _Nonnull) url;
```

### Example

```objectivec
- (BOOL)application:(UIApplication *)app openURL:(nonnull NSURL *)url options:(nonnull NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options {
    [AEPAssurance startSession:url];
    return false;
}
```

### Swift

### Example

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey : Any] = [:]) -> Bool {
    do {
        AEPAssurance.startSession(url)
        return false
    }
}
```

For SceneDelegate based applications

```swift
    func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
        AEPAssurance.startSession(URLContexts.first!.url)
    }
```
{% endtab %}
{% endtabs %}

