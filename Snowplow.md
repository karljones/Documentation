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

The JavaScript Tracker appears in a script tag in the head section of a web page.

Example:

<pre>
<!-- Snowplow starts plowing -->
   <script type="text/javascript">

       ;(function(p,l,o,w,i,n,g){if(!p[i]){p.GlobalSnowplowNamespace=p.GlobalSnowplowNamespace||[];
           p.GlobalSnowplowNamespace.push(i);p[i]=function(){(p[i].q=p[i].q||[]).push(arguments)
           };p[i].q=p[i].q||[];n=l.createElement(o);g=l.getElementsByTagName(o)[0];n.async=1;
           n.src=w;g.parentNode.insertBefore(n,g)}}(window,document,"script","{{  theme_asset( '/static/js/snowplow/sp.js' ) }}","snowplow"));

       window.snowplow('newTracker', 'co', 'd1epsz32winqbo.cloudfront.net', { // Initialise a tracker
           appId: 'Unique_string_to_identify_application', // Application ID. 
           platform: 'web'
       });
       window.snowplow('enableActivityTracking', 30, 30); // Ping every 30 seconds after 30 seconds
       window.snowplow('enableLinkClickTracking');
	   
	   window.snowplow('trackPageView');
			   
		window.snowplow('trackUnstructEvent', {
			schema: 'iglu:com.acme_company/viewed_product/jsonschema/2-0-0',
			data: {
				productId: 'ASO01043',
				category: 'Dresses',
				brand: 'ACME',
				returning: true,
				price: 49.95,
				sizes: ['xs', 's', 'l', 'xl', 'xxl'],
				availableSince: new Date(2013,3,7)
			}
		});

   </script>
<!-- Snowplow stops plowing -->
</pre>

See:

* https://github.com/snowplow/snowplow/wiki/javascript-tracker-setup
* Integrating Javascript tags onto your website

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
