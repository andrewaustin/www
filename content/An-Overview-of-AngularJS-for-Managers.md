---
title: "An Overview of AngularJS for Managers"
date: 2014-08-14T18:00:00-04:00
toc: true
type: "article"
---

In late 2013, I started building things in my free time using AngularJS and it has been an incredibly rewarding and productive journey. I started out in my JavaScript journey building single page applications using Dojo at IBM. More recently, I transitioned to working at a company that uses Node.js on the backend and Angular.js exclusively on the frontend.

At IBM I lobbied hard for my team to switch to Angular.js and wrote the first version of this article to make an objective argument that AngularJS was ready to be used in building enterprise single page applications. In particular, I hoped to make the case that large corporations would not lose anything by switching to AngularJS. Over the past several months of using Angular.js exclusively, this core argument has not changed, but I've also encountered a few things Angular.js could do better at. Many of Angular's weaknesses are things that Dojo and other legacy javascript frameworks do quite well.

This article is my attempt to share what I know.

I am first going to give a brief history of Angular, then dive into what is important to enterprises by talking about:

* Who is behind AngularJS?
* How can I hire and educate developers?
* What kind of browser support does AngularJS have?
* How does Google protect AngularJS' intellectual property?
* What GUI toolkits work with AngularJS?
* How can I handle internationalization and accessibility in Angular?
* How can I test my AngularJS applications?
* What are some painful aspects of AngularJS?

