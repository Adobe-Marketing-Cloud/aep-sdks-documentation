# Product variable

## Products variable <a id="products-variable"></a>

The products variable cannot be set by using processing rules. In the iOS 4.x SDK, you must use a special syntax in the context data parameter to set products directly on the server call.

To set the _`products`_ variable, set a context data key to `"&&products"`, and set the value by using the syntax that is defined for the _`products`_ variable:

```text
[contextData setObject:@"Category;Product;Quantity;Price[,Category;Product;Quantity;Price]" forKey:@"&&products"];
```

For example:

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

_`products`_ is set directly on the image request, and the other variables are set as context data. All context data variables must be mapped by using processing rules:

### \[Image Here\]

You do not need to map the _`products`_ variable using processing rules because it is set directly on the image request by the SDK.

## Products variable with merchandising eVars and product-specific events <a id="products-variable-with-merchandising-evars-and-product-specific-events"></a>

Here is an example of the products variable with Merchandising eVars and product-specific events.

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

> \[!TIP\]
>
> If you trigger a product-specific event by using the _`&&products`_ variable, you must also set that event in the _`&&events`_ variable. If you do not set that event, it is filtered out during processing.

