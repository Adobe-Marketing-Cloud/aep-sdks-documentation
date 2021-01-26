# Products variable

## Set the products variable using XDM events and the Edge extension

Experience Data Model (XDM) schemas can be used to send the products variable to Analytics. XDM schemas are composed of one class and zero or more mixins. For more information on creating an XDM schema, see [Basics of schema composition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#understanding-schemas) and [Create a schema using the Schema Editor](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html#tutorials). An Edge event containing a mixin for a [commerce detail object](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) can be used for sending product information to Analytics.

{% tabs %}
{% tab title="Android" %}

#### Java <a id="java-2"></a>

Create an Experience Edge event containing purchased product data and send it to Experience Edge. The following code sample is a modified version of the product purchase example within the [AEP SDK Sample App for Android](https://github.com/adobe/aepsdk-sample-app-android).

#### Example <a id="example"></a>

```java
// Create the purchased item objects
final ProductListItemsItem product1 = new ProductListItemsItem();
product1.setName("Running Shoes");
product1.setPriceTotal(69.95);
product1.setQuantity(1);

final ProductListItemsItem product2 = new ProductListItemsItem();
product2.setName("Running Socks");
product2.setPriceTotal(29.99);
product2.setQuantity(10);

// Create a list of purchased items
List<ProductListItemsItem> purchasedItems = new ArrayList<ProductListItemsItem>() {{
  add(product1);
  add(product2);
}};

// Create Purchases action
Purchases purchases = new Purchases();
purchases.setValue(1);
purchases.setId("1234567890");

// Create Commerce object and add Purchases action
Commerce commerce = new Commerce();
commerce.setPurchases(purchases);

// Compose the XDM Schema object and set the event name
MobileSDKCommerceSchema xdmData = new MobileSDKCommerceSchema();
xdmData.setEventType("commerce.purchases");
xdmData.setCommerce(commerce);
xdmData.setProductListItems(purchasedItems);

// Create an Experience Event with the built schema and send it using the AEP Edge extension
ExperienceEvent event = new ExperienceEvent.Builder()
  .setXdmSchema(xdmData)
  .build();
Edge.sendEvent(event, new EdgeCallback() {
  @Override
  public void onComplete(List<EdgeEventHandle> list) {
    // handle the response
  }
});
}
```

{% endtab %}

{% tab title="iOS" %}

Create an Experience Edge event containing purchased product data and send it to Experience Edge. The following code sample is a modified version of the product purchase example within the [AEP SDK Sample App for iOS](https://github.com/adobe/aepsdk-sample-app-ios/tree/main/Swift).

#### Swift

#### Example

```swift
// Create the purchased item objects
var product1 = ProductListItemsItem()
product1.name = "Running Shoes"
product1.priceTotal = 69.95
product1.quantity = 1
        
var product2 = ProductListItemsItem()
product2.name = "Running Socks"
product2.priceTotal = 29.99
product2.quantity = 10
                
// Create a list of purchased items
let purchasedItems: [ProductListItemsItem] = [product1, product2]

// Create Purchases action
var purchases = Purchases()
purchases.value = 1
purchases.id = "1234567890"

// Create Commerce object and add Purchases action
var commerce = Commerce()
commerce.purchases = purchases
                
// Compose the XDM Schema object and set the event name
var xdmData = MobileSDKCommerceSchema()
xdmData.eventType = "commerce.purchases"
xdmData.commerce = commerce
xdmData.productListItems = purchasedItems

// Create an Experience Event with the built schema and send it using the Platform extension
let event = ExperienceEvent(xdm: xdmData)
Edge.sendEvent(experienceEvent: event)
```

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

