# Profile API reference


## extensionVersion

The `extensionVersion()` API returns the version of the Profile extension.

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public static String extensionVersion()
```
**Example**

```java
String extensionVersion = UserProfile.extensionVersion();
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static var extensionVersion: String
```
**Example**

```swift
let extensionVersion = UserProfile.extensionVersion
```

### Objective-C

**Syntax**

```objectivec
+ (nonnull NSString*) extensionVersion;
```

**Example**

```objectivec
NSString *extensionVersion = [AEPMobileUserProfile extensionVersion];
```
{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static var extensionVersion: String
```
**Example**

```swift
let extensionVersion  = ACPUserProfile.extensionVersion()
```

### Objective-C

**Syntax**

```objectivec
+ (nonnull NSString*) extensionVersion;
```

**Example**

```objectivec
NSString *extensionVersion = [ACPUserProfile extensionVersion];
```

{% endtab %}

{% tab title="React Native" %}

### JavaScript

```jsx
ACPUserProfile.extensionVersion().then(extensionVersion => console.log("AdobeExperienceSDK: ACPUserProfile version: " + extensionVersion));
```
{% endtab %}

{% tab title="Flutter" %}

### Dart

```dart
String extensionVersion = await FlutterACPUserProfile.extensionVersion;
```
{% endtab %}

{% tab title="Cordova" %}

### Cordova

```jsx
ACPUserProfile.extensionVersion(function(version) {  
   console.log("ACPUserProfile version: " + version);
}, function(error) {  
   console.log(error);  
});
```
{% endtab %}

{% tab title="Unity" %}

### C\#

```csharp
string extensionVersion = ACPUserProfile.ExtensionVersion();
```
{% endtab %}

{% tab title="Xamarin" %}

### C\#

```csharp
string extensionVersion = ACPUserProfile.ExtensionVersion();
```
{% endtab %}
{% endtabs %}

## getUserAttributes

The `getUserAttributes()` API gets the user profile attributes with the given keys.

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public static void getUserAttributes(List<String> keys, AdobeCallback<Map<String, Object>> callback)
```

* _callback_ is invoked after the customer attributes are available.

**Example**

A retail application wants to get the `itemsAddedToCart` user data when processing checkout.

When `AdobeCallbackWithError` is provided, if the operation times out \(5s\) or an unexpected error occurs, the `fail` method is called with the appropriate `AdobeError`.

```java
UserProfile.getUserAttributes(Arrays.asList("itemsAddedToCart"), new AdobeCallbackWithError<Map<String, Object>>() {
            @Override
            public void fail(AdobeError adobeError) {
                // your customized code
            }
            @Override
            public void call(Map<String, Object> stringObjectMap) {
                     // your customized code
            }
        });
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
static func getUserAttributes(attributeNames: [String], completion: @escaping ([String: Any]?, AEPError) -> Void)
```
* _completion_ is the callback `function` which will be called with user attributes.

**Example**

A retail application wants to get the `itemsAddedToCart` user data when processing checkout.

When the callback is provided, if the operation times out \(5s\) or an unexpected error occurs, the `completion` method is called with the appropriate `AEPError`.

```swift
UserProfile.getUserAttributes(attributeNames: ["itemsAddedToCart"]) { attributes, error in
// your customized code
}
```
### Objective-C

**Syntax**

```objectivec
+ (void)getUserAttributesWithAttributeNames:(NSArray<NSString *> * _Nonnull) comletion:^(NSDictionary<NSString *,id> * _Nullable, enum AEPError)
```

**Example**

```objectivec
NSArray *attributes = @[@"itemsAddedToCart"];
[AEPMobileUserProfile getUserAttributesWithAttributeNames:attributes completion:^(NSDictionary<NSString *,id> * _Nullable, enum AEPError) {
        // your customized code
}];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func getUserAttributes(_ attributeNames: [String]?, withCompletionHandler completionHandler:([AnyHashable : Any]?, Error?) -> Void)
```
* _completionHandler_ is invoked after the customer attributes are available, or _error_ if an unexpected error occurs or the request times out. The default timeout is 5s.

**Example**

A retail application wants to get the `itemsAddedToCart` user data when processing checkout.

```swift
ACPUserProfile.getUserAttributes(["itemsAddedToCart"], withCompletionHandler: {(dict: [AnyHashable: Any]?, error: Error?) -> Void in
              // your customized code
})
```

### Objective-C

**Syntax**

```objectivec
+ (void) getUserAttributes: (nullable NSArray <NSString*>*) attributNames withCompletionHandler: (nonnull void (^) (NSDictionary* __nullable userAttributes, NSError* _Nullable error)) completionHandler
```

**Example**

```objectivec
[ACPUserProfile getUserAttributes:attributes withCompletionHandler:^(NSDictionary* dict, NSError* error){
    // your customized code
    }];
