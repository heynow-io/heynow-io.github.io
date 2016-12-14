---
layout: default
title: Home
---

# HeyNow

HeyNow is a Open Sourced alerting tool. 
Relatively simple, but powerful reactive engine and easy to integrate API makes it a perfect choice for both simple and complex alerting rules.

Developed and supported by [Ocado Technology](http://www.ocadotechnology.com/).

The idea behind HeyNow is really simple. HeyNow collects `events`, that are provided directly to Rest API by application or by one of the publishers:

* `AWS Kinesis` 
* `Elasticsearch`
* ...

Those events can be later used to define stream that will produce alerts. For example developer can configure:

* Send me SMS when event `foo` occurs,
* Send Email to support@support.com when there is more than 3 `bar` event in last 5 minutes,
* Send message to Slack if there was no events `foobar` in the last 24 hours,
* Send me SMS when more than 50% of fields `status` in event `gloo` has value equal `false`,
* Send me alert when average request processing time in last 30 minutes exceeded 1 second,
* ...