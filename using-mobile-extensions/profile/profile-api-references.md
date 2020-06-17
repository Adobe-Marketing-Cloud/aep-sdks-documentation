# Profile API reference

## Update user attributes

{% tabs %}
{% tab title="Android" %}
### **updateUserAttribute**

Sets the user profile attributes key and value and allows you to create or update a user profile attribute.

Remember the following information:

* If the attribute does not exist, it will be created.
* If the attribute exists, the value will be updated.
* A null attribute value removes the attribute.

#### **Syntax**

```java
public static void updateUserAttribute(String attributeName, 
                                       Object attributeValue)
```

#### **Example**

You want to update `username` of a user obtained in the log in page :

```java
UserProfile.updateUserAttribute("username", "Will Smith");
```

### updateUserAttributes

Sets the user profile attributes key and value.

Allows you to create/update a batch of user profile attributes:

* String, Integer, Boolean, Double, Array, Map are valid type of user profile attributes.
* Custom objects cannot be saved as a `UserProfile` attribute.
* If the attribute does not exist, it is created.
* If the attribute already exists, the value is updated.
* A null attribute value will remove the attribute.

#### **Syntax**

```java
public static void updateUserAttributes(Map<String, Object> attributeMap)
```

#### **Example**

You want to update `username, usertype` of a user obtained in the log in page :

```java
HashMap<String, Object> profileMap = new HashMap<>();
profileMap.put("username","Will Smith");
profileMap.put("usertype","Actor");
UserProfile.updateUserAttributes(profileMap);
```
{% endtab %}

{% tab title="iOS" %}
### updateUserAttribute

Sets the user profile attributes key and value and allows you to create or update a user profile attribute.

Remember the following information:

* If the attribute does not exist, it will be created.
* If the attribute already exists, then the value will be updated.
* A null attribute value will remove the attribute.

#### **Syntax**

```java
+ (void) updateUserAttribute: (nonnull NSString*) attributeName withValue: (nullable NSString*) attributeValue;
```

#### **Examples**

You want to update `username` of a user obtained in the log in page:

**Objective-C**

```text
[ACPUserProfile updateUserAttribute:@"username" withValue:@"Will Smith"];
```

**Swift**

```java
ACPUserProfile.updateUserAttribute("username", withValue: "Will Smith");
```

### updateUserAttributes

Sets the user profile attributes key and value.

Allows to create/update a batch of user profile attributes:

* String, Integer, Boolean, Double, Array, Map are valid type of user profile attributes.
* We do not allow custom objects to be saved as a `UserProfile` attribute.
* If the attribute already exists, then the value will be updated.
* If the attribute does not exist, it will be created.

A null attribute value will remove the attribute.

#### **Syntax**

```text
+ (void) updateUserAttributes: (nonnull NSDictionary*) attributeMap
```

#### **Examples**

You want to update `username, usertype` of a user obtained in the log in page :

**Objective C**

```objectivec
NSMutableDictionary *profileMap = [NSMutableDictionary dictionary];
[profileMap setObject:@"username" forKey:@"will_smith"];
[profileMap setObject:@"usertype" forKey:@"Actor"];
[ACPUserProfile updateUserAttributes:profileMap];
```

**Swift**

```swift
var profileMap = [AnyHashable: Any]()
profileMap["username"] = "will_smith"
profileMap["usertype"] = "Actor"
ACPUserProfile.updateUserAttributes(profileMap)
```
{% endtab %}

{% tab title="Cordova" %}
### **updateUserAttribute**

Sets the user profile attributes key and value and allows you to create or update a user profile attribute.

Remember the following information:

* If the attribute does not exist, it will be created.
* If the attribute exists, the value will be updated.
* A null attribute value removes the attribute.

#### **Syntax**

```javascript
ACPUserProfile.updateUserAttribute = function(attributeName, attributeValue, success, fail);
```

* _attributeName_ is a string containing the name of the user profile attribute to create or update.
* _attributeValue_ must be a string, number, or array containing the user profile attribute value.
* _success_ is a callback containing a general success message if the updateUserAttribute API executed without any errors.
* _fail_ is a callback containing error information if the updateUserAttribute API was executed with errors.

#### **Example**

You want to update `username` of a user obtained in the log in page :

```javascript
ACPUserProfile.updateUserAttribute("username", "Will Smith", handleCallback, handleError);
```

### updateUserAttributes

Sets the user profile attributes key and value.

Allows you to create/update a batch of user profile attributes:

* String, Number, and Array are valid types of user profile attributes.
* Custom objects cannot be saved as a `UserProfile` attribute.
* If the attribute does not exist, it is created.
* If the attribute already exists, the value is updated.
* A null attribute value will remove the attribute.

#### **Syntax**

```javascript
ACPUserProfile.updateUserAttributes = function(attributes, success, fail);
```

* _attributes_ is a object containing a batch of user profile attributes to create or update.
* _success_ is a callback containing a general success message if the updateUserAttributes API executed without any errors.
* _fail_ is a callback containing error information if the updateUserAttributes API was executed with errors.

#### **Example**

You want to update `username, usertype` of a user obtained in the log in page :

```javascript
var username = "will_smith";
var usertype = "Actor";
var attributes = {"username":username, "usertype":usertype};
ACPUserProfile.updateUserAttributes(attributes, handleCallback, handleError);
```
{% endtab %}
{% endtabs %}

