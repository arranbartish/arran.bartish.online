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

- - -

Writing software is exciting and it can be quite a personal kick to observe the delight of those that interact with the software. It is my opinion that those who interact with the software goes beyond the end-user and includes those that operate, develop, and provide vision of the software which includes;

* testers
* programmers
* analysts
* subject matter experts
* operations

There are properties of the software that we write which can delight these groups and I feel has a direct impact on being able to sustainably delight our end-users as a result. I am going to focus on some techniques that contribute to resilience to change. 

## The basics are good

When we first start to look at automated testing there are a lot of simple examples which are intended to get you excited and give you the basics. The system under test (sut) is simple and easy to rationalize with simple inputs and results.  

```java
BowlingGame sut = new BowlingGame();
sut.roll(10)
assertThat(sut.score()).isEqualTo(10);
```

The basics of red, green, refactor applied over and over again can lead us to some of the testing patterns that we want to apply to maintain our delight. Eventually we'll come across an existing data model that may be more difficult to create. It may be that the model is a fairly well understood concept within the business, perhaps something that is generated from a government regulated financial model.  

\[insert model uml]

## The noise trap

If we don't grow then we start to see some of the test smells that make our tests fragile and start to reduce our delight. 

```java
private MortgageEvaluator sut = new MortgageEvaluator();

@Test
void willApproveMortgage_WhenMoreAssets_ThanDebts() {  
  Application application = new Application();
  Applicant applicant = new Applicant();  
  applicant.setName("John");  
  application.set(applicant);  
  Employer job = new Employer();  
  job.setRole("programmer");  
  job.setCompany("Delightful Software");  
  job.setSalary(new Money("100"));  
  applicant.setEmployer(job);  
  applicant.setDebts(List.of(new Debt(new Money("50")))); 
  applicant.setAssets(List.of(new Asset(new Money("60"))));  
  application.setRequestedAmount(new Money(100));

  Decision result = sut.evaluate(toApprove);

  assertThat(result.getLineOfCredit()).extracting(LineOfCredit::getMaximum).isEqualTo(100);
  assertThat(result.getResult()).isEqualTo(approved);
 }
```

There is very little delight in the above test and we have just one test case. We will write the next test case and we'll have duplicate code that we'll refactor and eventually we'll start to use the [Creation Method](http://xunitpatterns.com/Creation%20Method.html). Nexit

These are great places to start and they are valuable, however we must recognize that as professionals we must grow beyond the basics in order to solve those more interesting problems. If we don't then we run the risk of everything looking like a nail to our proverbial hammer. 

## 

If we apply the basics to all our problems then we'll find that our tests become noisy. 

test with simple assert

mothers

traps

other things

what other people say

I've been writing software and its automated tests since 2006 and as a continuous learner I've developed skills and reflexes that make the tests and systems that I write more delightful. 

We are all developers and we are all on our own journeys to be better every day, so with that in mind, I can't offer you a short cut or a secret sauce, but I can and there is no secret sauce. 

. I remember seeing tests that had 

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