```

{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
static Future<String> getUserAttributes(List<String> attributeKeys) async
```

* _attributeKeys_ is an array of strings containing the names of user profile attributes to retrieve.

**Example**

A retail application wants to get the `itemsAddedToCart` user data when processing checkout.

```dart
try {
  result = await FlutterACPUserProfile.getUserAttributes(["itemsAddedToCart"]);
} on PlatformException {
  log("Failed to get the user attributes");
}
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```javascript
ACPUserProfile.getUserAttributes = function(attributeNames, success, fail);
```

* _attributeNames_ is an array of strings containing the names of user profile attributes to retrieve.
* _success_ is a callback containing the retrieved user profile attributes.
* _fail_ is a callback containing error information if the getUserAttributes API was executed with errors.

**Example**

A retail application wants to get the `itemsAddedToCart` user data when processing checkout.

```javascript
var attributeNames = new Array();
attributeNames.push("itemsAddedToCart");
ACPUserProfile.getUserAttributes(attributeNames, handleCallback, handleError);
```
{% endtab %}

{% tab title="Unity" %}

**Syntax**

```csharp
public static void GetUserAttributes(List<string> attributeKeys, AdobeGetUserAttributesCallback callback)
```

* _attributeKeys_ is an array of strings containing the names of user profile attributes to retrieve.
* _callback_ is a callback containing the `user profile attributes` if the GetUserAttributes API executed without any errors.

**Example**

```csharp
[MonoPInvokeCallback(typeof(AdobeGetUserAttributesCallback))]
public static void HandleAdobeGetUserAttributesCallback(string userAttributes)
{
    print("Attributes are : " + userAttributes);
    results = "Attributes are : " + userAttributes;
}

var attributeKeys = new List<string>(); 
attributeKeys.Add("attrNameTest");
attributeKeys.Add("mapKey");
ACPUserProfile.GetUserAttributes(attributeKeys, HandleAdobeGetUserAttributesCallback);
```
{% endtab %}

{% tab title="Xamarin" %}

**Syntax**

**Android**

```csharp
public unsafe static void GetUserAttributes (IList<string> keys, IAdobeCallback callback);
```

* _keys_ is an IList containing the names of user profile attributes to retrieve.

**iOS**

```csharp
public unsafe static void GetUserAttributes (string[] attributNames, [BlockProxy (typeof(ObjCRuntime.Trampolines.NIDActionArity2V0))] Action<NSDictionary, NSError> completionHandler);
```

* _attributNames_ is an array of strings containing the names of user profile attributes to remove.

**Example**

A retail application wants to get the `itemsAddedToCart` user data when processing checkout.

**Android**

```csharp
var keysToRetrieve = new List<string>();
keysToRetrieve.Add("itemsAddedToCart");
ACPUserProfile.GetUserAttributes(keysToRetrieve, new AdobeCallback());

