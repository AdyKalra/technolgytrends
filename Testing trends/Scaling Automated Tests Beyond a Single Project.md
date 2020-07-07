# Scaling Automated Tests Beyond a Single Project

### How to increase the ROI of your automated tests by using test frameworks with a highly readable DSL and reusable components

* This article shows corporations that have more than one application how to increase the ROI of their automated tests by having test frameworks with highly readable DSLs and reusable components. Companies with only one application still benefit from using the test frameworks suggested here for various reasons that we are going to explore.
Note: Automated tests here refer mostly to UI automated tests for web and mobile apps. However, we will also look at a few examples of API tests.
## The Problem
* In general, there are two types of reactions to automated testing. The first reaction is that it is difficult, takes too much time, devs can churn out features at a faster rate than testers can automate the tests, and we do not have the skills or the resources to do it, so let’s continue with manual testing for now. The second reaction is that it is easy, so let’s not spend too many resources on it. We can always catch up in the next sprint — and they never do.

* Well, here’s the hard truth: It is not easy to write and maintain automated tests, but you can make it easier and faster by using the right approach.
  * The first reason why automated testing is not as easy as many think it would be is that the UI nowadays is so much richer compared to a decade ago. Not only are the visuals getting more appealing, but the interactions — especially on mobile devices — are getting more complex. Suddenly, we are no longer dealing with just a single swipe but simultaneous multiple swipes to browse through the lists of movies on the Amazon Prime Video mobile app. Not to mention that in the pursuit of a richer lifestyle, a gamut of wearable IoT devices is born.
  * The second reason automated testing is notorious for taking a lot of time and effort is that the Agile landscape means tests often require changes in a short period of time. Over the years, I have seen a lot of automation code that struggled against this. Fast-paced release cycles require a smarter test approach. It is not just about writing the tests but also about easy-to-change code ready to reflect requirement changes on the fly, and yet with confidence that the code change will not break any tests.

## The Solution
* For testing to catch up to development, the QA team should take a leaf out of the dev team’s book. There is often a seed project that the developers can use to build an app right away. 
  * For instance, the seed project may contain a sample of an Angular project plus access to a wealth of Angular components from a central repository that your firm may have introduced to keep the look and feel consistent across all the apps developed in the firm. Learning by example, there should also be a seed project for automated tests — a test framework that imports a library consisting of components interacting with the UI components.
  * One such test component is highlighting a certain time period in a chart, which is certainly not something that can be done in a matter of one or two hours and guaranteed to be bug-free. Considering that it is no easy feat, we certainly do not want to repeat the effort in another project when both projects use the same graphical component — hence the goal of this article: free the testers from automating the app and let them focus on the real testing work.
  * Another reason for using a seed test project is that there is really no merit in having many test automation frameworks with varying implementations in the firm, unlike the concept of microservices that gives the dev team flexibility to choose the technology and language of choice best suited for the type of work it is doing. In fact, giving each squad or tribe the flexibility to use their own test framework of choice means loss of time because some may choose to write the framework from scratch, confusing test frameworks because each has his or her own interpretation of Page Object, and there is also the inability to share the test code.
* This article suggests that the firm keeps to only one or two test frameworks, these frameworks employ the Screenplay Pattern approach, and teams collaborate to produce reusable test components.
### The Screenplay Pattern
* There are three compelling reasons to use the Screenplay Pattern to scale:
  * It enables a highly readable DSL to be written, as we will see in the next section. Once the DSL is written, anyone (devs, manual testers, BAs from any squad) would be able to use it with a modest learning curve to form tests thanks to the easy-to-understand and articulate way to express the tests. This, in turn, speeds up the test writing process.
  * It is based on the concepts of actors, tasks, actions, and questions. Tests are formed by describing the tasks and questions from the viewpoint of the actors (users of the app) rather than pages or components. Each task is made up of actions (or even tasks). For instance, a search for flights is a task on a travel website and entering the destination is one of the actions for the task. The question we want answered is the total matching flights returned. Having them written this way means the action (“enter a value into the input field”) and the question (“the total items returned in the list”) can be reused in a shared library because they are solution-based interactions commonly found in most apps. Even business-based interactions can be shared across projects. For instance, someone in another department in your firm may have written the test code for adding, deleting, and retrieving an event from Google Calendar via API calls. If your app relies on the same interactions, then you could just reuse the shared task without taking a peek at the Google API documentation. Or perhaps your team’s app relies on the customer data created by another team’s app. In the same way, you could just reuse the 
  * Screenplay task shared by the other team to create the test data prior to running your test.
