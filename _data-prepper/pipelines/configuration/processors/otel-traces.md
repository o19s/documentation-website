---
layout: default
title: otel_traces 
parent: Processors
grand_parent: Pipelines
nav_order: 75
---

# otel_trace

The `otel_trace` processor completes trace-group-related fields in all incoming OpenSearch Data Prepper span records by state caching the root span information for each `traceId`. 

## Parameters

This processor includes the following parameters.

* `traceGroup`: Root span name
* `endTime`: End time of the entire trace in International Organization for Standardization (ISO) 8601 format
* `durationInNanos`: Duration of the entire trace in nanoseconds
* `statusCode`: Status code for the entire trace in nanoseconds

## Configuration

The following table describes the options you can use to configure the `otel_trace` processor.

<!--
This table is autogenerated. Do not edit it.
- name: otel_traces
- pluginType: processor
- source: https://github.com/opensearch-project/data-prepper/blob/c4455a7785bc2da4358067c217be7085e0bc8d0f/data-prepper-plugins/otel-trace-raw-processor/src/main/java/org/opensearch/dataprepper/plugins/processor/oteltrace/OtelTraceRawProcessorConfig.java
-->

Option | Required | Type | Description
:--- | :--- | :--- | :---
trace_flush_interval | No | Integer | Represents the time interval in seconds to flush all the descendant spans without any root span. Default is 180.


## Metrics

The following table describes common [Abstract processor](https://github.com/opensearch-project/data-prepper/blob/main/data-prepper-api/src/main/java/org/opensearch/dataprepper/model/processor/AbstractProcessor.java) metrics.

| Metric name | Type | Description |
| ------------- | ---- | -----------|
| `recordsIn` | Counter | Metric representing the ingress of records to a pipeline component. |
| `recordsOut` | Counter | Metric representing the egress of records from a pipeline component. |
| `timeElapsed` | Timer | Metric representing the time elapsed during execution of a pipeline component. |

The `otel_trace` processor includes the following custom metrics:

* `traceGroupCacheCount`: The number of trace groups in the trace group cache.
* `spanSetCount`: The number of span sets in the span set collection.
