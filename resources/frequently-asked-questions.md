# Frequently Asked Questions

### Launch

#### Do I need additional permissions to create a mobile property in Launch?

If you need access to Launch, see this page on [User Permissions](https://docs.adobelaunch.com/administration/user-permissions). If you have permissions to create a web property, you're all setup to create a mobile property. If you don't see the option to create a mobile property - you may refresh the page with your ad-blocker turned off.

#### Should I create one property per app or multiple properties per app platform?

If your apps send data to the same Analytics report suites, use the same extensions, rules, data elements, etc. - we recommend you group all of these mobile apps into the same property. If your apps send data to different Analytics report suites, or user different extensions per app, etc. then we suggest creating separate mobile properties. Alternatively, if you group your mobile apps into a single property, you should be able easily to split them out into separate properties over time.

#### How to delete a mobile property in Launch?

You may delete a mobile property from Launch by following these [instructions](https://docs.adobelaunch.com/administration/companies-and-properties#delete-a-property). Please note that if you choose to delete a mobile property, it may not be undone.

### Migration

#### Can I run both 4x and the new Adobe Experience Platform SDKs on my app?

Implementing both SDKs is not recommended or supported. The Experience Platform SDK migrates 4x SDK's locally stored, user context. Using both SDKs can cause severe data quality issues and user cliffing. See the [upgrade](upgrading-to-aep/) guide for more information.

