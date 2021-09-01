# Mobile extension schema

Experience Data Model \(XDM\) schemas are a set of rules that define and validate the customer experience data format in Adobe Experience Platform. XDM schemas are composed of one class and zero or more field groups. For more information about XDM Schemas, see [XDM System overview](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html) and [Basics of schema composition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html). For information about creating your own schema, see the tutorial on [Create a schema using the Schema Editor](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html).

## Sample schema for mobile extension

The XDM schema for the AEP Edge extension should extend from the [XDM Experience Event](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=en#xdm-experience-event) class, which is a time-series based class and captures the state of the system when an event, or events, occurred. The following field groups should be included in the schema:

* [Application Details](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-application.schema.json) - Data that is related to the application that generates or is targeted by the event.
* [Environment Details](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-environment-details.schema.json) - Data that is related to the device, location, and surrounding environment.
* [Commerce Details](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json) - Data that is related to buying and selling lists of products.

## Commerce

The [Experience Event Commerce Details](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-commerce.schema.json) field group defines a `Commerce` object and a `ProductListItemsItem` object. The `Commerce` object lets you specify which actions are happening in a list of `ProductListItemsItem`s.

### Commerce actions

Each action object that is defined in the `Commerce` object takes a value, typically set to 1, which indicates that action occurred.

* CartAbandons - A product list has been identified as no longer accessible \(for example, purchasable\) by the user.
* Checkouts - An action during a checkout process of a product list.
* ProductListAdds - Addition of a product to the product list.
* ProductListOpens - Initializations of a new product list.
* ProductListRemovals - Removal of a product entry from a product list.
* ProductListReopens - A product list that was not accessible\(abandoned\) and has been reactivated by the user.
* ProductListViews - Views of a product-list has occurred.
* ProductViews - Views of a product have occurred.
* Purchases - An order that has been accepted.
* SaveForLaters - Product list that is saved for future use.

Here is a sample of creating a `Commerce` object with the `ProductListAdds` action:

{% tabs %}
{% tab title="Android" %}
```java
Commerce commerce = new Commerce();
ProductListAdds productListAdds = new ProductListAdds();
productListAdds.setValue(1);
commerce.setProductListAdds(productListAdds);
```
{% endtab %}
{% endtabs %}

### Commerce order

The `Commerce` object also contains details about a purchase through the `Order` object. The `Order` object is typically included with a `Purchases` action and includes details for purchase ID and order number, total price, currency, and a list of payment items.

Here is a sample of creating a `Commerce` object with an `Order`:

{% tabs %}
{% tab title="Android" %}
```java
// Create PaymentItem which details the method of payment
PaymentsItem paymentsItem = new PaymentsItem();
paymentsItem.setCurrencyCode("USD");
paymentsItem.setPaymentAmount(25.99);
paymentsItem.setPaymentType("credit_card");

List<PaymentsItem> paymentsItemList = new ArrayList<>();
paymentsItemList.add(paymentsItem);

// create the Order
Order order = new Order();
order.setCurrencyCode("USD");
order.setPriceTotal(25.99);
order.setPayments(paymentsItemList);

// create Commerce and add Purchases action and Order details
Commerce commerce = new Commerce();
Purchases purchases = new Purchases();
purchases.setValue(1);
commerce.setPurchases(purchases);
commerce.setOrder(order);
```
{% endtab %}

{% tab title="iOS" %}
```swift
// Create PaymentItem which details the method of payment

var paymentsItem = PaymentsItem()
paymentsItem.currencyCode = "USD"
paymentsItem.paymentAmount = 25.99
paymentsItem.paymentType = "credit_card"

// create the Order
var order = Order()
order.currencyCode = "USD"
order.priceTotal = 25.99
order.payments = [paymentsItem]

// create Commerce and add Purchases action and Order details
var commerce = Commerce()
var purchases = Purchases()
purchases.value  = 1
commerce.order = order
commerce.purchases = purchases
```
{% endtab %}
{% endtabs %}

### Product list items

The `ProductListItemsItem` object includes details for a product that was selected by the user. The following `ProductListItemsItem` objects can be used to identity the products with which the user has interacted.

* SKU - Unique identifier for a product that was defined by the vendor. 
* currencyCode - The ISO 4217 alphabetic currency code used to price the product.
* name - The display name for the product as presented to the user for this product view.
* priceTotal - The total price for the product line item.
* product - The XDM identifier of the product.
* productAddMethod - The method that was used to add a product item to the list by the visitor.
* quantity - The number of units of the product that the customer has indicated they require.

## Examples

#### Product Add event

{% tabs %}
{% tab title="Android" %}
```java
ProductListItemsItem productItem = new ProductListItemsItem();
productItem.setName("red ball");
productItem.setSKU("625-740");
productItem.setCurrencyCode("USD");
productItem.setQuantity(1);
productItem.setPriceTotal(9.95);
productItem.setProductAddMethod("add to cart button");

List<ProductListItemsItem> itemsList = new ArrayList<>();
itemsList.add(productItem);

Commerce commerce = new Commerce();
ProductListAdds productListAdds = new ProductListAdds();
productListAdds.setValue(1);
commerce.setProductListAdds(productListAdds);

MobileSDKPlatformEventSchema xdmData = new MobileSDKPlatformEventSchema();
xdmData.setEventType("commerce.productListAdds");
xdmData.setCommerce(commerce);
xdmData.setProductListItems(itemsList);
```
{% endtab %}

{% tab title="iOS" %}
```swift
var productItem = ProductListItemsItem()
productItem.name = "red ball"
productItem.SKU  = "625-740"
productItem.currencyCode = "USD"
productItem.quantity     = 1
productItem.priceTotal   = 9.95

var itemsList: [ProductListItemsItem]
itemsList.append(productItem)  

var commerce = Commerce()
var productViews = ProductViews()
productViews.value = 1
commerce.productViews = productViews

var xdmData = MobileSDKPlatformEventSchema()
xdmData.eventType = "commerce.productListAdds"
xdmData.commerce = commerce
xdmData.productListItems = itemsList
```
{% endtab %}
{% endtabs %}

#### Purchase event

{% tabs %}
{% tab title="Android" %}
```java
// Create product item list with two products
ProductListItemsItem productItem1 = new ProductListItemsItem();
productItem1.setName("red ball");
productItem1.setSKU("625-740");
productItem1.setCurrencyCode("USD");
productItem1.setQuantity(1);
productItem1.setPriceTotal(9.95);

ProductListItemsItem productItem2 = new ProductListItemsItem();
productItem2.setName("blue car");
productItem2.setSKU("450-495");
productItem2.setCurrencyCode("USD");
productItem2.setQuantity(1);
productItem2.setPriceTotal(12.98);

List<ProductListItemsItem> itemsList = new ArrayList<>();
itemsList.add(productItem1);
itemsList.add(productItem2);

// Create PaymentItem which details the method of payment
PaymentsItem paymentsItem = new PaymentsItem();
paymentsItem.setCurrencyCode("USD");
paymentsItem.setPaymentAmount(22.93);
paymentsItem.setPaymentType("credit_card");

List<PaymentsItem> paymentsItemList = new ArrayList<>();
paymentsItemList.add(paymentsItem);

// Create the Order
Order order = new Order();
order.setCurrencyCode("USD");
order.setPriceTotal(22.93);
order.setPayments(paymentsItemList);

// Create Commerce and add Purchases action and Order details
Commerce commerce = new Commerce();
Purchases purchases = new Purchases();
purchases.setValue(1);
commerce.setPurchases(purchases);
commerce.setOrder(order);

// Create Platform Event
MobileSDKPlatformEventSchema xdmData = new MobileSDKPlatformEventSchema();
xdmData.setEventType("commerce.purchases");
xdmData.setCommerce(commerce);
xdmData.setProductListItems(itemsList);
```
{% endtab %}

{% tab title="iOS" %}
```swift
// Create product item list with two products

var productItem1 = ProductListItemsItem()
productItem1.name = "red ball"
productItem1.SKU  = "625-740"
productItem1.currencyCode = "USD"
productItem1.quantity     = 1
productItem1.priceTotal   = 9.95

var productItem2 = ProductListItemsItem()
productItem2.name = "blue car"
productItem2.SKU  = "450-495"
productItem2.currencyCode = "USD"
productItem2.quantity     = 1
productItem2.priceTotal   = 12.98

var itemsList: [ProductListItemsItem]
itemsList.append(productItem1)  
itemsList.append(productItem2)  

var paymentsItem = PaymentsItem()
paymentsItem.currencyCode = "USD"
paymentsItem.paymentAmount = 22.93
paymentsItem.paymentType = "credit_card"

// create the Order
var order = Order()
order.currencyCode = "USD"
order.priceTotal = 22.93
order.payments = [paymentsItem]

// create Commerce and add Purchases action and Order details
var commerce = Commerce()
var purchases = Purchases()
purchases.value  = 1
commerce.order = order
commerce.purchases = purchases    

var xdmData = MobileSDKPlatformEventSchema()
xdmData.eventType = "commerce.purchases"
xdmData.commerce = commerce
xdmData.productListItems = itemsList
```
{% endtab %}
{% endtabs %}

