# Product variable

## Products variable   <a id="products-variable"></a>

The products variable cannot be set by using processing rules. In the Adobe Experience Platform SDK, you must use a special syntax in the context data parameter to set products directly on the server call.

To set the _`products`_ variable, set a context data key to `"&&products"`, and set the value by using the syntax that is defined for the _`products`_ variable:

{% tabs %}
{% tab title="Android" %}
**Java**

### **Syntax**

```java
cdata.put("&&products", "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]");
```

### **Example**

```java
//create a context data dictionary 
HashMap cdata = new HashMap<String, String>(); 

// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
cdata.put("&&products", ";Running Shoes;1;69.95,;Running Socks;10;29.99"); 
cdata.put("myapp.purchase", "1"); 
cdata.put("myapp.purchaseid", "1234567890"); 

// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
MobileCore.trackAction("purchase", cdata); 
// trackState example: 
MobileCore.trackState("Order Confirmation", cdata);
```

\*\*\*\*
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

### **Syntax**

```text
[contextData setObject:@"Category;Product;Quantity;Price[,Category;Product;Quantity;Price]" forKey:@"&&products"];
```

### **Example**

```text
//create a context data dictionary 
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 

// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
[contextData setObject:@";Running Shoes;1;69.95,;Running Socks;10;29.99" forKey:@"&&products"]; 
[contextData setObject:@"1234567890" forKey:@"m.purchaseid"]; 
[contextData setObject:@"1" forKey:@"m.purchase"]; 

// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
[ACPCore trackAction:@"purchase" data:contextData]; 
// trackState example: 
[ACPCore trackState:@"Order Confirmation" data:contextData];
```
{% endtab %}
{% endtabs %}

_`products`_ is set directly on the image request, and the other variables are set as context data. All context data variables must be mapped by using processing rules:

![](../../.gitbook/assets/map-products.png)

You do not need to map the _`products`_ variable using processing rules because it is set directly on the image request by the SDK.

## Products variable with merchandising eVars and product-specific events   <a id="products-variable-with-merchandising-evars-and-product-specific-events"></a>

Here is an example of the products variable with Merchandising eVars and product-specific events.

{% tabs %}
{% tab title="Android" %}
**Java**

### **Example**

```java
//create a context data dictionary 
HashMap cdata = new HashMap<String, String>(); 

// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
cdata.put("&&events", "event1"); 
cdata.put("&&products", ";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99"); 
cdata.put("myapp.purchase", "1"); 
cdata.put("myapp.purchaseid", "1234567890"); 

// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
MobileCore.trackAction("purchase", cdata); 
// trackState example: 
MobileCore.trackState("Order Confirmation", cdata);
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

### **Example**

```text
//create a context data dictionary 
NSMutableDictionary *contextData = [NSMutableDictionary dictionary]; 

// add products, a purchase id, a purchase context data key, and any other data you want to collect. 
// Note the special syntax for products 
[contextData setObject:@"event1" forKey:@"&&events"]; 
[contextData setObject:@";Running Shoes;1;69.95;event1=5.5;eVar1=Merchandising,;Running Socks;10;29.99" forKey:@"&&products"]; 
[contextData setObject:@"1234567890" forKey:@"m.purchaseid"]; 
[contextData setObject:@"1" forKey:@"m.purchase"]; 

// send the tracking call - use either a trackAction or TrackState call. 
// trackAction example: 
[ACPCore trackAction:@"purchase" data:contextData]; 
// trackState example: 
[ACPCore trackState:@"Order Confirmation" data:contextData];
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you trigger a product-specific event by using the `&&products` variable, you must also set that event in the `&&events` variable. If you do not set that event, it is filtered out during processing.
{% endhint %}

