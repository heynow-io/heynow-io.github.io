---
layout: page
title: Roadmap
---

> Current Stage: `Requirements Gathering`

## Alpha Milestone

* **Rest API** - Prepare Rest API for the event collecting
* **Event Source Operator** - Implement Event Producer Operator
* **Email Sending Sink Operator** - Integrate email notification channel
* **Stream Definition Storage** - Implement `Storage` service which will be responsible for storing and managing stream definitions.

## Beta Milestone

* **Alerting Service** - The service that will store alerts
* **Auth** - Implement Auth that allow access control and restriction, taking a lot of the `Gitlab` concepts of groups and projects
* **Dashboard** - Implement first basic version of Dashboard for alert querying.
* **More Hard-coded rules** - Implement more rules to cover around 70% of the use-cases
* **Data Retention** - Add configurable time period in which the events will be stored
* **Slack** - Add slack notification channel
* **Content of alerts** - Add ability to specify content of alerts 
* **AWS Kinesis Integration** - Add integration with Kinesis

## Live Milestone

* **Operators** - Advanced Operators for event backpressure, mapping and collecting. 
* **Templates** - Add rules templates
* **Rule edition UI** - Add UI for rule definition
* **Test button** - Add ability to test alerts
* **Environments** - Add ability to distinct alerts by environments