class AdobeCallback : Java.Lang.Object, IAdobeCallbackWithError
{
  public void Fail(AdobeError error)
  {
    Console.WriteLine("GetUserAttributes error: " + error.ToString());
  }

  public void Call(Java.Lang.Object retrievedAttributes)
  {
    if (retrievedAttributes != null)
    {
      var attributesDictionary = new Android.Runtime.JavaDictionary<string, object>(retrievedAttributes.Handle, Android.Runtime.JniHandleOwnership.DoNotRegister);
      foreach (KeyValuePair<string, object> pair in attributesDictionary)
      {
        Console.WriteLine("[ " + pair.Key + " : " + pair.Value + " ]");
      }
    }
    else
    {
      Console.WriteLine("GetUserAttributes callback is null.");
    }
  }
}
```

**iOS**

```csharp
var callback = new Action<NSDictionary, NSError>(handleCallback);
var keysToRetrieve = new string[] { "itemsAddedToCart" };
ACPUserProfile.GetUserAttributes(keysToRetrieve, callback);

private void handleCallback(NSDictionary content, NSError error)
{
  if (error != null)
  {
    Console.WriteLine("GetUserAttributes error: " + error.DebugDescription);
  }
  else if (content == null)
  {
    Console.WriteLine("GetUserAttributes callback is null.");
  }
  else
  {
    var attributesDictionary = (NSDictionary)content;
    foreach (KeyValuePair<NSObject, NSObject> pair in attributesDictionary)
    {
      Console.WriteLine("[ " + pair.Key + " : " + pair.Value + " ]");
    }
  }
}
```
{% endtab %}
{% endtabs %}


## registerExtension

Registers the Profile extension with the Mobile Core extension.

{% tabs %}
{% tab title="Android" %}

### Java

**Syntax**

```java
public static void registerExtension()
```

**Example**
```java
import com.adobe.marketing.mobile.UserProfile

...

UserProfile.registerExtension();
```

{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

In iOS, the registration occurs by passing UserProfile extension to the [MobileCore.registerExtensions API](../mobile-core/mobile-core-api-reference.md#registerextension-s).

### Swift

**Syntax**

```swift
static func registerExtensions(_ extensions: [NSObject.Type], 
                               _ completion: (() -> Void)? = nil)
```

**Example**

```swift
import AEPUserProfile

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  
  MobileCore.registerExtensions([UserProfile.self])
  // Override point for customization after application launch.
  return true;
}

```

### Objective-C

**Syntax**

```objectivec
+ (void) registerExtensions: (NSArray<Class*>* _Nonnull) extensions 
                 completion: (void (^ _Nullable)(void)) completion;
```
**Example**

```objectivec
@import AEPUserProfile;

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  
  [AEPMobileCore registerExtensions:@[AEPMobileUserProfile.class] completion:nil];
  // Override point for customization after application launch.
  return YES;
}

```

{% endtab %}
{% tab title="iOS (ACP 2.x)" %}

Register the Identity extension in your app's didFinishLaunchingWithOptions function:

### Swift

**Syntax**

```swift
static func registerExtensions()
```

**Example**

```swift

func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  ACPUserProfile.registerExtension()
  // Override point for customization after application launch.
  return true;
}
```

### Objective-C

**Syntax**

```objectivec
+ (void) registerExtension;
```
**Example**

```objectivec

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  [ACPUserProfile registerExtension];
  // Override point for customization after application launch.
  return YES;
}

```

{% endtab %}
{% endtabs %}

## removeUserAttribute

Removes the user profile attribute for the given key.

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public static void removeUserAttribute(String attributeName)
```

**Example**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

```java
UserProfile.removeUserAttribute("itemsAddedToCart");
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func removeUserAttribute(_ attributeName: String)
```
**Example**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

```swift
ACPUserProfile.removeUserAttribute("itemsAddedToCart");
```

### Objective-C

**Syntax**

```objectivec
+ (void) removeUserAttribute: (nonnull NSString*) key
```

