# Assurance API reference

## extensionVersion

Returns the current version of the AEP Assurance extension

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
public static String extensionVersion()
```

**Example**

```java
Assurance.extensionVersion()
```
{% endtab %}

{% tab title="iOS" %}

### Swift

**Example**

```swift
AEPAssurance.extensionVersion()
```

### Objective-C

**Syntax**

```objectivec
+ (nonnull NSString*) extensionVersion;
```

**Example**

```objectivec
[AEPAssurance extensionVersion];
```

{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Example**

```objectivec
AEPAssurance.extensionVersion().then(version => console.log("AdobeExperienceSDK: AEP Assurance version: " + version));
```
{% endtab %}

{% tab title="Flutter" %}

### Dart

**Syntax**

```dart
static Future<String> get extensionVersion async
```

**Example**

```dart
assuranceVersion = await FlutterAssurance.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```javascript
AEPAssurance.extensionVersion = function(success, fail);
```

**Example**

```javascript
AEPAssurance.extensionVersion(function(version) {  
   console.log("AEPAssurance version: " + version);
}, function(error) {  
   console.log(error);  
});
```
{% endtab %}

{% tab title="Unity" %}

### C\#

**Syntax**

```text
public static string ExtensionVersion()
```

**Example**

```text
string version = AEPAssurance.ExtensionVersion();
print(LOG_TAG + "Assurance version: "+version);
```
{% endtab %}

{% tab title="Xamarin" %}
### C\#

**Example**

```text
string version = AEPAssurance.ExtensionVersion()  
Console.WriteLine("AEPAssurance version installed is: " + version);
```
{% endtab %}
{% endtabs %}

## startSession

The `startSession` API needs to be called to begin a AEP Assurance session. When called, the Mobile SDK displays a PIN authentication overlay to begin a session.

{% hint style="info" %}
You may call this API when the app launches with a url \(see code snippet below for sample usage\)
{% endhint %}

{% tabs %}
{% tab title="Android" %}
This API is optional for Android.

Android does not require this API to be called. When the `registerExtension` API is called, AEP Assurance extension registers the app lifecycle handlers which automatically pick up any deep links and use them to start the session.

### Java

**Syntax**

```java
public static void startSession(final String url)
```

**Example**

```java
 Assurance.startSession(url);
```
{% endtab %}

{% tab title="iOS" %}

### Swift

**Example**

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

### Objective-C

**Syntax**

```objectivec
+ (void) startSession: (NSURL* _Nonnull) url;
```

**Example**

```objectivec
- (BOOL)application:(UIApplication *)app openURL:(nonnull NSURL *)url options:(nonnull NSDictionary<UIApplicationOpenURLOptionsKey,id> *)options {
    [AEPAssurance startSession:url];
    return false;
}
```

{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Example**

```javascript
AEPAssurance.startSession("your-griffon-session-url");
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Syntax**

```dart
static Future<void> startSession(String url);
```

**Example**

```dart
FlutterAssurance.startSession(url);
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```javascript
AEPAssurance.startSession = function(sessionurl,success, fail);
```

**Example**

```javascript
AEPAssurance.startSession(url,function(result) {  
   console.log("AdobeExperenceSDK: AEPAssurance session started succesfully: " + result);
}, function(error) {  
   console.log("AdobeExperenceSDK: Failed to start AEPAssurance session: " + error);
});
```
{% endtab %}

{% tab title="Unity" %}

### C#

**Syntax**

```text
public static void StartSession(string url)
```

**Example**

```text
AEPAssurance.StartSession(url);
```
{% endtab %}

{% tab title="Xamarin" %}
### C#

```text
AEPAssurance.StartSession(url);
```
{% endtab %}
{% endtabs %}

