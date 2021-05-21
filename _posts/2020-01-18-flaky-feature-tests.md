---
layout: post
title: The ‘flakiness’ of feature testing
date: 2021-01-18
---

For the new app my team is building it was decided that we should make use of a concourse pipeline to enable us to do continuous integration, as opposed to manually deploying new builds. 

One of the jobs in the pipeline was our suite of smoke tests. In the smoke tests we included a number of feature tests. Unlike model spec tests, which test ActiveRecord models by themselves, feature specs test the whole “stack” including model code, controller code, and any HTML/CSS/JavaScript together. As a consequence of this feature tests are relatively time-consuming to run because you’re running more stuff than in a model spec. 

Feature tests are also different in that they replicate the user journey in a browser, as opposed to being run within a terminal. Running tests in a browser better replicates the user experience but it also opens up the tests to multiple avenues of failure which may lay outside the code. 

This happened recently to our service, the smoke tests would intermittently fail when being built in the pipeline and no one was quite sure why. When run locally the feature tests were very reliable, and never failed, this suggested that the tests were fine from a code standpoint and that the issue was related to the infrastructure surrounding the pipeline. 

Eventually, after much digging, it emerged that the smoke tests had been failing as sometimes the javascript associated with the tests was not able to execute in time. This hadn’t occurred when running the tests locally as there was no lag in the execution of the code. The solution was to change the code in such a way that the test would be able to ‘wait’ around for what it expected to see rather than jumping the gun and failing prematurely if it did not get an immediate result. 

It was interesting to discover the cause of the flakiness in this instance. It seems that in software engineering flaky tests are seen as an occupational hazard and not really a big deal, as the tests could just be rerun until a build passed. I appreciate that it’s not usually worth the time investment to investigate these issues but I was glad I had the opportunity to do so as it removed some of the mystery regarding flaky tests. Prior to this I didn’t really know why they would fail, I would just shrug my shoulders and try to rerun the tests. I now feel a lot less anxious about the failure now I know the likely cause.