**Example**

```objectivec
[ACPUserProfile removeUserAttribute:@"itemsAddedToCart"];
```

{% endtab %}

{% tab title="React Native" %}

**Syntax**

```jsx
removeUserAttribute(attributeName: string);
```

* _attributeName_ is a string containing the name of the user profile attribute to remove.

**Example**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

```jsx
ACPUserProfile.removeUserAttribute("itemsAddedToCart");
```

{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
static Future<void> removeUserAttribute(String attributeName) async
```

* _attributeName_ is a string containing the name of the user profile attribute to remove.

**Example**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

```dart
FlutterACPUserProfile.removeUserAttribute("itemsAddedToCart");
```

{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```javascript
ACPUserProfile.removeUserAttribute = function(attributeName, success, fail);
```

* _attributeName_ is a string containing the name of the user profile attribute to remove.
* _success_ is a callback containing a general success message if the removeUserAttribute API executed without any errors.
* _fail_ is a callback containing error information if the removeUserAttribute API was executed with errors.

**Example**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

```javascript
ACPUserProfile.removeUserAttribute("itemsAddedToCart", handleCallback, handleError);
```

{% endtab %}

{% tab title="Unity" %}

**Syntax**

```csharp
public static void RemoveUserAttribute(string attributeName)
```

* _attributeName_ is a string containing the name of the user profile attribute to remove.

**Example**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

```csharp
ACPUserProfile.RemoveUserAttribute("itemsAddedToCart");
```

{% endtab %}

{% tab title="Xamarin" %}

**Syntax**

**Android**

```csharp
public unsafe static void RemoveUserAttribute (string attributeName);
```

* _attributeName_ is a string containing the name of the user profile attribute to remove.

**iOS**

```csharp
public static void RemoveUserAttribute (string attributeName);
```

* _attributeName_ is a string containing the name of the user profile attribute to remove.

**Example**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

```csharp
ACPUserProfile.RemoveUserAttribute("itemsAddedToCart");
```

{% endtab %}
{% endtabs %}


## removeUserAttributes

Removes the user profile attributes for the given keys.

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public static void removeUserAttributes(List<String> attributeNames)
```

**Example**

You want to remove `username`, `usertype` user data when session timeout occurs.

```java
UserProfile.removeUserAttributes(Arrays.asList("username", "usertype"));
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}


### Swift

**Syntax**

```swift
public static void removeUserAttributes(List<String> attributeNames)
```

**Example**

You want to remove `username`, `usertype` user data when session timeout occurs.

```swift
UserProfile.removeUserAttributes(Arrays.asList("username", "usertype"));
```

### Objective-C

**Syntax**

```objectivec
+ (void) removeUserAttributesWithAttributeNames:(NSArray<NSString *> * _Nonnull)
```

**Example**

```objectivec
[AEPMobileUserProfile removeUserAttributesWithAttributeNames:@[@"username", @"usertype"]]
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}


### Swift

**Syntax**

```swift
static func removeUserAttributes(_ attributeNames: [String]?)
```
**Example**

You want to remove `username`, `usertype` user data when session timeout occurs.

```swift
ACPUserProfile.removeUserAttributes(["username","usertype"]);
```

### Objective-C

**Syntax**

```objectivec
+ (void) removeUserAttributes: (nonnull NSArray <NSString*>*) attributeNames
```

**Example**

```objectivec
[ACPUserProfile removeUserAttributes:@[@"username", @"usertype"]]
```

