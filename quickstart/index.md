---
layout: page
title: Quickstart
---

This short guide should wal you through deploying `HeyNow` in test purposes, using docker. 
You will need server with `docker` and `docker-compose` installed.

### Recommended system requirements 

* 8 cores
* 16 GB RAM
* 10 GB hard drive

### Installing docker

> Feel free to skip this step if you have docker and docker-compose already installed.

First, you need to install docker. To do so quick installation script provided by Docker can be used:

`curl https://get.docker.com | sh`

Remember to start docker service afterward. 

`systemctl start docker`

Finally you can install docker-compose. You can get it from GitHub.

`curl -L "https://github.com/docker/compose/releases/download/1.8.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`
`chmod +x /usr/local/bin/docker-compose`

## Starting HeyNow

Having the server prepared you can start HeyNow. 

First, download `docker-compose.yml` from GitHub.

`curl https://raw.githubusercontent.com/heynow-io/heynow-compose/master/docker-compose.yml > docker-compose.yml`

Then you can start it using docker-compose. 

`docker-compose up -d`

This command starts the database, RabbitMQ, custom SMTP server and all the HeyNow services.
After a minute, whole system should be up. You can verify this by visiting either Eureka on port `9000` or 
Shepherd on port `8080`. There should be several services registered, eg. `configserver`, `stream-manager` and `email-sink`.

![Shepherd](/images/shepherd.png)

## Testing HeyNow

Currently HeyNow doesn't expose UI. To create new pipeline, you will need to use REST API.

First you need to create stream, by sending `POST` request to `stream-manager`
Fill `your_email@here` using your email address. This json describes stream 
that has one operator - `email-sink`. Every time there will be `plain-notification` send, HeyNow will send an email.

```
http://<ip>/stream-manager/streams
POST
{
  
   "name": "testing",
   "description": "doing nothing really",
   "rootNode": {
       "operator": {
           "name": "email-sink",
           "eventSource": "manual",
           "eventType": "plain-notification",
           "properties": [
               {
                    "name":"recipient",
                    "value":"your_email@here"
               },
               {
                   "name":"subject",
                   "value":"It's a test alert"
               }
           ]
       }
   }
}
```

Having the stream created you can start feeding HeyNow with events.
To do so, send `POST` request to `event-source`.

```
http://<edge_url>/event-source/event
POST
{
   "source":"manual",
   "type":"plain-notification",
   "payload" : {
       "health": "unhealthy"
   }
}
```

After sending this request you should receive email from `HeyNow`.
Because the SMTP server created by docker doesn't have reputation, most likely the message
will end up in SPAM catalogue. Sometimes the recipient mailbox will block this SMTP server. If you didn't received email,
check logs from `heynow-smtp` docker container if there are some errors.
