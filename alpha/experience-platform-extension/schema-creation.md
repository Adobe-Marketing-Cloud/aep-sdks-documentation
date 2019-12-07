# XDM Schema

Experience Data Model (XDM) schemas are a set a rules which defines and validates the format of customer experience data in Adobe Data Platform. XDM schemas are composed of a single class and zero or more mixins. For more information on XDM Schemas, read the [XDM System overview](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/xdm_system/xdm_system_in_experience_platform.md) and [basics of schema composition](https://www.adobe.io/apis/experienceplatform/home/xdm/xdmservices.html#!api-specification/markdown/narrative/technical_overview/schema_registry/schema_composition/schema_composition.md). For information on creating your own Schema, see the tutorials on creating a schema [using the user interface](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/schema_editor_tutorial/schema_editor_tutorial.md).

## Sample schema for mobile extension

For Alpha customers of the Adobe Experience Platform mobile extension, a sample XDM schema is already created for your use. The schema defines a basic set of things you want to send to Adobe Data Platform if you have products in your application. 

The sample XDM schema for the Experience Platform mobile extension extends from the [XDM ExperienceEvent]() class, which is a time-series based class and captures the state of the system when an event, or events, occurred. Three mixins are also included in the schema: 

- [ExperienceEvent Application Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-application.schema.md) - data related to the application generating or targeted by the event
- [ExperienceEvent Environment Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-environment-details.schema.md) - data related to the device, location, and surrounding situation
- [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) - data related to buying and selling lists of products.

## Commerce

For the most part, you only need to be concerned with the ExperienceEvent Commerce Details mixin, as the Experience Platform mobile extension automatically collects application and environment details for each experience event.

The [ExperienceEvent Commerce Details](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) mixin defines a `Commerce` object and a `ProductListItemsItem` object. The `Commerce` object lets you specify which actions are happening on a list of `ProductListItemsItem`s. 

### Commerce actions

Each action object defined in the `Commerce` object takes a value, typically set to 1, which indicates that action occurred.

- CartAbandons - A product list has been identified as no longer accessible (e.g purchasable) by the user.
- Checkouts - An action during a checkout process of a product list.
- ProductListAdds - Addition of a product to the product list.
- ProductListOpens - Initializations of a new product list.
- ProductListRemovals - Removal(s) of a product entry from a product list.
- ProductListReopens - A product list that was no longer accessible(abandoned) has been re-activated by the user.
- ProductListViews - View(s) of a product-list has occurred.
- ProductViews - View(s) of a product have occurred.
- Purchases - An order has been accepted.
- SaveForLaters - Product list is saved for future use.

Here is a sample of creating a `Commerce` object with the `ProductListAdds` action.

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

Here is a sample of creating a `Commerce` object with an `Order`.

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

{% endtabs %}

### Product list items

The `ProductListItemsItem` object includes details for a product selected by the customer. A list of  `ProductListItemsItem` objects can be used to identity the products the customer has interacted with.

- SKU - Unique identifier for a product defined by the vendor. 
- currencyCode - The ISO 4217 alphabetic currency code used for pricing the product.
- name - The display name for the product as presented to the user for this product view.
- priceTotal - The total price for the product line item.
- product - The XDM identifier of the product itself.
- productAddMethod - The method that was used to add a product item to the list by the visitor.
- quantity - The number of units the customer has indicated they require of the product.

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

{% endtabs %}