* At its core, the Screenplay Pattern is the application of the SOLID design principles. Desirable traits like separation of concerns, high cohesion, and loose coupling resulting from the principles pave the way for a clean, maintainable, and malleable test code.
### Why Not Page Object?
* A seasoned tester would find that Page Object falls short of a scalable and maintainable test suite. Many tried to overcome the weaknesses by employing variations of Page Object. In my opinion, the best variation so far is breaking the UI into components instead of pages and introducing a layer of abstraction between the UI and the tests. John Smart’s article on how to write Page Objects that “suck less” further suggests how to improve the approach by storing only the locators in the Page Objects, keeping the Page 
* Objects free of business logic, and categorising the abstraction layer into actions and questions. Next, apply the SOLID principles and use objects rather than methods to represent the actions and questions, and we naturally arrive at the Screenplay Pattern.
* Head to the Resources section down below to read articles that explain why you would want to employ these techniques. After reading the articles, you should be convinced of the benefits of the techniques mentioned.
* Perhaps you are already using Page Object and thinking of just using some of the techniques above without fully resorting to using the Screenplay Pattern. I’ll show you why you would still want to consider rewriting your whole test framework or switch over to a test framework that supports the Screenplay Pattern.
We have established in the previous section that a fluent DSL is highly attractive to meet our goal of a scalable test framework. Let’s take Cheapflights or any travel website as an example. Say a user wants to fly from London to Bali on the 1st of October 2020 and return on the 31st of October 2020. In the Page Object world, the action “search flights" would be represented by the ensuing method. This is the method that contains the implementation of the interactions with the website that you would call from your step library. We are not going to go into why you shouldn’t do the implementation in the step library itself.
searchFlights("London", "Bali", "1 October 2020", "31 October 2020");
* In an attempt to make this read better, you might use the Builder Pattern so that calling the method now looks like this:
Flight flight = Flight.builder()
                      .from("London")
                      .to("Bali")
                      .departOn("1 October 2020")
                      .returnOn("31 October 2020")
                      .build();
searchFlights(flight);
Now that looks better, but the Screenplay Pattern can make it even more elegant. This is possible because the action “search flights" is an object:
SearchFlights.from("London")
             .to("Bali")
             .departOn("1 October 2020")
             .returnOn("31 October 2020");
* Let’s take another example on the website. After making the basic search, users are presented with the search results and options to filter the results. Some of the options are in the form of a slider. You might create a Page Object for the slider component that takes in the data attribute of the slider container as a parameter to differentiate the sliders on the results page. Using the Builder Pattern for the stopover duration slider, the code looks like this:
Slider stopoverDurationSlider = Slider.builder()
                      .id(stopoverDurationSliderId)
                      .min(30)
                      .max(120)
                      .build();
slide(stopoverDurationSlider);
Compare that with the following if you were to use the Screenplay Pattern. Again, notice how the latter looks more fluent and natural:
Slide.toMin(30)
     .andToMax(120)
     .the(stopoverDurationSlider)
* There you have it. The solid reasons not to use Page Object.
### Which Test Framework to Use
* If you are sold on using the Screenplay Pattern but do not know how or where to begin, fret not because there are already a few open-source test frameworks that support it.
Serenity BDD is a Java-based test framework that supports both the Page Object and Screenplay Pattern. It acts as a wrapper on top of Selenium Webdriver for web automation and Cucumber/jBehave for BDD. You can also use it with Appium for mobile and desktop automation — see Appium for Mac and Appium Windows Driver — and REST-assured for RESTful API testing. That’s pretty much everything covered except Windows 7 because Appium Windows Driver only supports Windows 10 and above.
* It also comes in the TypeScript flavour, namely SerenityJS, for those who prefer the language. And if you prefer Puppeteer, SerenityJS doesn’t support it at the moment, but there is always an opportunity to extend the framework to include Puppeteer.
* Serenity BDD and SerenityJS have already solved part of the problem by giving us a plethora of common actions like hover, double-click, scroll to a target, move mouse to a target, and more. Also, see the available questions and matchers. I have personally used Serenity for a number of years and have been impressed by the built-in functionalities, including a great reporting tool.
* For the missing Windows 7 coverage (after all, it still has a 33.44% share in the market compared to Windows 10 at 55.72%, according to the latest Windows OS Families coverage report by Perfecto Mobile), I recommend using Specflow integrated with FlaUI. Specflow is a great .NET test framework that supports BDD and some additional extensions, although the latter is only available via licensing in Specflow+. Meanwhile, FlaUI is a driver in .NET that uses Microsoft’s UI Automation libraries under the hood to interact with Win32, WinForms, and WPF desktop applications. The good news is there is a project that wraps around Specflow that enables Screenplay Pattern usage called CSF.Screenplay, and it is inspired by Serenity. Therefore, you will be familiar with it right away if you have been working with Serenity. The bad news is, at the time of writing, it only has the extension to work with Selenium WebDriver, so you would have to create the FlaUI extension or wait for someone to contribute to the project.
## In Summary
Teams should start collaborating and not working in silos, as is often the case when it comes to automating tests. Having a single test approach is crucial, and we have seen in this article why the Screenplay Pattern is the cornerstone of a successful automation collaboration.
In short, use the Serenity BDD Java test framework. Offer SerenityJS as well if you have the extra capacity to let testers work with TypeScript. And finally, add the support for FlaUI via CSF.Screenplay if you care about your Windows 7 user base.
