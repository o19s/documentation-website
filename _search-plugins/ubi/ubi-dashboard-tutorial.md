---
layout: default
title: UBI Dashboard Tutorial
parent: User Behavior Insights
has_children: false
nav_order: 7
---


# UBI dashboard tutorial

Whether you've been collecting user events and queries for a while, or [you've uploaded some sample events](https://github.com/o19s/chorus-OpenSearch-edition/blob/main/katas/003_import_preexisting_event_data.md), you're now ready to visualize the data collected through UBI in a dashboard in OpenSearch.

To quickly view a dashboard without following the tutorial, follow these steps:
1. Download and save the [sample UBI dashboard]({{site.url}}{{site.baseurl}}/assets/examples/ubi-dashboard.ndjson).
1. On the top menu, go to **Management > Dashboard Management**.
1. From the **Dashboards** panel, choose **Saved objects**.
1. In the upper right corner, select **Import**.
1. In the **Select file** panel, choose **Import**.
1. Select the UBI dashboard file that you downloaded and select the **Import** button.

## 1. Start OpenSearch Dashboards

Depending on your configuration: `http://{server}:5601/app/home#/`
![Dashboard Home]({{site.url}}{{site.baseurl}}/images/ubi/home.png "Dashboards")
{: .note} 

## 2. Create an index pattern

Within OpenSearch Management, navigate to **Dashboards Management > Index patterns**.

`http://{server}:5601/app/management/OpenSearch-dashboards/indexPatterns`

It will look something like the following.

OpenSearch Dashboards access your indexes using index patterns. To visualize your users' online search behavior, you must create an index pattern in order to access the indexes that UBI creates. For more information, see [Index patterns]({{site.url}}{{site.baseurl}}/dashboards/management/index-patterns/).

After you select **Create index pattern**, a list of indexes in your OpenSearch instance is displayed. The UBI stores may be hidden by default, so make sure to select **Include system and hidden indexes**, as shown in the following image. 
![Index Patterns]({{site.url}}{{site.baseurl}}/images/ubi/index_pattern2.png "Index Patterns")

You can group indexes into the same data source for your dashboard using wildcards. For this tutorial we'll combine the query and event stores into the `ubi_*` pattern.

OpenSearch Dashboards prompts you to filter on any `date` field in your schema, so that you can look at things like trending queries over the last 15 minutes. However, for your first dashboard, select **I don't want to use the time filter**, as shown in the following image. 
<img src="{{site.url}}{{site.baseurl}}/images/ubi/index_pattern3.png" alt="Index Patterns" width="400"/>


After selecting **Create index pattern, you're ready to start building a dashboard that displays the UBI store data.

## 3. Create a new dashboard

To create a new dashboard, on the top menu select **OpenSearch Dashboards > Dashboards**, then **Create > Dashboard** > **Create new**.
If you haven't previously created a dashboard, you should see something like the following:
![First Dashboard]({{site.url}}{{site.baseurl}}/images/ubi/first_dashboard.png "First Dashboard")

Otherwise, you will see previously created dashboards here.
{: .note} 

In the **New Visualization** window, select **Pie** to create a new pie chart. Then select the index pattern you created in Step 2.

Most visualizations require some sort of aggregate function on an bucket/facet/aggregatable field (numeric or keyword). You'll add a `Terms` aggregation on the `action_name` field so that you can view the distribution of event names. Change the **Size** to the number of slices you want to display, as shown in the following image.
![Pie Chart]({{site.url}}{{site.baseurl}}/images/ubi/pie.png "Pie Chart")

Save that visualization so it is added to your new dashboard. Now that you have a visualization on your dashboard, you can save your dashboard.

## 4. Add a tag cloud visualization

Now you'll add a word cloud for trending searches by creating a new visualization, similar to the previous step.  In the **New Visualization** window, select **Tag Cloud**. Then select the index pattern you created in Step 2. Choose the Tag Cloud visualization of the terms in the `message` field where the JavaScript client logs the raw text that the user searches on.  (Note: The true query, as processed by OpenSearch with filters, boosting, and so on, resides in the `ubi_queries` index. However, you'll view the `message` field of the `ubi_events` index, where the Javascript client captures the text that the user actually typed.) The following image shows the tag cloud visualization on the `message` field.
![Word Cloud]({{site.url}}{{site.baseurl}}/images/ubi/tag_cloud1.png "Word Cloud")

The underlying queries can be found under [SQL trending queries]({{site.url}}{{site.baseurl}}/search-plugins/ubi/sql-queries/#trending-queries).
{: .note} 


However, this visualization is not exactly what you're looking for. The `message` field is updated on every event---not only query/search events---and can be used in any way the client developer decides to use it. As a result, it can contain error messages, debug messages, click information, and other data.
To view only search terms on query events, you need to add a filter to your visualization. Since the developer provided a `message_type` of `QUERY` for each search event, you can filter on that message type to isolate the specific users' searches. To do this, select **Add filter** and then select **QUERY** in the **Edit filter** panel, as shown in the following image. 
![Word Cloud]({{site.url}}{{site.baseurl}}/images/ubi/tag_cloud2.png "Word Cloud")

You should now have two visualizations (the pie chart and the tag cloud) on your dashboard, as shown in the following image.
![UBI Dashboard]({{site.url}}{{site.baseurl}}/images/ubi/dashboard2.png "UBI Dashboard")

## 5. Add a histogram of item clicks

Now you'll add a histogram visualization to your dashboard, similar to the previous step. In the **New Visualization** window, select **Vertical Bar**. Then select the index pattern you created in Step 2. 

The data field you want to examine is `event_attributes.position.ordinal`. This field contains the position of the item in a list that the user selected. For the histogram visualization, the x-axis will be the ordinal number of the selected item (n). The y-axis will be the number of times that the nth item was clicked, as shown in the following image. 

![Vertical Bar Chart]({{site.url}}{{site.baseurl}}/images/ubi/histogram.png "Vertical Bar Chart")

## 6) Have fun slicing and dicing

Now you can further filter the displayed data. For example, let's see how the click position changes when there is a purchase. Select **Add filter** and then select the `action_name:product_purchase` field, as shown in the following image.
![Product Purchase]({{site.url}}{{site.baseurl}}/images/ubi/product_purchase.png "Product Purchase")


You can filter event messages containing the word `*laptop*` by adding wildcards, as shown in the following image.
![Laptop]({{site.url}}{{site.baseurl}}/images/ubi/laptop.png "Laptop").
 

