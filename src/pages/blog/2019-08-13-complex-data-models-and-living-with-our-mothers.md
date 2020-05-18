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
  - Resilience
---
![Happy mothers day note with flowers](/img/mothersday.jpg)

****

****

**Message:** If you're struggling with tests that are hard to understand or maintain, engineering patterns may be your path to maintainable production software. 

**Why can it be a problem:** It can happen that as your team adapts to change, your code needs to adapt significantly to its new context. Your hundreds or thousands of tests can reduce confidence and result in the feedback equivalent of a Christmas tree (All green and red, probably mostly red). 

**Surprising fact:** The use of some good engineering patterns in your tests can ensure your tests are robust to change and remain the guardians of your confidence and production software. 

**What you'll take away:** We'll discuss some of the common indicators that you might see in your project and some critical things that can be done early to reduce their impact. It's never too late to start introducing these concepts even if your software is mature. 

**I am passionate about this because:** I am excited about software and the delight that it brings everyone who interacts with it, including end users, operators and the developers.  

**outline**

**Steps on this journey:** 

* I started writing automated tests in 2005 and I've been "test infected" ever since. There are times when I try to imagine how I ever wrote some of the systems I did without the tests that bring me so much confidence today.
* The early tests that I wrote were not great. In some cases I suspect most of the tests were written so that they would pass, but I wonder how much value they actually brought when they failed, other than the system is broken.  
* Experience started to show that the most valuable tests i'd written were protecting me as I made changes. They would not only highlight that the system was broken, but they would explain to me why. 
* The test after approach was moderately successful, but this was only the last part of a tests possible useful life cycle. I wasn't until I was exposed to things like automated acceptance test, behaviour, and example driven approaches that I started to crack the two first two stages from test first approach.

[![Tests (especially microtests) have a journey: First they are prophets, Then they are guides, Then they are guards.](/img/tottinge-twitter-prophets-guides-guards.png 'Tim "Agile Otter" Ottinger on the test journey')](https://twitter.com/tottinge/status/1126136286966943745)

* There were still things that I was learning about what brittleness meant, size and expressiveness of the tests. There was an emergent pattern for the smells that would develop in my tests, most of the time it was due to a lack of or mistakes in engineering.
  * mixed concerns / violating SRP
  * WET tests
  * Ignoring design patterns because these are "just" tests

[![Be precise with test assertions. Give your microtest only one reason to fail. Brittleness is over-dependency 90+ percent of the time.](/img/tottinge-twitter-test-engineering.png 'Tim "Agile Otter" Ottinger on tests that test too much')](https://twitter.com/tottinge/status/1127614638785486849)

* I started to find that when I made good engineering decisions around my tests early then my tests were clearer, more stable, and more valuable

[![tdd pro-tip #6: prevent complex test data from spiraling out of control by going to builder & custom comparator early on.](/img/geepawhill-twitter-builder-comparators.png "GeePaw Hill on planning for your system to become more complex early")](https://twitter.com/GeePawHill/status/1043228698512695296)

* 

[![Tests are partitioned by threads of behavior, not by classes. Any given test will often involve many classes within the tested behavior.   You may partition your production code with classes; but should not force your tests to adhere to that structure.](/img/uncle-bob-martin-2020-01-05.png "Robert Martin on the scope of a test")](https://twitter.com/unclebobmartin/status/1213826854957854721)

"Testing shows the presence, not the absence of bugs" - Edsger W. Dijkstra

* As valuable as simple examples are, they don't help us when we get to the components that need complex object graphs or data models.

```java
BowlingGame sut = new BowlingGame();
sut.roll(10)
assertThat(sut.score()).isEqualTo(10);
```

But what do we do when our setup data or model is more complicated than `10`

```java
@Test
void willApproveMortgage() {
  MortgageEvaluator sut = new MortgageEvaluator()
  Mortgage toApprove = new Mortgage();
  Applicant john = new Applicant();
  Money Amount = new Money();

  Decision result = sut.evaluate(toApprove);

  assertSoftly(softly -> {
      softly.assertThat(mansion.guests()).as("Living Guests").isEqualTo(7);
      softly.assertThat(mansion.kitchen()).as("Kitchen").isEqualTo("clean");
      softly.assertThat(mansion.library()).as("Library").isEqualTo("clean");
      softly.assertThat(mansion.revolverAmmo()).as("Revolver Ammo").isEqualTo(6);
      softly.assertThat(mansion.candlestick()).as("Candlestick").isEqualTo("pristine");
      softly.assertThat(mansion.colonel()).as("Colonel").isEqualTo("well kempt");
      softly.assertThat(mansion.professor()).as("Professor").isEqualTo("well kempt");
      // no need to call assertAll, it is done by assertSoftly.
   });
}
```

> The 'mother of all creation methods' is Object Mother

* Meszaros, G. (2010). XUnit test patterns: refactoring test code.

> Object Mother which is a combination of [Creation Method](http://xunitpatterns.com/Creation%20Method.html), [Test Helper](http://xunitpatterns.com/Test%20Helper.html), and optionally [Automated Teardown](http://xunitpatterns.com/Automated%20Teardown.html).

* Meszaros, G. (2010). XUnit test patterns: refactoring test code.

## References

![Book cover: xUnit Test Patterns - Refactoring Test Code](/img/xunit-test-patterns.gif)

## Images

[Photo by Giftpundits.com from Pexels](https://www.pexels.com/photo/happy-mothers-day-card-beside-pen-macaroons-flowers-and-box-near-coffee-cup-with-saucer-2072160/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)
