---
layout: default
title: User behavior insights
<<<<<<< HEAD
has_children: true
nav_order: 90
redirect_from:
  - /search-plugins/ubi/
---
# Overview

**Introduced 2.15**
{: .label .label-purple }

**References UBI Draft Specification X.Y.Z**
{: .label .label-purple }

User Behavior Insights, or UBI, is a community plugin for capturing client-side events and queries for the purposes of improving search relevance and user experience.
It is a causal system, linking a user's query to all subsequent user interactions with your application until they perform another search.


* An machine readable [schema](https://github.com/o19s/ubi) that faciliates interoperablity of the UBI specification.
* An OpenSearch [plugin](https://github.com/o19s/opensearch-ubi) that facilitates the storage of client-side events and queries.
* A client-side JavaScript [ example ]({{site.url}}{{site.baseurl}}/search-plugins/ubi/data-structures/) reference implementation that shows how to capture events and send those events to the OpenSearch UBI plugin.

<!-- vale off -->

| Explanation & Reference | Description
| :--------- | :------- |
| [UBI Request/Response Specification](https://github.com/o19s/ubi/) <br/> **References UBI Draft Specification X.Y.Z**  | Schema standard for making UBI requests and responses  |
| [UBI OpenSearch Schema Documentation]({{site.url}}{{site.baseurl}}/search-plugins/ubi/schemas/) | Documentation on the individual Query and Event stores for OpenSearch |
| `query_id` Data Flow <!-- ({{site.url}}{{site.baseurl}}/search-plugins/ubi/query_id/) --> | To remove? |


| Tutorials & How-to Guides | Description
| :--------- | :------- |
| [UBI Plugin Admin]({{site.url}}{{site.baseurl}}/search-plugins/ubi/documentation/) | How to install and use the UBI Plugin |
| [ JavaScript client structures ]({{site.url}}{{site.baseurl}}/search-plugins/ubi/data-structures/)  | Sample JavaScript structures for populating the Event store |
| [UBI SQL queries ]({{site.url}}{{site.baseurl}}/search-plugins/ubi/sql-queries/)  | How to write analytic queries for UBI data in SQL |
| [UBI Dashboard Tutorial]({{site.url}}{{site.baseurl}}/search-plugins/ubi/ubi-dashboard-tutorial/) | Teaches you how to build an OpenSearch dashboard with UBI data |
| ... | teaches how to do something |

<!-- vale on -->
Documentation adapted using concepts from [Diátaxis](https://diataxis.fr/)
{: .tip }

=======
parent: Search relevance
has_children: false
nav_order: 220
---

# User behavior insights

User Behavior Insights, or UBI, is a community plugin for capturing client-side events and queries for the purposes of improving search relevance and user experience. UBI consists of three components:

* An OpenSearch [plugin](https://github.com/o19s/opensearch-ubi) that facilitates the storage of client-side events and queries.
* A client-side JavaScript library reference implementation that shows how to capture events and send those events to the OpenSearch UBI plugin.
* An OpenSearch Dashboards plugin that provides access to the collected events and queries for analysis. This component is still largely in the design phase.

UBI is currently only supported in OpenSearch 2.12.0.
{: .warning }

## Installing the plugin

The User Behavior Insights plugin is available for OpenSearch 2.12.0. To install the plugin, run the following command:

```bash
./bin/opensearch-plugin install \
   "https://github.com/o19s/opensearch-ubi/releases/download/0.0.8/opensearch-ubi-0.0.8-os2.12.0.zip"
```
{% include copy.html %}

For plugin APIs and examples, see [OpenSearch User Behavior Insights documentation](https://github.com/o19s/opensearch-ubi/blob/main/documentation.md).

The following steps outline how to get started with the UBI plugin.

## Initializing a UBI store

A _store_ contains the client-side events and the queries. After installing the plugin we need to initialize a store. In the following request we are creating a store called `mystore`.

```json
PUT _plugins/ubi/mystore
```
{% include copy.html %}

A store consists of two OpenSearch indexes whose names are based on the name of the store being created. For the `mystore` store, the names of the indexes are:

* `.mystore_events` - This index contains the client-side events sent to the plugin by the JavaScript library.
* `.mystore_queries` - This index contains the queries that the plugin passively stores.

## Sending events to the store

With the store initialized, you can now send client-side events to our `mystore` store:

```json
POST /_plugins/ubi/mystore
{
  "type": "instant-search",
  "keywords": "laptop",
  "url": "my_url.html",
  "lang": "en-US",
  "session": "npckcy4",
  "channel": "demo-channel"
}
```
{% include copy-curl.html %}

## Capturing queries

The UBI plugin passively stores queries. To test it, you can run a query against an example index of products called `ecommerce`:

```bash
GET /ecommerce/_search -H "X-ubi-store: mystore"
```
{% include copy.html %}

Note that this request includes a header called `X-ubi-store`. This header allows the UBI plugin to associate this query with a UBI store.
>>>>>>> 7ae1d111 (gathering potential documentation attempts)
