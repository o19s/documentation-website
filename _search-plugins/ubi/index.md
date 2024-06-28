---
layout: default
title: User Behavior Insights
has_children: true
nav_order: 90
redirect_from:
  - /search-plugins/ubi/
---
# Overview

**Introduced 2.15**
{: .label .label-purple }

**References UBI Specification 1.0.0**
{: .label .label-purple }

User Behavior Insights (UBI) is a plugin that captures client-side events and queries for the purposes of improving search relevance and user experience.
It is a causal system, linking a user's query to all subsequent user interactions with your application until the user performs another search.

UBI includes the following elements:
* A machine-readable [schema](https://github.com/o19s/ubi) that faciliates interoperablity of the UBI specification.
* An OpenSearch [plugin](https://github.com/opensearch-project/user-behavior-insights) that facilitates the storage of client-side events and queries.
* A client-side JavaScript [example reference implementation]({{site.url}}{{site.baseurl}}/search-plugins/ubi/data-structures/) that shows how to capture events and send those events to the OpenSearch UBI plugin.

<!-- vale off -->
The UBI documentation is organized in the following categories.

| Explanation and Reference | Description |
| :--------- | :------- |
| [UBI Request/Response Specification](https://github.com/o19s/ubi/) <br/> **References UBI Specification 1.0.0**  | Industry-standard schema for making UBI requests and responses  |
| [UBI OpenSearch Schema Documentation]({{site.url}}{{site.baseurl}}/search-plugins/ubi/schemas/) | Documentation on the individual Query and Event stores for OpenSearch |


| Tutorials and how-to guides | Description
| :--------- | :------- |
| [UBI plugin ](https://github.com/opensearch-project/user-behavior-insights) | How to install and use the UBI plugin. |
| [ JavaScript client structures ]({{site.url}}{{site.baseurl}}/search-plugins/ubi/data-structures/)  | Sample JavaScript structures for populating the event store. |
| [UBI SQL queries]({{site.url}}{{site.baseurl}}/search-plugins/ubi/sql-queries/)  | How to write analytic queries for UBI data in SQL. |
| [UBI Dashboard Tutorial]({{site.url}}{{site.baseurl}}/search-plugins/ubi/ubi-dashboard-tutorial/) | Teaches you how to build an OpenSearch dashboard with UBI data |
| [Chorus Opensearch Edition](https://github.com/o19s/chorus-opensearch-edition/?tab=readme-ov-file#structured-learning-using-chorus-opensearch-edition) katas | A series of structured tutorials that teach you how to UBI with OpenSearch using a demo Ecommerce Store. |

<!-- vale on -->
Documentation categories adapted using concepts from [Diátaxis](https://diataxis.fr/)
{: .tip }
