---
layout: page
title: Roadmap
---

> Current Stage: `Requirements Gathering`

## Alpha Milestone

* **Rest API** - Prepare Rest API for the event collecting
* **Basic Hard-coded rules** - Implement most commonly alerting rules as hard-coded strategies (no rule-definition language for now)
* **Emails** - Integrate email notification channel
* **Storage** - Implement `Storage` service which will be responsible for collecting and browsing alerts.
* **Schedulers** - Implement `Scheduler`, `Rule` and `Worker` 

## Beta Milestone

* **Auth** - Implement Auth that allow access control and restriction, taking a lot of the `Gitlab` concepts of groups and projects
* **Dashboard** - Implement first basic version of Dashboard for alert querying.
* **More Hard-coded rules** - Implement more rules to cover around 70% of the use-cases
* **Data Retention** - Add configurable time period in which the events will be stored
* **Slack** - Add slack notification channel
* **Content of alerts** - Add ability to specify content of alerts 
* **AWS Kinesis Integration** - Add integration with Kinesis

## Live Milestone

* **Rule language** - Advanced Rule-definition language 
* **Templates** - Add rules templates
* **Rule edition UI** - Add UI for rule definition
* **Test button** - Add ability to test alerts
* **Environments** - Add ability to distinct alerts by environments
