---
layout: post
title: "MVVM with ReactiveCocoa 3, in Swift"
date: 2015-08-12 01:45:00 +0200
summary: "There are plenty of good introductions to the MVVM architecture on iOS. The next challenge is to apply these concepts in a real-world scenario! To find out how this could look like, I created an open-source Swift app that interacts with a remote server, using the brand-new ReactiveCocoa 3."
---

*__Update, 22 Oct 2015:__ The ReactiveCocoa core team [recently decided][rac-3-vs-4] to increment their major version alongside Swift. So while ReactiveCocoa 4 will use Swift 2, conceptually it stays very close to its Swift 1.2 counterpart, ReactiveCocoa 3. The required code changes are illustrated in my [ReactiveCocoa 4 migration example][migrating-to-swift-2-and-reactivecocoa-4].*

<hr>

Despite its somewhat unwieldy name, the __Model-View-ViewModel (MVVM)__ architecture has been gaining lots of traction in the iOS developer community in the last few years. This is no coincidence, as during that time, said community has also acquired a taste for [unit testing][nshipster-unit-testing] and [reactive programming][reactivecocoa], both of which are closely related to the concept, as we shall see.

MVVM promises to do away with the spaghettification that plagues many vanilla codebases which follow Apple's recommended structure, especially as their view controllers grow to [epic proportions][massive-view-controller]. It recognizes that view controllers are basically glorified views, and introduces a new layer between data (model) and presentation (view): the view model.

Bob Spryn has written [a fantastic introduction][sprynthesis-rac-mvvm] on what exactly that means, with animated illustrations and all. Honestly – if you only read one introductory post on the matter, make it this one!

Yet even after reading all of it (and a lot more), I felt unsure how to apply MVVM in a real-world application. Some of my most pressing questions were:

* If views own their view models, but the latter hold the business logic, how does one handle navigation between views?
* What if two views need to share some state?
* How can one tap into networking signals to report "loading" state to a view?

(Remember that "view" in the above questions now includes view controllers, too.)

## Learning by Coding

Looking for answers, I decided to write a little open-source app that would be simple enough to create in my free time, yet complex enough to shed some light on these issues. Since some of my colleagues and I love to play FIFA on our office Xbox, the app ended up being a match logbook with a simple rating system. Written in Objective-C, you can still find it on GitHub under the name of [ObjectiveGoal][objectivegoal].

As summer came, Swift became mature, and the ReactiveCocoa 3 betas began to stabilize. It was time to explore the new and long-awaited possibilities that Swift's type safety and syntax brought along. I took the old ObjectiveGoal code and started porting it to Swift, making improvements here and there. Some parts were redesigned entirely, due to the rather large differences between ReactiveCocoa 2 and 3.

The result is, somewhat predictably, __[SwiftGoal][swiftgoal]__ – now on GitHub for your reading pleasure! :smiley:

![SwiftGoal's New Match screen]({{ site.baseurl }}/resources/swiftgoal-new-match.png) ![SwiftGoal's Matches screen]({{ site.baseurl }}/resources/swiftgoal-matches.png) ![SwiftGoal's Rankings screen]({{ site.baseurl }}/resources/swiftgoal-rankings.png)

## What's Next

In the upcoming posts, I will explain my learnings in more detail and address all the questions mentioned earlier,

* [How to handle navigation and pass data between views?]({% post_url 2015-08-20-navigation-with-mvvm-on-ios %})
* [How to share state between views?]({% post_url 2015-10-13-sharing-state-between-views-with-mvvm %})
* How to report "loading" activity from a view model to a view?

 as well as the following:

* [How to replace (most) singletons by dependency injection, and how this benefits unit testing]({% post_url 2015-09-06-how-getting-rid-of-singletons-boosts-testability %})
* [How to use changesets to animate row changes in a table view]({% post_url 2015-12-30-animating-table-row-changes-using-changesets-with-mvvm %})
* [How to choose between mutable properties and signals in RAC]({% post_url 2016-07-30-exposing-view-model-properties-in-rac %})
* How to set up actions on view models in Swift to asynchronously handle user input

[rac-3-vs-4]: https://github.com/ReactiveCocoa/ReactiveCocoa/issues/2327
[migrating-to-swift-2-and-reactivecocoa-4]: {% post_url 2015-10-22-migrating-to-swift-2-and-reactivecocoa-4 %}
[nshipster-unit-testing]: http://nshipster.com/unit-testing/
[reactivecocoa]: http://github.com/ReactiveCocoa/ReactiveCocoa
[massive-view-controller]: https://twitter.com/colin_campbell/status/293167951132098560
[sprynthesis-rac-mvvm]: http://www.sprynthesis.com/2014/12/06/reactivecocoa-mvvm-introduction/
[objectivegoal]: http://github.com/richeterre/ObjectiveGoal
[swiftgoal]: http://github.com/richeterre/SwiftGoal
[swiftgoal-viewmodels]: https://github.com/richeterre/SwiftGoal/tree/master/SwiftGoal/ViewModels
