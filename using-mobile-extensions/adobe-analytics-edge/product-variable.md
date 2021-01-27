# Products variable

## Set the products variable using Experience events and the Edge extension

An Experience Event can be used to send the products variable to the Experience Edge after an XDM schema and dataset have been setup for receiving the event. For more information on creating an XDM schema, see [Basics of schema composition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#understanding-schemas) and [Create a schema using the Schema Editor](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html#tutorials). The created schema should contain a mixin for a [commerce detail object.](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md)

For more information on the products variable, see [Implementing a Merchandising Variable](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/addproductevar.html#vars).

{% tabs %}
{% tab title="Android" %}

#### Java <a id="java-2"></a>

#### Example <a id="example"></a>

```java
// build a product map for each product
HashMap<String, Object> product1 = new HashMap<>();
product1.put("SKU", "SH100");
product1.put("name", "Running Shoes");
product1.put("priceTotal", 69.95);
product1.put("quantity", 1);
HashMap<String, Object> product2 = new HashMap<>();
product2.put("SKU", "SO100");
product2.put("name", "Running Socks");
product2.put("priceTotal", 29.99);
product2.put("quantity", 10);

// build a product list and add the product maps
List<Object> productListItems = new ArrayList<>();
productListItems.add(product1);
productListItems.add(product2);

// create an order total variable
double orderTotal = 0D;
orderTotal += (double)product1.get("priceTotal");
orderTotal += (double)product2.get("priceTotal");

// create a paymentsItem map which details the method of payment
HashMap<String, Object> paymentsItem = new HashMap<>();
paymentsItem.put("transactionID", "abc123");
paymentsItem.put("paymentAmount", orderTotal);
paymentsItem.put("paymentType", "credit_card");
paymentsItem.put("currencyCode", "USD");

// build an order, purchases, and commerce map
HashMap<String, Object> order = new HashMap<>();
order.put("purchaseID", "1234567890");
order.put("priceTotal", orderTotal);
order.put("currencyCode", "USD");
order.put("payments", paymentsItem);

HashMap<String, Object> purchases = new HashMap<>();
purchases.put("value", 1.0);

HashMap<String, Object> commerce = new HashMap<>();
commerce.put("order", order);
commerce.put("purchases", purchases);

// create an Experience Event and send it using the AEP Edge extension
HashMap<String, Object> xdmData = new HashMap<>();
xdmData.put("commerce", commerce);
xdmData.put("productListItems", productListItems);
xdmData.put("eventType", "commerce.purchases");
final ExperienceEvent experienceEvent = new ExperienceEvent.Builder().setXdmSchema(xdmData,"your-dataset-id").build();
Edge.sendEvent(experienceEvent, new EdgeCallback() {
  @Override
  public void onComplete(List<EdgeEventHandle> list) {
    // handle the response
  }
});
}
```

The alternative to using raw dictionaries for your XDM data is building a concrete class based on your XDM schema. For more information, see the Schema interface in [Edge API public classes](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge/edge-api-reference#public-classes) and the commerce example in [AEP SDK Sample App for Android](https://github.com/adobe/aepsdk-sample-app-android).

{% endtab %}

{% tab title="iOS" %}

#### Swift

#### Example

```swift
// build a product map for each product
let product1 = ["SKU":"SH100","name":"Running Shoes","priceTotal": 69.95, "quantity": 1] as [String : Any]
let product2 = ["SKU":"SO100","name":"Running Socks","priceTotal": 29.99, "quantity": 10] as [String : Any]

// build a product list and add the product maps
let productListItems: [[String : Any]] = [product1, product2]

// create an order total variable
var orderTotal = 0.0
orderTotal += product1["priceTotal"] as! Double
orderTotal += product2["priceTotal"] as! Double

// create a paymentsItem map which details the method of payment
let paymentsItem =  ["transactionID":"abc123", "paymentAmount":orderTotal,"paymentType":"credit_card","currencyCode":"USD"] as [String: Any]

// build an order, purchases, and commerce map
let order = ["purchaseID":"1234567890","priceTotal":orderTotal,"currencyCode":"USD","payments":paymentsItem] as [String : Any]

let purchases = ["value":1.0]

let commerce = ["order":order,"purchases":purchases]

// create an Experience Event and send it using the AEP Edge extension
let xdmData =  ["commerce":commerce,"productListItems":productListItems,"eventType":"commerce.purchases"] as [String : Any]
let event = ExperienceEvent(xdm: xdmData, datasetIdentifier: "your-dataset-id")
Edge.sendEvent(experienceEvent: event)
```

The alternative to using raw dictionaries for your XDM data is building a concrete class based on your XDM schema. For more information, see the XDMSchema protocol in [Edge API public classes](https://aep-sdks.gitbook.io/docs/v/AEP-Edge-Docs/using-mobile-extensions/adobe-edge/edge-api-reference#public-classes) and the commerce example in [AEP SDK Sample App for iOS](https://github.com/adobe/aepsdk-sample-app-ios/tree/main/Swift).

{% endtab %}

{% endtabs %}

## Set the products variable using the AEP Analytics extension

As _products_ variable cannot be set by processing rules, you need the syntax below in context data parameters to set serialized events directly on the hits that are sent to Analytics.

To set the products variable, set a context data key to `&&products`, and set the value by using the syntax that is defined for the products or merchandising variable. For more information, see [Implementing a Merchandising Variable](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/addproductevar.html#vars).

{% tabs %}
{% tab title="Android" %}
#### Java <a id="java-2"></a>

#### Syntax <a id="syntax"></a>

```java
cdata.put("&&products", "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]");
```

#### Example <a id="example"></a>

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
#### Objective C

#### Syntax

```objectivec
[contextData setObject:@"Category;Product;Quantity;Price[,Category;Product;Quantity;Price]" forKey:@"&&products"];
```

#### Example

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
[AEPMobileCore trackAction:@"purchase" data:contextData];
// trackState example:
[AEPMobileCore trackState:@"Order Confirmation" data:contextData];
```

#### Swift

#### Syntax

```swift
contextData["&&products"] = "Category;Product;Quantity;Price[,Category;Product;Quantity;Price]"
```

#### Example

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
MobileCore.track(action: "purchase", data: contextData)
// trackState example:
MobileCore.track(state: "Order Confirmation", data: contextData)
```
{% endtab %}

{% tab %}
The _`products`_ variable is set directly on the image request and the other variables are set as context data. All context data variables must be mapped by using processing rules except for the _`products`_ variable as it is set directly on the image request by the SDK.
{% endtab %}
{% endtabs %}

## Products variable with merchandising eVars and product-specific events <a id="products-variable-with-merchandising-evars-and-product-specific-events"></a>

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

// send the tracking call - use either a trackAction or trackState call. 
// trackAction example: 
MobileCore.trackAction("purchase", cdata); 
// trackState example: 
MobileCore.trackState("Order Confirmation", cdata);
```
{% endtab %}

{% tab title="iOS" %}
**Objective-C**

### **Example**

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
[AEPMobileCore trackAction:@"purchase" data:contextData]; 
// trackState example: 
[AEPMobileCore trackState:@"Order Confirmation" data:contextData];
```

**Swift**

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
MobileCore.track(action: "purchase", data: contextData)
// trackState example:
MobileCore.track(state: "Order Confirmation", data: contextData)
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you trigger a product-specific event by using the `&&products` variable, you must also set that event in the `&&events` variable. If you do not set that event, it is filtered out during processing.
{% endhint %}

