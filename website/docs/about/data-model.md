---
title: Data Model
sidebar_label: hidden
description: A deep dive into Vector's data model
---

import SVG from 'react-inlinesvg';

<SVG src="/img/data-model-event.svg" />

## Event

All data flowing through Vector are considered an "events". Events 
must be classified as a [`log`](#log) or [`metric`](#metric) event:

import Jump from '@site/src/components/Jump';

<Jump to="/docs/about/data-model/log">Log</Jump>
<Jump to="/docs/about/data-model/metric">Metric</Jump>

## FAQ

### Why Not _Just_ Events?

Although Vector generalizes all data flowing through it as "events", we do
not expose our data structure as such. Instead, we expose the specific event
types (`log` and `metric`). Here's why:

1. We like the "everything is an event" philosophy a lot.
2. We recognize that there's a large gap between that idea and a lot of existing tooling.
3. By starting "simple" (from an integration perspective, i.e. meeting people where they are) and evolving our data model as we encounter the specific needs of new sources/sinks/transforms, we avoid overdesigning yet another grand unified data format.
4. Starting with support for a little more "old school" model makes us a better tool for supporting incremental progress in existing infrastructures towards more event-based architectures.


