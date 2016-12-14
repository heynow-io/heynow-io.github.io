---
layout: page
title: How it works
---

### Alerts Processing

HeyNow operates on streams. If you are already familiar with reactive programming, getting to know 
HeyNow engine should be extremely easy. If not, please read this awesome [The introduction to Reactive Programming you've been missing](https://gist.github.com/staltz/868e7e9bc2a7b8c1f754).

Lets assume that our example application, call it `DeathStar`, every now and then sends to HeyNow `Event` with core temperature information.

```json
{
   eventType: "core-temperature",
   temperature: 2
}
```

We can describe this event stream on diagram:

```
coreTemperature: ---2----1--3----4--5---2-->
```

We want to receive alerts, when core temperature exceeds 3 enabling our engineers to start hyper-cooling systems preventing the whole construction from exploding.

First, we need to filter our stream:

```
coreTemperature: ---2----1--3----4--5---2-->
                 vvvvvvvv filter(>3) vvvvvvv
     dangerZone: ----------------4--5------>
```

Also, we don't want to spam our engineers - the cooling systems needs couple minutes to kick in. So, after sending an alert we want to keep tool quiet for 15 minutes.


```
coreTemperature: ---2----1--3----4--5---2-->
                 vvvvvvvv filter(>3) vvvvvvv
     dangerZone: ----------------4--5------>
                 vvv throttleFirst(15m) vvvv
     alerts:     ----------------4--------->
```

All we need to do now is to subscribe the `alerts` stream and send email when stream emits. 


| HeyNow allows to express this flow in a simpler manner than in the examples above. When setting up new pipeline one can use diagram drawing tool to simply drag and drop appropriate operators and connect them using arrows. | ![Architecture](/images/heynow-example.png) |

### Reactive Architecture  

HeyNow is build on Reactive Architecture. This means that in addition to use Micro-Services Architecture it follows these four principles:

* Event-Driven
* Scalable
* Resilient
* Responsive

This is achieved by building whole solution around the queue system. Each `Source`, `Operator` and `Sink` is a different service, eg.
we have `MapOperator` or `EmailSink`. Those services exchange `Events`, according to the `Streams` defined by users using queues.
Each service can scale independently adapting system to the load. 
Because the stream processing is realised in near real-time by exchanging messages, system is responsive and cost-effective. 
