---
templateKey: blog-post
title: Individually wrapped assorted assertions
date: 2020-08-15T01:05:22.412Z
description: >-
  Good tests stand by an application from beginning to end. Choosing the wrong
  assertion for a test can make a test more expensive, fragile, or devalue it
  entirely. There are many different approaches to your assertion and there is
  no one assertion to rule them all. 
featuredpost: true
featuredimage: /img/lolly.jpg
tags:
  - Assertion
  - Testing
  - Engineering
  - Quality
  - Agility
  - Robustness
---
![Unwrapped lolly with wrapped lollies in the background](/img/lolly.jpg "Unwrapped lolly")

When it comes to our tests, if our tests are green we're satisfied and more or less ready to roll this change out to production. If our tests are red then our system is broken or deviated from the behaviour that would would otherwise describe as "working", thank goodness we have those tests. It can happen that we look to the test report and our hearts sink at the least helpful feedback we could get. 

```
expected <true> but was <false>
```

Typically this sort of feedback may come from an assertion that may look like this `assertEquals(true, sut.doSomething() > 0);`

A couple of questions instantly spring to mind from this feedback: 

1. What was false?
2. Why was it false?
3. why was it supposed to be true? 

The feedback lacks context and bug localisation and both of these mean that we're going to spend time gaining context and potentially debugging. 

We tend to not care too much when they're green.When we write a test it is probably because we want to know when our system is not behaving as we expect.
