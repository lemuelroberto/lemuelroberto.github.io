---
layout: post
title: "Book notes: Desingning Data-Intensive Applications"
date: "2018-06-04 08:00:00 -0300"
author: "Lemuel Roberto"
meta: "book notes"
---

> The big ideias behid reliable, scalable, and maintainable systems

**Author:** Martin Kleppemann

## Chapter 1

### What's the meaning of reliability?

Reliability is the system's ability to operates in the ways it's users expects even in the presence of faults.

A system maybe exposed to hardware, software and human faults along its lifetime and it's infeasible to prevent all of them.

What we can do it's to design our system in such way that those faults doesn't become a full system failure and continue to work as users expects with smallest possible damage.

### What's the meaning of scalability?

Scalability is the system's ability to cope with an increase demand due to increase of user base, requests, transactions, data or any other resources.

It's important note that there are more than one aspect to pay attention to when we're talking scalabily and it's our job to make sure we have a good understand how our system load looks like in order to answering two main questions:

1. how the system's performance is affected when we increase load and keep the resources unchanged?
2. how much of resources do we need to increase to maintain the system's performance when we increase a load parameter?

When mesuring perfomance there are many aspects to look at such as throughput or response time.

When dealing with online systems we're usually after a good response time to our clients. In such contexts, instead of using a mean, we can leverage percentiles to better understading which are the maximum response time for half or any other percentile of our user base.

To deal with the increase of load we can scale up our machines increasing memory and CPU or scale out our system adding the number of machines.

### What's the meaning of maintainability?

Maintainability is the system's ability to be operated in production, to be simply understood and changed.

When we have a system deployed in a production environment we want to be able to health check it, count the number of errors and find it's root causes easily, measure metrics as response time, cache miss and so on. And we whant to do all this with litle to none effort, in a visual way and when needed with as much as information as needed to respond to bugs or production faults as soon as possible.

As time goes on, the initial team are no longer maintaining the code base or the team is rapidly growing and it's our job to design our system to be easily understood by newcomers in a way that they can deliver code to production as soon as possible.

The last but not least aspect of maintainability is the system's ability to be changed to meet new load demands and to add brand new features to it. Some examples are changing a database of feature, adding a new cache layer or breaking our system into standalone services.
