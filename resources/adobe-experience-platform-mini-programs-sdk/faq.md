# WeChat Mini-program SDK Implementation FAQ

## Frequently asked questions

### I have setup all the necessary configurations, why I couldn’t see the data coming into my WeChat report?
You can do self-check with following steps first. If you couldn’t find the problem by yourself, please contact our client care.
-	Use debug tool within WeChat Devtools or Charles to check if your WeChat Mini-program successfully sending requests to Adobe with right configurations (including tracking server, report suite), and right parameters (including the context variables or s parameters your intend pass to Adobe Analytics). 
-	Assure the configuration of “analytics.offlineEnabled” in your mini-program is aligned with the setting of Timestamp Configuration in your report suite. You can find Timestamp at  Analytics > Admin > Report Suites > General > Timestamp Configuration.
E.g. 
“analytics.offlineEnabled = ture” ties to Timestamps required or optional
“analytics.offlineEnabled = false” ties to Timestamps not allowed or optional
       

### Tencent requires ICP on all the domains requested from Mini program. If we are using a subdomain of *sc.adobedc.cn, is this covered by Adobe or do we need to apply for an ICP separately?
Adobe applied ICP for *.adobedc.cn. You don’t need to apply an ICP for subdomain of *.adobedc.cn.


### Can I use Adobe Launch to deploy this SDK?
We currently don’t support deploy WeChat SDK though Adobe Launch. But it's in our future development plan.


### How to set the products variables in WeChat SDK? 
Similar to mobile SDK, products variable cannot be set by using processing rules. To set the products variable, set a context data key to “&&products”, and set the value by using the syntax that is defined for the products variable:
“&&products”: “Category;Product;Quantity;Price[,Category;Product;Quantity;Price]”
```javascript
AdobeSDK.trackAction('AddToCart',
{"&&events":"scAdd",
 "&&products": ";running shoes;1;69.95,;running socks;10;29.99"})
```


### When sending data from mini-program to Adobe Analytics, should I use context variable and processing rule? Can I send eVars and events directly to Adobe Analytics? 
Although it is supported to send eVars, events directly to Analytics with WeChat SDK, we recommend sending data in context variable and using processing rules to manage them.


### Does Adobe WeChat SDK support tracking the hybrid mini-program? (hybrid means embedding html page in the native WeChat mini-program)
Yes. As long as the Adobe tracking server is configured in Server Domain Name, you should be able to track hybrid WMP with Adobe WeChat SDK.


### When use Adobe WeChat SDK tracking hybrid mini-program, will it be able to tell an unique visitor if a visitor visits both native and embedded web page during a session?
This is a use case which will be support when we support ECID in WeChat SDK in the future. Right now, it’s only able to be resolved by customized solution. Please contact our client care for detailed solution. 


### Can I use mobile service to implement WeChat SDK?
Yes. 
