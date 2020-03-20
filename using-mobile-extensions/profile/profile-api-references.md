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
{% endtabs %}

## **Remove a user attribute**

Removes the given attribute name.

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

You want to remove `username`, `passowrd` user data when session timeout occurs. 

```java
UserProfile.removeUserAttributes(Arrays.asList("UserName", "Password"));
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

You want to remove `username`, `passowrd` user data when session timeout occurs. 

**Objective C**

```objectivec
[ACPUserProfile removeUserAttributes:@[@"UsesrName", @"Password"]]
```

**Swift**

```swift
ACPUserProfile.removeUserAttributes(["UsesrName","Password"]);
```

{% endtab %}
{% endtabs %}

