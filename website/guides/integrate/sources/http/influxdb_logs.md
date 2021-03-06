---
last_modified_on: "2020-07-13"
$schema: "/.meta/.schemas/guides.json"
title: "Send logs from HTTP to InfluxDB"
description: "A simple guide to send logs from HTTP to InfluxDB in just a few minutes."
author_github: https://github.com/binarylogic
cover_label: "HTTP to InfluxDB Logs Integration"
tags: ["type: tutorial","domain: sources","domain: sinks","source: http","sink: influxdb_logs"]
hide_pagination: true
---

import ConfigExample from '@site/src/components/ConfigExample';
import InstallationCommand from '@site/src/components/InstallationCommand';
import Jump from '@site/src/components/Jump';
import ServiceDiagram from '@site/src/components/ServiceDiagram';
import Steps from '@site/src/components/Steps';

Logs are an _essential_ part of observing any
service; without them you are flying blind. But collecting and analyzing them
can be a real challenge -- especially at scale. Not only do you need to solve
the basic task of collecting your logs, but you must do it
in a reliable, performant, and robust manner. Nothing is more frustrating than
having your logs pipeline fall on it's face during an
outage, or even worse, disrupt more important services!

Fear not! In this guide we'll show you how to send send logs from [HTTP][urls.http] to [InfluxDB][urls.influxdb]
and build a logs pipeline that will be the backbone of
your observability strategy.

<!--
     THIS FILE IS AUTOGENERATED!

     To make changes please edit the template located at:

     website/guides/integrate/sources/http/influxdb_logs.md.erb
-->

## Background

### What is InfluxDB Logs?

[InfluxDB][urls.influxdb] is an open-source time series database developed by InfluxData. It is written in Go and optimized for fast, high-availability storage and retrieval of time series data in fields such as operations monitoring, application metrics, Internet of Things sensor data, and real-time analytics.

## Strategy

### How This Guide Works

We'll be using [Vector][urls.vector_website] to accomplish this task. Vector
is a [popular][urls.vector_stars] [open-source][urls.vector_repo] utility for
building observability pipelines. It's written in [Rust][urls.rust], making it
lightweight, [ultra-fast][urls.vector_performance] and highly reliable. And
we'll be deploying Vector as a
[service][docs.strategies#service].

The [service deployment strategy][docs.strategies#service] treats Vector like a
separate service. It is designed to receive data from an upstream source and
fan-out to one or more destinations.
For this guide, Vector will receive data from
HTTP via Vector's
[`http` source][docs.sources.http].
The following diagram demonstrates how it works.

<ServiceDiagram
  platformName={null}
  sourceName={"http"}
  sinkName={"influxdb_logs"} />

### What We'll Accomplish

To be clear, here's everything we'll accomplish in this short guide:

<ul className="list--icons list--icons--checks list--indent">
  <li>
    Accept log data over HTTP.
    <ul>
      <li>Decode JSON, NDJSON, and text.</li>
      <li>Enrich your logs with select HTTP headers.</li>
    </ul>
  </li>
  <li>
    Send structured logs to InfluxDB v1 or v2.
    <ul>
      <li>Batch data to maximize throughput.</li>
      <li>Automatically retry failed requests, with backoff.</li>
      <li>Automatically aggregate metrics at the edge for improved performance.</li>
    </ul>
  </li>
  <li className="list--icons--arrow text--pink text--bold">All in just a few minutes!</li>
</ul>

## Tutorial

<Steps headingDepth={3}>
<ol>
<li>

### Install Vector

<InstallationCommand />

Or choose your [preferred method][docs.installation].

</li>
<li>

### Configure Vector

<ConfigExample
  format="toml"
  path={"vector.toml"}
  sourceName={"http"}
  sinkName={"influxdb_logs"} />

</li>
<li>

### Start Vector

```bash
vector --config vector.toml
```

That's it! Simple and to the point. Hit `ctrl+c` to exit.

</li>
</ol>
</Steps>

## Next Steps

Vector is _powerful_ utility and we're just scratching the surface in this
guide. Here are a few pages we recommend that demonstrate the power and
flexibility of Vector:

<Jump to="https://github.com/timberio/vector" leftIcon="github" target="_blank">
  <div className="title">Vector Github repo <span className="badge badge--primary"><i className="feather icon-star"></i> 4k</span></div>
  <div className="sub-title">Vector is free and open-source!</div>
</Jump>

<Jump to="/guides/getting-started/" leftIcon="book">
  <div className="title">Vector getting started series</div>
  <div className="sub-title">Go from zero to production in under 10 minutes!</div>
</Jump>

<Jump to="/docs/about/what-is-vector/" leftIcon="book">
  <div className="title">Vector documentation</div>
  <div className="sub-title">Thoughtful, detailed docs that respect your time.</div>
</Jump>

[docs.installation]: /docs/setup/installation/
[docs.sources.http]: /docs/reference/sources/http/
[docs.strategies#service]: /docs/setup/deployment/strategies/#service
[urls.http]: https://www.w3.org/Protocols/
[urls.influxdb]: https://www.influxdata.com/products/influxdb-overview/
[urls.rust]: https://www.rust-lang.org/
[urls.vector_performance]: https://vector.dev/#performance
[urls.vector_repo]: https://github.com/timberio/vector
[urls.vector_stars]: https://github.com/timberio/vector/stargazers
[urls.vector_website]: https://vector.dev
