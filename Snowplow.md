# Snowplow

Snowplow is a marketing and product analytics platform.

Home page:

http://snowplowanalytics.com/

## Overview of the Snowplow process

Stages of the Snowplow process:

* Set up a Snowplow Tracker and/or Setup a Third-Party Webhook
* Set up a Snowplow Collector
* Set up Enrich
* Set up alternative data stores (e.g. Redshift, PostgreSQL)
* Data modeling in Redshift
* Analyze data

See:
https://github.com/snowplow/snowplow/wiki/Setting-up-Snowplow

### Set up Snowplow Collector

A Snowplow Collector receives (collects) data sent by a Tracker.

See:
https://github.com/snowplow/snowplow/wiki/Setting-up-a-collector

### Set up Snowplow Tracker

Snowplow Trackers generate event-data and send that data to Snowplow Collectors to log to S3.

Trackers are available for a variety of environments:

* Tracker	Description	Status
* ActionScript3 Tracker
* Android Tracker
* Arduino Tracker
* Golang Tracker
* iOS Tracker
* Java Tracker
* JavaScript Tracker
* Lua Tracker
* .NET Tracker
* Node.js Tracker
* PHP Tracker
* Python Tracker
* Pixel Tracker
* Ruby Tracker
* Scala Tracker
* Unity Tracker
* Golang Tracker

See:
https://github.com/snowplow/snowplow/wiki/Setting-up-a-Tracker

#### JavaScript Tracker

This document focuses on the JavaScript Tracker.

See:
https://github.com/snowplow/snowplow/wiki/javascript-tracker-setup

#### Integrating Javascript tags into website

...

See:
Integrating Javascript tags onto your website

### Enrichment stage

The enrichment stage "enriches" data in the S3 log files.

Generally, schema reference looks like this:

<pre>
iglu:vendor_name/event_name/jsonschema/2-0-0
---- ----------- ---------- ---------- -----
  |        |          |          |       |- schema version (model-revision-addition)
  |        |          |          |- schema format
  |        |          |- event name
  |        |- vendor of the event
  |- schema methodology
</pre>

On the other hand, the JSON schema describing the event will look like:

<pre>
{
    "$schema": "http://iglucentral.com/schemas/com.snowplowanalytics.self-desc/schema/jsonschema/1-0-0#",
    "description": "Schema for event_name",
    "self": {
        "vendor": "vendor_name",
        "name": "event_name",
        "format": "jsonschema",
        "version": "2-0-0"
    },
    "type": "object",
    "properties": {
        "productId": {
            "type": "string"
        },
        "category": {
            "type": "string"
        },
        ...
    },
    "minProperties":<<min number>>,
    "required": [<<list of required properties>>],
    "additionalProperties": <<false/true>>
}
</pre>

The important part here is the self section:

<pre>
"self": {
        "vendor": "vendor_name",
        "name": "event_name",
        "format": "jsonschema",
        "version": "2-0-0"
}
</pre>

## Integrating Javascript tags onto your website

See:
https://github.com/snowplow/snowplow/wiki/integrating-javascript-tags-onto-your-website