## **Remove user attributes**

{% tabs %}
{% tab title="Android" %}
### **removeUserAttribute**

Removes the user profile attribute for the given key.

#### **Syntax**

```java
public static void removeUserAttribute(String attributeName)
```

#### **Example**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

```java
UserProfile.removeUserAttribute("itemsAddedToCart");
```

### **removeUserAttributes**

Removes the user profile attributes for the given keys.

#### **Syntax**

```java
public static void removeUserAttributes(List<String> attributeNames)
```

#### **Example**

You want to remove `username`, `usertype` user data when session timeout occurs.

```java
UserProfile.removeUserAttributes(Arrays.asList("username", "usertype"));
```
{% endtab %}

{% tab title="iOS" %}
### removeUserAttribute

Removes the user profile attribute for the given key.

#### **Syntax**

```objectivec
+ (void) removeUserAttribute: (nonnull NSString*) key
```

#### **Examples**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

**Objective C**

```objectivec
[ACPUserProfile removeUserAttribute:@"itemsAddedToCart"];
```

**Swift**

```swift
ACPUserProfile.removeUserAttribute("itemsAddedToCart");
```

### removeUserAttributes

Removes the user profile attributes for the given keys.

#### **Syntax**

```objectivec
+ (void) removeUserAttributes: (nonnull NSArray <NSString*>*) attributeNames
```

#### **Examples**

You want to remove `username`, `usertype` user data when session timeout occurs.

**Objective C**

```objectivec
[ACPUserProfile removeUserAttributes:@[@"username", @"usertype"]]
```

**Swift**

```swift
ACPUserProfile.removeUserAttributes(["username","usertype"]);
```
{% endtab %}

{% tab title="Cordova" %}
### **removeUserAttribute**

Removes the user profile attribute for the given key.

#### **Syntax**

```javascript
ACPUserProfile.removeUserAttribute = function(attributeName, success, fail);
```

* _attributeName_ is a string containing the name of the user profile attribute to remove.
* _success_ is a callback containing a general success message if the removeUserAttribute API executed without any errors.
* _fail_ is a callback containing error information if the removeUserAttribute API was executed with errors.

#### **Example**

A retail application wants to remove the `itemsAddedToCart` user data after the product is purchased.

```javascript
ACPUserProfile.removeUserAttribute("itemsAddedToCart", handleCallback, handleError);
```

### **removeUserAttributes**

Removes the user profile attributes for the given keys.

#### **Syntax**

```javascript
ACPUserProfile.removeUserAttributes = function(attributeNames, success, fail);
```

* _attributeNames_ is an array of strings containing the names of user profile attributes to remove.
* _success_ is a callback containing a general success message if the removeUserAttributes API executed without any errors.
* _fail_ is a callback containing error information if the removeUserAttributes API was executed with errors.

#### **Example**

You want to remove `username`, `usertype` user data when session timeout occurs.

```javascript
var attributeNames = new Array();
attributeNames.push("username");
attributeNames.push("usertype");
ACPUserProfile.removeUserAttributes(attributeNames, handleCallback, handleError);
```
{% endtab %}
{% endtabs %}

## **Get user attributes**

{% tabs %}
{% tab title="Android" %}
### **getUserAttributes**

Gets the user profile attributes with the given keys.

#### **Syntax**

```java
public static void getUserAttributes(List<String> keys, AdobeCallback<Map<String, Object>> callback)
```

* _callback_ is invoked after the customer attributes are available.

#### **Example**

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

{% tab title="iOS" %}
### **getUserAttributes**

Gets the user profile attributes with the given keys.

#### **Syntax**

```objectivec
+ (void) getUserAttributes: (nullable NSArray <NSString*>*) attributNames withCompletionHandler: (nonnull void (^) (NSDictionary* __nullable userAttributes, NSError* _Nullable error)) completionHandler
```

* _completionHandler_ is invoked after the customer attributes are available, or _error_ if an unexpected error occurs or the request times out. The default timeout is 5s.

#### **Examples**

A retail application wants to get the `itemsAddedToCart` user data when processing checkout.

**Objective C**

```objectivec
[ACPUserProfile getUserAttributes:attributes withCompletionHandler:^(NSDictionary* dict, NSError* error){
    // your customized code
    }];
```

**Swift**

```swift
ACPUserProfile.getUserAttributes(["itemsAddedToCart"], withCompletionHandler: {(dict: [AnyHashable: Any]?, error: Error?) -> Void in
              // your customized code
})
```
{% endtab %}

{% tab title="Cordova" %}
### **getUserAttributes**

Gets the user profile attributes with the given keys.

#### **Syntax**

```javascript
ACPUserProfile.getUserAttributes = function(attributeNames, success, fail);
```

* _attributeNames_ is an array of strings containing the names of user profile attributes to retrieve.
* _success_ is a callback containing the retrieved user profile attributes.
* _fail_ is a callback containing error information if the getUserAttributes API was executed with errors.

#### **Example**

A retail application wants to get the `itemsAddedToCart` user data when processing checkout.

```javascript
var attributeNames = new Array();
attributeNames.push("itemsAddedToCart");
ACPUserProfile.getUserAttributes(attributeNames, handleCallback, handleError);
```
{% endtab %}
{% endtabs %}

