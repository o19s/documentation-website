---
layout: default
title: How does the plugin fit in?
nav_order: 20
parent: LTR search
has_children: false
---

# How does the plugin fit in

In [core concepts]({{site.url}}{{site.baseurl}}/search-plugins/ltr/core-concepts/) we mentioned a couple
of activities you undertake when implementing learning to rank:

1.  Judgement List Development
2.  Feature Engineering
3.  Logging features into the Judgement list to create a training set
4.  Training and testing models
5.  Deploying and using models when searching

How does OpenSearch LTR fit into this process?

## What the plugin does

This plugin gives you building blocks to develop and use learning to
rank models. It lets you develop query-dependent features and store them
in OpenSearch. After storing a set of features, you can log them for
documents returned in search results to aid in offline model
development.

Then other tools take over. With a logged set of features for documents,
you join data with your Judgement lists you've developed on your own.
You've now got a training set you can use to test/train ranking models.
Using of a tool like Ranklib or XGBoost, you'll hopefully arrive at a
satisfactory model.

With a ranking model, you turn back to the plugin. You upload the model
and give it a name. The model is associated with the set of features
used to generate the training data. You can then search with the model,
using a custom OpenSearch Query DSL primitive that executes the
model. Hopefully this lets you deliver better search to users.

## What the plugin is NOT

The plugin does not help with Judgement list creation. This is work you
must do and can be very domain specific. The Wikimedia Foundation wrote a
[great
article](https://blog.wikimedia.org/2017/09/19/search-relevance-survey/)
on how they arrive at Judgement lists for people searching articles.
Other domains such as e-commerce might be more conversion focused. Yet
others might involve human relevance judges \-- either experts at your
company or mechanical turk.

The plugin does not train or test models. This also happens offline in
tools appropriate to the task. Instead the plugin uses models generated
by XGboost and Ranklib libraries. Training and testing models is CPU
intensive task that, involving data scientist supervision and offline
testing. Most organizations want some data science supervision on model
development. And you would not want this running in your production
Elasticsearch cluster!

The rest of this guide is dedicated to walking you through how the
plugin works to get you there. Continue on to
`building-features`{.interpreted-text role="doc"}.