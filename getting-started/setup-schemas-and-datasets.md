# Setup schemas & datasets

To standardize data collection for use across applications that leverage Adobe Experience Platform, Adobe has created the open and publicly documented Experience Data Model standard, or, in short: [XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html).

XDM provides a foundational framework to allow [Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/home.html) services and Adobe Experience Cloud solutions to interoperate for reliable marketing and experience delivery use cases.

{% hint style="info" %}
To learn more about XDM, see [XDM System Overview](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html)​
{% endhint %}

To leverage data collection via the Experience Platform Edge Network, data has to be sent in as XDM objects. The use of non-XDM objects is currently unsupported.

In order to begin sending XDM data from your mobile application to Edge Network, you'll need to do the following:

1. [Create & configure your XDM schema\(s\)](setup-schemas-and-datasets.md#create-and-configure-your-xdm-schema)
2. [Create & configure Dataset based on the previously created schema\(s\)](setup-schemas-and-datasets.md#create-and-configure-a-dataset)

## Create & configure your XDM schema <a id="create-and-configure-your-xdm-schema"></a>

### What is an XDM schema?

Schemas are a formalized description of the structure of your data. Schemas provide a standardized way of describing data in Experience Platform. This allows for all data that conforms to schemas to be reused across an organization without conflicts, or even shared between multiple organizations.

Edge Network and Adobe Experience Platform require your incoming data to have a defined schema that describes your data’s structure and provide constraints to the type of data that can be contained within each field.

{% hint style="info" %}
To learn more about creating your own XDM schema, industry specific recommendations, or best-practices — see [Basics of schema composition](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html).
{% endhint %}

### Creating a sample schema

The following steps illustrate the creation of a sample schema for mobile data collection, follow the steps below to get started:

1. In the browser, navigate to [Adobe Experience Platform](https://experience.adobe.com/platform) and login with your credentials.
2. Create an XDM Schema as follows:
   1. From the left panel, select Schemas
   2. Click **Create schema**
   3. Select **XDM Experience event**
   4. Under **Mixins**, select **Add**; search and add the `Environment Details`,`Application Details`, and other pre-created or custom _mixins_ as needed.
   5. Set a **Display Name** for this schema and click `Save`.

![Schema Creation in Adobe Experience Platform](https://gblobscdn.gitbook.com/assets%2F-Lf1Mc1caFdNCK_mBwhe%2Fsync%2Ffe309e8b2ebd1c7573cf23ccdab56f406b4aa822.png?alt=media)

## Create & configure a dataset <a id="create-and-configure-a-dataset"></a>

Data ingested into Adobe Experience Platform is stored \(in the Data Lake\) as datasets that conform to the aforementioned mentioned XDM schema\(s\) \(setup in the step above\).

{% hint style="info" %}
To learn more about datasets in Adobe Experience Platform, visit [Datasets overview](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html).
{% endhint %}

The following steps illustrate the creation of a sample dataset for mobile data collection, follow the steps below to get started:

1. In the browser, navigate to [Adobe Experience Platform](https://experience.adobe.com/platform) and login with your credentials.
2. Create a new Dataset as follows:
   1. From the left navigation panel, under **Data Management**, select **Datasets**
   2. Click **Create dataset from schema**
   3. Select the XDM schema previously created and click **Next**.
   4. Set a name for this Dataset and click **Finish**.

![Dataset Creation in Adobe Experience Platform](https://gblobscdn.gitbook.com/assets%2F-Lf1Mc1caFdNCK_mBwhe%2Fsync%2Feb712f9b357538dfc425d5af67a0663d044d6087.png?alt=media)

