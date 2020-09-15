---
description: 'Last Updated September 2, 2020'
---

# Adobe Experience Cloud & Apple’s IDFA & Privacy Announcements

## What’s changed?

Apple recently announced [new changes](https://developer.apple.com/app-store/user-privacy-and-data-use/) to iOS 14, which are scheduled to take effect later in 2020/2021. Among the highlights of the changes: 

1. Apple will ask app developers to self-report data types collected and how they may be used by the brand. 
2. Beginning iOS 14, apps will need to ask & receive user’s permission to be tracked \(specifically referring to accessing the device’s advertising identifier or IDFA\). 
3. Apple is introducing a new variant of device location signal labelled “reduced” or “Approximate Location”.

{% tabs %}
{% tab title="As of Sep 15, 2020" %}
### Next Steps & Industry Reaction

Apple continues to release new details regarding these changes, and fuller business, legal, and technical impact assessments will follow accordingly. On the legal and technical sides, these changes raise questions as to how to best effectuate consumer rights and choices under laws like GDPR, CCPA, and the like. 

In terms of early reactions, the US ad trades are still evaluating and further preparing responses. [The Association of National Advertisers \(ANA\)](https://www.ana.net/content/show/id/60948) expressed concerns about the impact these changes would have on personalization, measurement and marketing communications, underscoring the importance of having a coordinated ecosystem wide solution not determined by a single company.  

IAB Europe released a [letter to Tim Cook](https://iabeurope.eu/all-news/marketing-professionals-urge-apple-to-adopt-standards-promoting-interoperability-and-more-predictable-user-privacy/) on July 2,

> Marketing professionals urge Apple to adopt standards promoting interoperability and more predictable user privacy

along with concerns about developers’ abilities to continue to meet their legal obligations under the announced guidelines.

Given that these developments are taking place against the backdrop of broader changes to addressable communications in the wider ecosystem \(e.g., browser changes\) Adobe is engaged in the appropriate policy and technical forums to work on these important issues.   

Adobe is proud to join the Partnership for Responsible Addressable Media as a founding member. We support the partnership’s principles and objectives to develop common standards, technologies, and practices for addressability. This cross-industry approach is critical to building consumer trust, powering exceptional digital experiences designed to delight consumers, and driving innovation that supports continued growth of the digital economy in a responsible and transparent way. 
{% endtab %}
{% endtabs %}

## **Potential Impact to Adobe Experience Cloud**

The changes Apple announced at WWDC 2020 concerning privacy protection may potentially impact how enterprises track, collect, and engage with their consumers. As we continue to learn more, we are not anticipating any major impact from Apple’s announcements to Adobe Analytics, Adobe Target, and Adobe Campaign. The following are some of the potential impacts on other Adobe Applications and Adobe Experience Platform. 

### Adobe Experience Platform 

Experience Platform will continue to enable customers to collect, and store data using the Mobile SDK or any other form of data ingestion. IDs that are identified to represent an opt-out event \(i.e., an IDFA changing from a unique value to all zero values\) can be used to unlink any historic IDs associated to that device. 

#### Adobe Experience Platform Mobile SDKs

We are monitoring changes associated the Apple iOS 14 beta and actively testing our SDKs for compatibility. We’ll announce and publish SDK updates as necessary. Updates will be noted in SDK release notes. Customers should contact Adobe Customer Care or their Customer Success Manager for help with specific issues and for further information. 

The Adobe SDK does not automatically collect or require sensitive user data, device location, or advertising identifiers for its standard use. Customers should resolve how to collect sensitive user data, location and advertising identifiers based on applicable mobile OS developer guidelines, including recent Apple’s changes covering the use of device identifiers, only sending to Adobe the data the customer deems appropriate. 

### Adobe Audience Manager 

Audience Manager will continue to enable customers to collect, and store data using the Mobile SDK or any other form of data ingestion. IDs that are identified to represent an opt-out event \(i.e., an IDFA changing from a unique value to all zero values\) can be used to unlink any historic IDs associated to that device. 

### Adobe Advertising Cloud 

Advertising Cloud will enable its customers to continue to deliver digital advertising campaigns on app inventory against targeted audiences provided by customers \(via standard data onboarding processes\). Customers should work with their data providers to only include user IDs they deem appropriate \(e.g. opted-in IDFAs\) in any segments that are provided to Advertising Cloud for purposes such as targeting, frequency capping, and measurement, etc. 

Please contact your Adobe Customer Success Manager or account representatives for further detail.

