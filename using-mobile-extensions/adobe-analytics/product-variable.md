# Products variable

## Set the products variable

Since the products variable cannot be set by processing rules, you need to set serialized events directly on the hits that are sent to Analytics.

To set the products variable, set a context data key to `&&products`, and set the value to the products or merchandising variable. For more information, see the [implementing a merchandising variable tutorial](https://docs.adobe.com/content/help/en/analytics/components/variables/merchandising-variables/var-merchandising.html).

{% tabs %}
{% tab title="Android" %}
### Java <a id="java-2"></a>

**Syntax** <a id="syntax"></a>

```java
cdata.put("&&products", "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]");
```

**Example** <a id="example"></a>

```java
//create a context data dictionary
HashMap cdata = new HashMap<String, String>();
// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
cdata.put("&&products", ";Running Shoes;1;69.95,;Running Socks;10;29.99");
cdata.put("myapp.purchase", "1");
cdata.put("myapp.purchaseid", "1234567890");
// send the tracking call - use either a trackAction or trackState call.
// trackAction example:
MobileCore.trackAction("purchase", cdata);
// trackState example:
MobileCore.trackState("Order Confirmation", cdata);
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

**Syntax**

```objectivec
[contextData setObject:@"Category;Product;Quantity;Price[,Category;Product;Quantity;Price]" forKey:@"&&products"];
```

**Example**

```objectivec
//create a context data dictionary
NSMutableDictionary *contextData = [NSMutableDictionary dictionary];

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
[contextData setObject:@";Running Shoes;1;69.95,;Running Socks;10;29.99" forKey:@"&&products"];
[contextData setObject:@"1234567890" forKey:@"m.purchaseid"];
[contextData setObject:@"1" forKey:@"m.purchase"];

// send the tracking call - use either a trackAction or trackState call.
// trackAction example:
[ACPCore trackAction:@"purchase" data:contextData];
// trackState example:
[ACPCore trackState:@"Order Confirmation" data:contextData];
```

### Swift

**Syntax**

```swift
contextData["&&products"] = "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]"
```

**Example**

```swift
//create a context data dictionary
var contextData:[String:String]=[:] 

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
contextData["&&products"] = ";Running Shoes;1;69.95,;Running Socks;10;29.99"
contextData["m.purchaseid"] = "1234567890"
contextData["m.purchase"] = "1"

// send the tracking call - use either a trackAction or trackState call.
// trackAction example:
ACPCore.trackAction("purchase", data: contextData)
// trackState example:
ACPCore.trackState("Order Confirmation", data: contextData)
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Syntax**

```jsx
contextData["&&products"] = "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]";
```

**Example**

```jsx
//create a context data dictionary
var contextData = {};

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
contextData["&&products"] = ";Running Shoes;1;69.95,;Running Socks;10;29.99";
contextData["m.purchaseid"] = "1234567890";
contextData["m.purchase"] = "1";

// send the tracking call - use either a trackAction or TrackState call.
// trackAction example:
ACPCore.trackAction("purchase", contextData);
// trackState example:
ACPCore.trackState("Order Confirmation", contextData);
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Syntax**

```dart
contextData["&&products"] = "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]";
```

**Example**

```dart
//create a context data dictionary
var contextData = {};

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
contextData["&&products"] = ";Running Shoes;1;69.95,;Running Socks;10;29.99";
contextData["m.purchaseid"] = "1234567890";
contextData["m.purchase"] = "1";

// send the tracking call - use either a trackAction or TrackState call.
// trackAction example:
FlutterACPCore.trackAction("purchase", data: contextData);
// trackState example:
FlutterACPCore.trackState("Order Confirmation", data: contextData);
```
{% endtab %}
{% endtabs %}

A sample network request can be seen in the image below:

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-Lf1Mc1caFdNCK_mBwhe%2F-Lf1N06T8hdv0-r5jPPN%2F-Lf1N9cAUiiQNZvVBMFC%2Fproducts-bloodhound.png?generation=1558039282074316&alt=media)

_`products`_ is set directly on the image request, and the other variables are set as context data. All context data variables must be mapped by using processing rules:

![](../../.gitbook/assets/map-products.png)

You do **not** need to map the `products` variable using processing rules because it is set directly on the image request by the SDK.

## Products variable with merchandising eVars and product-specific events <a id="products-variable-with-merchandising-evars-and-product-specific-events"></a>

The following code samples show an example of the products variable with merchandising eVars and product-specific events.

{% tabs %}
{% tab title="Android" %}
### Java

**Example**

```java
//create a context data dictionary 
HashMap cdata = new HashMap<String, String>(); 

// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
cdata.put("&&events", "event1"); 
cdata.put("&&products", ";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99"); 
cdata.put("myapp.purchase", "1"); 
cdata.put("myapp.purchaseid", "1234567890"); 

// send the tracking call - use either a trackAction or trackState call. 
// trackAction example: 
MobileCore.trackAction("purchase", cdata); 
// trackState example: 
MobileCore.trackState("Order Confirmation", cdata);
```
{% endtab %}

{% tab title="iOS" %}
### Objective-C

**Example**

```objectivec
//create a context data dictionary 
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 

// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
[contextData setObject:@"event1" forKey:@"&&events"]; 
[contextData setObject:@";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99" forKey:@"&&products"]; 
[contextData setObject:@"1234567890" forKey:@"m.purchaseid"]; 
[contextData setObject:@"1" forKey:@"m.purchase"]; 

// send the tracking call - use either a trackAction or trackState call. 
// trackAction example: 
[ACPCore trackAction:@"purchase" data:contextData]; 
// trackState example: 
[ACPCore trackState:@"Order Confirmation" data:contextData];
```

### Swift

**Example**

```swift
//create a context data dictionary
var contextData:[String:String]=[:] 

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
contextData["&&events"] = "event1"
contextData["&&products"] = ";Running Shoes;1;69.95,;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99"
contextData["m.purchaseid"] = "1234567890"
contextData["m.purchase"] = "1"

// send the tracking call - use either a trackAction or trackState call.
// trackAction example:
ACPCore.trackAction("purchase", data: contextData)
// trackState example:
ACPCore.trackState("Order Confirmation", data: contextData)
```
{% endtab %}

{% tab title="React Native" %}
### JavaScript

**Example**

```jsx
//create a context data dictionary
var contextData = {};

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
contextData["&&events"] = "event1";
contextData["&&products"] = ";Running Shoes;1;69.95,;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99";
contextData["m.purchaseid"] = "1234567890";
contextData["m.purchase"] = "1";

// send the tracking call - use either a trackAction or TrackState call.
// trackAction example:
ACPCore.trackAction("purchase", contextData);
// trackState example:
ACPCore.trackState("Order Confirmation", contextData);
```
{% endtab %}

{% tab title="Flutter" %}
### Dart

**Example**

```dart
//create a context data dictionary
var contextData = {};

// add products, a purchase id, a purchase context data key, and any other data you want to collect.
// Note the special syntax for products
contextData["&&events"] = "event1";
contextData["&&products"] = ";Running Shoes;1;69.95,;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99";
contextData["m.purchaseid"] = "1234567890";
contextData["m.purchase"] = "1";

// send the tracking call - use either a trackAction or TrackState call.
// trackAction example:
FlutterACPCore.trackAction("purchase", data: contextData);
// trackState example:
FlutterACPCore.trackState("Order Confirmation", data: contextData);
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you trigger a product-specific event by using the `&&products` variable, you must also set that event in the `&&events` variable. If you do not set that event, it is filtered out during processing.
{% endhint %}

