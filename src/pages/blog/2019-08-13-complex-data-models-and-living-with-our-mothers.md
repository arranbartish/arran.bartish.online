---
templateKey: blog-post
title: Complex data models and living with our mothers
date: 2019-08-13T14:04:10.000Z
description: >-
  Engineering software is hard and it's even harder when you don't have the
  freedom and confidence to make major changes to your application. Even those
  of us that might have amazing automation protection could find themselves in
  the awful position where a change could turn your tests from friends to foes
  as they all go red. There are engineering patterns that when employed can help
  keep your test suites friendly. I'll be exploring some of them here. 
featuredpost: true
featuredimage: /img/mothersday.jpg
tags:
  - Object Mother
  - Testing
  - Engineering
  - Quality
  - Agility
  - Robustness
---
![Happy mothers day note with flowers](/img/mothersday.jpg)

**Message:** Well engineered tests are critical to ensuring that your production code remains maintainable. 

**Why can it be a problem:** It can happen that as your team adapts to change, your code needs to adapt significantly to its new context. This can reduce result in the feedback equivalent of a Christmas tree, all green and red, probably mostly red

**Surprising fact:** Testing behaviours and use of good engineering patterns in your tests can ensure your tests are robust to change and remain the guardians of your production application. 

**What you'll take away:** We'll discuss some of the common indicators that you might see in your project and two critical things that can be done early to reduce their impact. It's never too late to start introducing these concepts even if your application is mature. 

**I am passionate about this because:** Tests can become an impediment and people blame the tests instead of identifying the grassroots engineering decisions that would make their lives easier.  

**outline**

**Steps on this journey:** 

* I started writing automated tests in 2005 and I've been "test infected" ever since. There are times when I try to imagine how I ever wrote some of the systems I did without the tests that bring me so much confidence today.
* The early tests that I wrote were not great. In some cases I suspect most of the tests were written so that they would pass, but I wonder how much value they actually brought when they failed, other than the system is broken.  
* Experience started to show that the most valuable tests i'd written were protecting me as I made changes. They would not only highlight that the system was broken, but they would explain to me why. 
* The test after approach was moderately successful, but this was only the last part of a tests possible useful life cycle. I wasn't until I was exposed to things like automated acceptance test, behaviour, and example driven approaches that I started to crack the two first two stages from test first approach.

![Tests (especially microtests) have a journey: First they are prophets, Then they are guides, Then they are guards.](/img/tottinge-twitter-prophets-guides-guards.png)

* There were still things that I was learning about what brittleness meant, size and expressiveness of the tests. There was an emergent pattern for the smells that would develop in my tests, most of the time it was due to a lack of or mistakes in engineering.
  * mixed concerns / violating SRP
  * WET tests
  * Ignoring design patterns because these are "just" tests

![Be precise with test assertions. Give your microtest only one reason to fail. Brittleness is over-dependency 90+ percent of the time.](/img/tottinge-twitter-test-engineering.png)

* I started to find that when I made good engineering decisions around my tests early then my tests were clearer, more stable, and more valuable

![tdd pro-tip #6: prevent complex test data from spiraling out of control by going to builder & custom comparator early on.](/img/geepawhill-twitter-builder-comparators.png)

"Testing shows the presence, not the absence of bugs" - Edsger W. Dijkstra

* As valuable as simple examples are, they allow us to ignore some of these principles.

```java
BowlingGame sut = new BowlingGame();
sut.roll(10)
assertThat(sut.score()).isEqualTo(10);
```

But that do we do when our setup data or model is more complicated than `10`

```java
@Test
void willApproveMortgage() {
  MortgageEvaluator sut = new MortgageEvaluator()
  Mortgage toApprove = new Mortgage();
  Applicant john = new Applicant();
  Money Amount = new Money();

  Decision result = sut.evaluate(toApprove);

  
}
```

## References

![Book cover: xUnit Test Patterns - Refactoring Test Code](/img/xunit-test-patterns.gif)

## Images

[Photo by Giftpundits.com from Pexels](https://www.pexels.com/photo/happy-mothers-day-card-beside-pen-macaroons-flowers-and-box-near-coffee-cup-with-saucer-2072160/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)
