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

...

## Integrating Javascript tags onto your website

See:
https://github.com/snowplow/snowplow/wiki/integrating-javascript-tags-onto-your-website