{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
static Future<void> removeUserAttributes(List<String> attributeName) async
```

* _attributeName_ is an array of strings containing the names of user profile attributes to remove.

**Example**

You want to remove `username`, `usertype` user data when session timeout occurs.

```dart
FlutterACPUserProfile.removeUserAttributes(["username", "usertype"])
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```javascript
ACPUserProfile.removeUserAttributes = function(attributeNames, success, fail);
```

* _attributeNames_ is an array of strings containing the names of user profile attributes to remove.
* _success_ is a callback containing a general success message if the removeUserAttributes API executed without any errors.
* _fail_ is a callback containing error information if the removeUserAttributes API was executed with errors.

**Example**

You want to remove `username`, `usertype` user data when session timeout occurs.

```javascript
var attributeNames = new Array();
attributeNames.push("username");
attributeNames.push("usertype");
ACPUserProfile.removeUserAttributes(attributeNames, handleCallback, handleError);
```
{% endtab %}

{% tab title="Unity" %}

**Syntax**

```csharp
public static void RemoveUserAttributes(List<string> attributeNames)
```

* _attributeName_ is an array of strings containing the names of user profile attributes to remove.

**Example**

You want to remove `username`, `usertype` user data when session timeout occurs.

```csharp
var attributeKeys = new List<string>(); 
attributeKeys.Add("username");
attributeKeys.Add("usertype");
ACPUserProfile.RemoveUserAttributes(attributeKeys);
```
{% endtab %}

{% tab title="Xamarin" %}

**Syntax**

**Android**

```csharp
public unsafe static void RemoveUserAttributes (IList<string> attributeNames);
```

* _attributeNames_ is an IList containing the names of user profile attributes to remove.

**iOS**

```csharp
public static void RemoveUserAttributes (string[] attributeNames);
```

* _attributeNames_ is an array of strings containing the names of user profile attributes to remove.

**Example**

You want to remove `username`, `usertype` user data when session timeout occurs.

**Android**

```csharp
var attributes = new List<string>();
attributes.Add("username");
attributes.Add("usertype");
ACPUserProfile.RemoveUserAttributes(attributes);
```

**iOS**

```csharp
string[] attributes = new string[] { "username", "usertype" };
ACPUserProfile.RemoveUserAttributes(attributes);
```
{% endtab %}
{% endtabs %}


## updateUserAttribute

Sets the user profile attributes key and value and allows you to create or update a user profile attribute.

Remember the following information:

* If the attribute does not exist, it will be created.
* If the attribute exists, the value will be updated.
* A null attribute value removes the attribute.


{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public static void updateUserAttribute(String attributeName, 
                                       Object attributeValue)
```

**Example**

You want to update `username` of a user obtained in the log in page :

```java
UserProfile.updateUserAttribute("username", "Will Smith");
```

{% endtab %}


{% tab title="iOS (ACP 2.x)" %}


### Swift

**Syntax**

```swift
static func updateUserAttribute(_ attributeName: String, withValue attributeValue: String?)
```
**Example**

You want to update `username` of a user obtained in the log in page:

```swift
ACPUserProfile.updateUserAttribute("username", withValue: "Will Smith");
```

### Objective-C

**Syntax**

```objectivec
+ (void) updateUserAttribute: (nonnull NSString*) attributeName withValue: (nullable NSString*) attributeValue;
```

**Example**

```objectivec
[ACPUserProfile updateUserAttribute:@"username" withValue:@"Will Smith"];
```

{% endtab %}

{% tab title="React Native" %}

**Syntax**

```jsx
updateUserAttribute(attributeName: string, attributeValue: string);
```

* _attributeName_ is a string containing the name of the user profile attribute to create or update.
* _attributeValue_ must be a string, number, or array containing the user profile attribute value.

**Example**

You want to update `username` of a user obtained in the log in page :

```jsx
ACPUserProfile.updateUserAttribute("username", "Will Smith");
```
{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
static Future<void> updateUserAttribute(String attributeName, String attributeValue) async
```

* _attributeName_ is a string containing the name of the user profile attribute to create or update.
* _attributeValue_ must be a string, number, or array containing the user profile attribute value.

**Example**

You want to update `username` of a user obtained in the log in page :

```dart
FlutterACPUserProfile.updateUserAttribute("username", "Will Smith");
```

{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```javascript
ACPUserProfile.updateUserAttribute = function(attributeName, attributeValue, success, fail);
```

* _attributeName_ is a string containing the name of the user profile attribute to create or update.
* _attributeValue_ must be a string, number, or array containing the user profile attribute value.
* _success_ is a callback containing a general success message if the updateUserAttribute API executed without any errors.
* _fail_ is a callback containing error information if the updateUserAttribute API was executed with errors.

**Example**

You want to update `username` of a user obtained in the log in page :

```javascript
ACPUserProfile.updateUserAttribute("username", "Will Smith", handleCallback, handleError);
```

{% endtab %}

{% tab title="Unity" %}

**Syntax**

```csharp
public static void UpdateUserAttribute(string attributeName, string attributeValue)
```

* _attributeName_ is a string containing the name of the user profile attribute to create or update.
* _attributeValue_ must be a string, number, or array containing the user profile attribute value.

**Example**

You want to update `username` of a user obtained in the log in page :

```csharp
ACPUserProfile.UpdateUserAttribute("username", "Will Smith");
```

{% endtab %}

{% tab title="Xamarin" %}

**Syntax**

**Android**

```csharp
public unsafe static void UpdateUserAttribute (string attributeName, Java.Lang.Object attributeValue);
```

* _attributeName_ is a string containing the name of the user profile attribute to create or update.
* _attributeValue_ must be a String, Integer, Boolean, Double, Array, or Map containing the user profile attribute value. Custom objects cannot be saved as a `UserProfile` attribute.

**iOS**

```csharp
public static void UpdateUserAttribute (string attributeName, string attributeValue);
```

* _attributeName_ is a string containing the name of the user profile attribute to create or update.
* _attributeValue_ is a string containing the user profile attribute value.

**Example**

You want to update `username` of a user obtained in the log in page :

```csharp
ACPUserProfile.updateUserAttribute("username", "Will Smith");
```

{% endtab %}
{% endtabs %}

## updateUserAttributes

Sets the user profile attributes key and value.

Allows you to create/update a batch of user profile attributes:

* String, Integer, Boolean, Double, Array, Map are valid type of user profile attributes.
* Custom objects cannot be saved as a `UserProfile` attribute.
* If the attribute does not exist, it is created.
* If the attribute already exists, the value is updated.
* A null attribute value will remove the attribute.

{% tabs %}
{% tab title="Android" %}

**Syntax**

```java
public static void updateUserAttributes(Map<String, Object> attributeMap)
```

**Example**

You want to update `username, usertype` of a user obtained in the log in page :

```java
HashMap<String, Object> profileMap = new HashMap<>();
profileMap.put("username","Will Smith");
profileMap.put("usertype","Actor");
UserProfile.updateUserAttributes(profileMap);
```
{% endtab %}

{% tab title="iOS (AEP 3.x)" %}

### Swift

**Syntax**

```swift
public static func updateUserAttributes(attributeDict: [String: Any])
```
**Example**

You want to update `username, usertype` of a user obtained in the log in page :

```swift
var profileMap = [AnyHashable: Any]()
profileMap["username"] = "will_smith"
profileMap["usertype"] = "Actor"
UserProfile.updateUserAttributes(attributeDict: profileMap)
```

### Objective-C

**Syntax**

```objectivec
+ (void)updateUserAttributesWithAttributeDict:(NSDictionary<NSString *,id> * _Nonnull)
```

**Example**

```objectivec
NSMutableDictionary *profileMap = [NSMutableDictionary dictionary];
[profileMap setObject:@"username" forKey:@"will_smith"];
[profileMap setObject:@"usertype" forKey:@"Actor"];
[AEPMobileUserProfile updateUserAttributesWithAttributeDict:profileMap];
```

{% endtab %}

{% tab title="iOS (ACP 2.x)" %}

### Swift

**Syntax**

```swift
static func updateUserAttributes(_ attributeMap: [AnyHashble: Any])
```
**Example**

You want to update `username, usertype` of a user obtained in the log in page :

```swift
var profileMap = [AnyHashable: Any]()
profileMap["username"] = "will_smith"
profileMap["usertype"] = "Actor"
ACPUserProfile.updateUserAttributes(profileMap)
```

### Objective-C

**Syntax**

```objectivec
+ (void) updateUserAttributes: (nonnull NSDictionary*) attributeMap
```

**Example**

```objectivec
NSMutableDictionary *profileMap = [NSMutableDictionary dictionary];
[profileMap setObject:@"username" forKey:@"will_smith"];
[profileMap setObject:@"usertype" forKey:@"Actor"];
[ACPUserProfile updateUserAttributes:profileMap];
```

{% endtab %}

{% tab title="React Native" %}

**Syntax**

```jsx
updateUserAttributes(attributeMap: {string: any});
```

**Example**

You want to update `username, usertype` of a user obtained in the log in page :

```jsx
ACPUserProfile.updateUserAttributes({"username":"will_smith", "usertype":"Actor"});
```
{% endtab %}

{% tab title="Flutter" %}

**Syntax**

```dart
static Future<void> updateUserAttributes(Map<String, Object> attributeMap) async
```

* _attributeMap_ is a object containing a batch of user profile attributes to create or update.

**Example**

You want to update `username, usertype` of a user obtained in the log in page :

```dart
FlutterACPUserProfile.updateUserAttributes({"username":"will_smith", "usertype":"Actor"});
```
{% endtab %}

{% tab title="Cordova" %}

**Syntax**

```javascript
ACPUserProfile.updateUserAttributes = function(attributes, success, fail);
```

* _attributes_ is a object containing a batch of user profile attributes to create or update.
* _success_ is a callback containing a general success message if the updateUserAttributes API executed without any errors.
* _fail_ is a callback containing error information if the updateUserAttributes API was executed with errors.

**Example**

You want to update `username, usertype` of a user obtained in the log in page :

```javascript
var username = "will_smith";
var usertype = "Actor";
var attributes = {"username":username, "usertype":usertype};
ACPUserProfile.updateUserAttributes(attributes, handleCallback, handleError);
```
{% endtab %}

{% tab title="Unity" %}

**Syntax**

```csharp
public static void UpdateUserAttributes(Dictionary<string, object> attributeMap)
```

* _attributeMap_ is a object containing a batch of user profile attributes to create or update.

**Example**

You want to update `username, usertype` of a user obtained in the log in page :

```csharp
var dict = new Dictionary<string, object>();
dict.Add("username", "will_smith");
dict.Add("usertype", "Actor");
ACPUserProfile.UpdateUserAttributes(dict);
```
{% endtab %}

{% tab title="Xamarin" %}

**Syntax**

**Android**

```csharp
public unsafe static void UpdateUserAttributes (IDictionary<string, Java.Lang.Object> attributeMap);
```

* _attributeMap_ is a object containing a batch of user profile attributes to create or update.

**iOS**

```csharp
public static void UpdateUserAttributes (NSDictionary attributeMap);
```

* _attributeMap_ is a object containing a batch of user profile attributes to create or update.

**Example**

You want to update `username, usertype` of a user obtained in the log in page :

**Android**

```csharp
var attributes = new Dictionary<string, Java.Lang.Object>();
attributes.Add("username", "will_smith");
attributes.Add("usertype", "Actor");
ACPUserProfile.UpdateUserAttributes(attributes);
```

**iOS**

```csharp
 var attributes = new NSMutableDictionary<NSString, NSString>
 {
   ["username"] = new NSString("will_smith"),
   ["usertype"] = new NSString("Actor")
 };
ACPUserProfile.updateUserAttributes(attributes);
```
{% endtab %}
{% endtabs %}