AngularJS has huge shoes to fill. Despite not being touted on [Hacker News](https://news.ycombinator.com/) or [/r/programming](http://www.reddit.com/r/programming/), Dojo (and its complimentary UI widget toolkit Dijit) has always been an incredibly versatile platform for serious single page application development. Many of the “best practices” in the JavaScript world were first adopted by Dojo before being taken up by others. (See an interesting talk by Peter Higgins called [Dojo Already Did That](http://www.youtube.com/watch?v=BY0-AI1Sxy0) for more information.)

But the JavaScript world is increasingly volatile. Technology is changing rapidly. New frameworks are being introduced everyday and many are dying as quickly as they are created. If you follow [/r/javascript](http://www.reddit.com/r/javascript) or Hacker News, then throughout the course of a week you will probably see 4-5 frameworks being touted as the next great thing.

It's no wonder that companies building serious software are reluctant to make changes to their JavaScript technology stack. Today's fad will likely not be around tomorrow.

But there is hope in the JavaScript world. Over the past year some serious frameworks have really established themselves as viable alternatives to Dojo and jQuery spaghetti code. Frameworks like Backbone.js and Ember.js are excellent Model-View-Whatever frameworks that are perfectly suited to building great single page applications

But, for various reasons, I think we can do better than Backbone.js for enterprise applications. And the market seems to be agreeing with me. Angular.js just seems like it has more to offer.

But a comparison of why “Why Angular is Better” is a post for another day. Today I simply want to convince you, as an enterprise, that Angular is as viable as Dojo for building large scale, single page, applications.

### The History of AngularJS

AngularJS was created, as a side project, in 2009 by two developers, Misko Hevery and Adam Abrons. The two originally envisioned their project, GetAngular, to be an end-to-end tool that allowed web designers to interact with both the frontend and the backend.

Hevery eventually began working on a project at Google called Google Feedback. Hevery and 2 other  developers wrote 17,000 lines of code over the period of 6 months for Google Feedback. However, as the code size increased, Hevery began to grow frustrated with how difficult it was to test and modify the code the team had written.

So Hevery made the bet with his manager that he could rewrite the entire application using his side GetAngular project in two weeks. Hevery lost the bet. Instead of 2 weeks it took him 3 weeks to rewrite the entire application, but he was able to cut the application from 17,000 lines to 1,500 lines. (For a talk from Misko Hevery about the full history up until January 2014, see [his keynote from ngConf 2014](http://www.youtube.com/watch?v=r1A1VR0ibIQ)).

Because of Hevery's success, his manager took notice, and Angular.js development began to accelerate from there.

### Who is Behind AngularJS?

Google.

One of the original creators, Adam Abrons stopped working on AngularJS but Misko Hevery and his manager, Brad Green, spun the original GetAngular project into a new project, named it AngularJS, and built a team to create an maintain it within Google.

One of AngularJS' first big wins internally at Google occurred when the company DoubleClick was acquired by Google and they started rewriting part of their application using AngularJS. Because of DoubleClick's initial success, Google seems to have invested even more resources into Angular and has blessed AngularJS for internal and external product usage.

Because of this, the Angular team inside Google has grown rapidly.

Take a look at the list of the top 10 contributors to AngularJS as of 2/8/2014 (when this article was first written):

<table>
<tr>
<th>Contributor</th>
<th>Company</th>
<th>Last Commit</th>
<th>Commits</th>
</tr>
<tr>
<td>Igor Minar</td>
<td>Google</td>
<td>02/07/2014</td>
<td>1222</td>
</tr>
<tr>
<td>Misko Hevery</td>
<td>Google</td>
<td>10/10/2013</td>
<td>703</td>
</tr>
<tr>
<td>Vojta Jina</td>
<td>Google</td>
<td>01/31/2014</td>
<td>327</td>
</tr>
<tr>
<td>Matias Niemela</td>
<td>Google</td>
<td>02/07/2014</td>
<td>177</td>
</tr>
<tr>
<td>Pete Bacon Darwin</td>
<td>Google</td>
<td>01/23/2014</td>
<td>135</td>
</tr>
<tr>
<td>Brian Ford</td>
<td>Google</td>
<td>02/07/2014</td>
<td>69</td>
</tr>
<tr>
<td>Tobias Bosch</td>
<td>Google</td>
<td>02/16/2014</td>
<td>47</td>
</tr>
<tr>
<td>Chirayu Krishnappa</td>
<td>Google</td>
<td>11/22/2013</td>
<td>40</td>
</tr>
<tr>
<td>Ken Sheedlo</td>
<td>Google (Intern)</td>
<td>09/27/2013</td>
<td>29</td>
</tr>
<tr>
<td>Caitlin Potter</td>
<td>Google</td>
<td>02/04/2014</td>
<td>23</td>
</tr>
</table>

Now take a look at this updated table of the top committers as of 8/25/2014:

<table>
<tr>
<th>Contributor</th>
<th>Company</th>
<th>Last Commit</th>
<th>Commits</th>
</tr>
<tr>
<td>Igor Minar</td>
<td>Google</td>
<td>08/22/2014</td>
<td>1380</td>
</tr>
<tr>
<td>Misko Hevery</td>
<td>Google</td>
<td>11/10/2013</td>
<td>703</td>
</tr>
<tr>
<td>Vojta Jina</td>
<td>Google</td>
<td>07/14/2014</td>
<td>350</td>
</tr>
<tr>
<td>Pete Bacon Darwin</td>
<td>Google</td>
<td>08/23/2014</td>
<td>323</td>
</tr>
<tr>
<td>Matias Niemela</td>
<td>Google</td>
<td>08/05/2014</td>
<td>232</td>
</tr>
<tr>
<td>Brian Ford</td>
<td>Google</td>
<td>08/22/2014</td>
<td>162</td>
</tr>
<tr>
<td>Caitlin Potter</td>
<td>Google</td>
<td>08/22/2014</td>
<td>104</td>
</tr>
<tr>
<td>Tobias Bosch</td>
<td>Google</td>
<td>08/22/2014</td>
<td>67</td>
</tr>
<tr>
<td>Rodric Haddad</td>
<td>Google</td>
<td>08/15/2014</td>
<td>47</td>
</tr>
<tr>
<td>Chirayu Krishnappa</td>
<td>Google</td>
<td>03/20/2014</td>
<td>42</td>
</tr>
</table>

The first thing you'll notice is that they are all Googlers. This might make you uneasy, and to be sure, relying on a framework that is entirely controlled by a single entity can be a little risky from a business perspective.

However, there are many positives about the AngularJS team all working for Google. For one, having one commercial entity control the framework can often be a positive because it completely avoids infighting between political factions. In the open source world, this infighting can be public and nasty, detracting for the team's purpose of building great software. Forks of open source software can often be bad for consumers, especially in the short term where battle lines are drawn and collaboration ceases.

Just look at one of the recent high profile fights between the two of the company's backing Node.js, [Joyent and Strongloop](http://gigaom.com/2013/12/02/slap-fight-in-node-js-land/). You company can certainly do without all this manufactured developer drama happening while you're trying to build enterprise grade software.

Back to the table...

What about non-Google contributors? Surely they exist, right?

They do. The first non-Google contributor is the 14th most active AngularJS contributor, Shahar Talmi, who works for a company called Wix. (Ken Sheedlo is a former Google Intern who now works at rackspace. Almost all of his commits were while he was an intern, so I've not counted him as a non-Googler.) Shahar has made 27 commits ranging from documentation to new features.

In addition to Shahar there have been **943** unique contributors to the project. Some of them were certainly Googlers, but the vast majority are not.

There is one important fact that the above table hides, though. Many of the top contributors did not start out as Googler's, but were hired by Google after they started actively contributing to AngularJS. This again reaffirms the notion that Google is serious about investing in AngularJS.

Another odd thing you might notice about the above table is that the co-creator Misko Hevery and has not madeany recent commits compared to others on the Angular team. Why?

The answer to that is Google's investment into another language, Dart. Dart is a JavaScript replacement by Google, and Google has been “dog fooding” Dart internally by porting AngularJS to the Dart language. This port is known as AngularDart. This is where Hevery has been spending most of his time lately. Other members of the AngularJS team are also actively working on the Dart port of AngularJS.

Which is pretty interesting for us AngularJS developers. According to the Google team, porting Angular to Dart has been tremendous for AngularJS development because it has allowed the Angular team to introduce new ideas that ultimately make their way back into the JavaScript version.

### How Can I Educate & Hire Developers?

Compared to hiring jQuery developers, hiring AngularJS developers may be more difficult for an organization.  Traditional job sites like [indeed.com](http://www.indeed.com/q-Angular-jobs.html) give good overview of the high demand for good AngularJS talent. But don't worry, with each passing day more and more JavaScript developers are discovering AngularJS and they are using it to build real applications. In addition to traditional job sites for hiring AngularJS developers you may have better luck with specialized sites like [Stack Overflow Careers tagged with AngularJS](http://careers.stackoverflow.com/jobs/tag/angularjs) or one of the dedicated AngularJS job boards such as [Angular Jobs](https://www.angularjobs.com/).

Rather than hiring developers with AngularJS experience, it may be easiest to train your existing team or hire JavaScript generalists interested in learning AngularJS. AngularJS has traditionally been considered to have very poor documentation. This has been changing recently and it seems the core AngularJS team has made great strides to improve the documentation. See http://docs.angularjs.org/api for the official documentation.

One of the great things about AngularJS, however, is the availability of third party video tutorials and lessons. You can learn an incredible amount about Angular by watching the short (and mostly free) videos by John Lindquist at his [egghead.io](https://egghead.io/) training site. This site is full of 3-5 minutes videos introducing AngularJS topics using real code. Another great video introduction to Angular is Dan Wahlin's [AngularJS in 60ish Minutes](http://weblogs.asp.net/dwahlin/archive/2013/04/12/video-tutorial-angularjs-fundamentals-in-60-ish-minutes.aspx ) . If reading is more of your thing, a great introduction to AngularJS is an article by Todd Motto entitled “[Ultimate Guide to Leraning AngularJS in One Day](http://toddmotto.com/ultimate-guide-to-learning-angular-js-in-one-day/)."

More recently, AngularJS had its first conference, ngConf. This conference was incredible, and even more so because it was not put on by the core AngularJS team, but instead a few independent developers and companies in Utah. The best thing about this conference is that all the videos are posted on YouTube and can be found at http://www.youtube.com/user/ngconfvideos. My two favorite talks from the conference were Dave Smith's “[Deep Dive into Custom Directives](http://www.youtube.com/watch?v=UMkd0nYmLzY)" and Vojta Jina's talk on [Dependency Injection](http://www.youtube.com/watch?v=_OGGsf1ZXMs)

### What Browsers Does AngularJS Support?

Angular claims to support “Class A Browsers.” As of Angular 1.2, the Angular team considers the following browsers “Class A”:

* Chrome
* Firefox
* Safari
* iOS
* Android
* IE8+.

However, starting with AngularJS 1.3, the Angular team is dropping support for IE8 because Google has stated that it does not have a need to support IE8. The Angular team has asked the community if there are any community members willing to step up and support IE8. The AngularJS core team seems willing to help facilitate community development of IE8 support, but are just not interested in maintaining it on their own.

### What About AngularJS' Intellectual Property?

Intellectual property concerns are very important for enterprise software development, and the AngularJS team (along with Google) takes steps to protect their intellectual property and the intellectual property of the contributions they receive.

AngularJS is licensed under the MIT license.

AngularJS also makes all contributors sign an contributors license agreement (CLA). Google also accepts signed CLAs on behalf of a company. To make code contributions to AngularJS you or your company MUST have a signed CLA on file with Google, otherwise your contribution will be rejected.

Because of the MIT license and the strict CLA requirement, AngularJS is a good fit for enterprise usage, but you should probably consult your intellectual property lawyer for more details.

### What GUI Toolkits are available for AngularJS?

If you are coming from a Dojo background, you have certainly been spoiled by the Dijit GUI toolkit. It's the best out there when it comes to building HTML forms and widgets. Nothing else even comes close.

With that said, there are a couple of alternatives that work great with AngularJS.

The first, and most popular is angular-ui which provides a number of directives and modules that are pre-built and provide additional UI functionality. Their most popular widgets are provided by the [angular-ui/bootstrap](https://github.com/angular-ui/bootstrap) project which is an encapsulation of Twitter's Bootstrap widgets to Angular.

There are two major problems with angular-ui/bootstrap. The first is that the directives are not very accessible. Most of the widgets are missing wai-aria tags and you cannot tab between widgets. When building an application that is Section 508 compliant, or just accessible in general, angular-ui/bootstrap falls pretty short. The second issue is that Twitter's bootstrap does not support RTL locales. This feature has been planned for bootstrap for a long period of time, but they keep pushing this feature back. RTL support has been promised in 3.0, 3.1, and most recently 3.2. Each time it was not completed. Who kows if it will ever make it in?

If you're looking to go the commercial route, Kendo UI also has bindings for Angular that support RTL and seem to be more accessible than the angular-ui/bootstrap project. Another commercial option is [wijmo](http://wijmo.com/), which provides a variety of UI widgets for a variety of UI frameworks, including Angular.

### How Does AngularJS Handle Internationalization and Accessibility?

Out of the box, Angular comes with several filters that provide basic internationalization and localization features. These filters are the datetime, number, and currency. These filters provide the i18n features as their name suggests.

AngularJS also has a $locale service which allows you to detect the browsers locale and serve content according. This makes it incredibly easy to roll your own translation service for applications that need to support multiple languages. If you'd much rather use translations provided by well tested open source , a project called angular-translate is the preferred method of translating strings in AngularJS. Most details about using angular-translate can be found on angular-translate's [github page](https://github.com/PascalPrecht/angular-translate).

Nothing about core AngularJS makes AngularJS inherently inaccessible. However, most of your accessibilities issues are going to come as a result of the GUI toolkit you decide to use. Since no non-commerical GUI toolkit that works well with Angular is accessible (as mentioned in the GUI toolkit section), your best bet is to roll your own if you have strict accessibility requirements. Since AngularJS allows you to create easily tested and reusable DOM manipulating modules, called directives, rolling your own accessible widgets is not as bad as it first may seem.

This is probably the biggest area improvement for the AngularJS team if they are looking for more widespread enterprise adoption.

### How Can I Test My AngularJS Code?

Since one of the major pain points leading to the creation of AngularJS, as we know it today, was the inability to create good tests, it is no surprise that AngularJS takes testing very seriously.

Writing tests is easier in AngularJS than just about any other JavaScript framework out there. One of the core facets of AngularJS is its reliance of Dependency Injection. Dependency injection makes unit testing AngularJS incredibly simple because all your dependencies are passed as parameters to your modules. This means, mocking out your dependencies is a breeze as you can just manipulate the parameters that are passed to your modules. AngularJS core team has released a great guide to unit testing your AngularJS application. It can be found [here](http://docs.angularjs.org/guide/dev_guide.unit-testing). It is important to note that your development team can use the test frameworks they know and love (Jasmine, Mocha, QUnit, etc) without the need of changing to an AngularJS specific framework.

The AngularJS team has also released a number of tools to make testing AngularJS apps easier. One that I find really interesting is a Google Chrome plugin called Batarang. Batarang integrates with the Chrome developer tools and provides all kinds of interesting interesting insights into your AngularJS application. With Batarang you can see how your application scopes are nested, how well your application performs,  and a dependencies graph between your modules. These three features makes Batarang a great tool for working with AngularJS and understanding how your application code works together. Batarang is available [here](https://github.com/angular/angularjs-batarang).

End to End(e2e) testing is also a focus of AngularJS. The Angular team has created an e2e tool called [Protractor](https://github.com/angular/protractor) which uses the WebDriver API, much like Selenium does in the Java world. Much like AngularJS's unit testing guide, the AngularJS team has published a good introduction to e2e testing of AngularJS applications. You can read that guide [here](http://docs.angularjs.org/guide/dev_guide.e2e-testing).

In addition to testing, AngularJS takes code quality seriously. They do this in two ways. First, AngularJS adheres to ES5's “strict mode” which restricts you to a cleaner subset of JavaScript than what is normally available in the browser. Second, AngularJS makes use of jsHint for static analysis. JsHint ensures that code is consistent in its styling, and that many simple bugs you might find in projects not using jsHint have already been caught and cleaned up before they are committed.

### What are some painful aspects of Angularjs?
As already mentioned, the i18n and a11y elements of the AngularJS framework are a little weak, but improving everyday. There are a few other annoyances that sometimes come up as challeges when developing AngularJs applications.

The first is that AngularJS often has terrible error reporting. Due to the way that AngularJS is structured, sometimes you will see an error on the JavaScript console that points to the wrong line, or even the wrong file. This is especially a problem when you are unit testing your own code and manually performing dependency injection yourself. If you make a mistake, you can see some strange behaviors. One remedy I've used for working around this issue is to instrument my code with proper logging constructs so that I am not relying entirely on a browser's strack trace for debug information.

Another potential issue that you might have with Angular.js is that Angular.js is not opinionated. This is one of the biggest complaints you hear coming from the Ember.js community. If you were to look at a bunch of different Angular.js applications you'd probably find each of them doing things differently. Angular.js is very similiar to Dojo and jQuery in that regard, but this may make you comfortable if you expect your framework to decide on the *One True Way*. Personally, I find the flexibility of Angular.js to be a its strong suit, but some people prefer to paint by number instead.

### Conclusion

AngularJS is a great frontend framework for enterprise development. Its focus on testability and code quality really set it apart from other frameworks. It's not without some minor problems, however. If you do not mind a little extra freedom to go your own way and are willing to do a little bit more work to make sure your site is fully accessible, then AngularJS might be a perfect fit for your enterprise application.
