---
layout: post
title:  "Building a kickass idea at Battle of the Hacks"
date:   2016-07-20 12:00:00
localhost: "localhost:4000"
extra_css:
categories: []
published: false
---


***Hackathon:** A 24–48 hour event where teams of up to four build something awesome. Examples include [a 2014 game similar to Pokemon Go](http://www.cbc.ca/news/canada/kitchener-waterloo/pokemon-go-similar-to-game-students-created-at-uw-competition-in-2014-1.3676833), [Iron Man’s hipster tech cousin](http://devpost.com/software/silicon-man) and more.*

—

A few weeks ago, I was a part of [Hack the North’s](https://hackthenorth.com/) team as a designer for Battle of the Hacks at Andreessen Horowitz’s HQ. It’s an exclusive 24 hour hackathon for hackathon organizers, with a grand prize of $25,000 for the team’s hackathon. Hack the North won last year with [an Android screen streaming app.](http://devpost.com/software/moocast)

This year, we wanted to try something even crazier. We ended up bringing [Instant Apps](http://www.theverge.com/2016/5/18/11705918/google-instant-apps-android-hands-on-video) to iOS. It was **a ton of fun **and to our surprise, **it worked. **By the end of the hackathon, our end result could open native iOS apps without installation. We called it OneApp.

### What is Instant Apps and why do we need it?
> We’re evolving Android Apps to run instantly without installation.
 — Ellie Powers, Product Manager at Google

During Google I/O 2016, Instant Apps was shown to the world. It’s a new concept allowing your device to not have to install any apps. Google is bringing this to Android phones and showed everyone how useful this could be.

<iframe src="https://medium.com/media/5899730a0c812880092c7441cb740078" frameborder=0></iframe>

The current state of apps is that all native apps have to be installed on your devices before they can be used. Native apps cannot be opened directly.

Similar to how people prefer streaming instead of downloading a movie, Instant Apps allows you to use the app without installing the app. It gets downloaded and lives in your device’s memory until you’re done using it.

## 1. Defining a Problem to Solve

*Every idea starts with a problem. What are you trying to solve? Is the problem worth solving? From the initial problem, it allows you to get the ball rolling and come up with different ideas for your hackathon.*

—

With the introduction of Instant Apps, the experience for using apps is going to be completely redefined. Constantly having to install apps to use them on infrequent occasions adds friction and underutilizes our phone’s limited storage space.

Google will be releasing this for Android developers and users soon. Since there is currently no way to open iOS apps without installation, we decided to build that experience during the hackathon.

Due to the time constraints of a hackathon, we had to narrow the scope our hack. In order to do that, we asked ourselves:

**What could improve your experience with your phone if you had access to all existing apps without installation?**

## 2. Brainstorming

*After defining the problem, it’s important to create a list of possible solutions. By the end of a hackathon, you want to show that your hack is useful and can add value to its users.*

—

After establishing the constraints, we needed to define how users would use our app. Having access to all apps on your phone opens a whole new world of ideas and experiences. Our team came up with several new use cases and thought through old ones, such as:

* Directly opening a native app from the browser

* Play a demo of a game like Flappy Bird

* Open an app from a QR code

* Receive push notifications from apps you don’t have installed

We had many more ideas for our app. Given that we had 24 hours, we scoped the project to the best ones.

## 3. Designing the Best Use Cases

*Be selective. From your list of ideas, select the best ones. Keep in mind that you will only have 24 hours for your hackathon. For your top ideas, start asking yourself how these solve your initial problem.*

—

### Browsing Apps

The first was being able to use any native app without installing it. When a user needs an app, OneApp would allow users to browse uninstalled apps that they can open directly. Users can search for an app similar to how they’d search for it in their iOS home screen and open it directly.

### Context Aware Apps

We introduced context(time, location, etc…) triggers to prompt users to use an app. This becomes especially useful for one-off apps. For example, event apps(Facebook F8, WWDC, etc…), airport apps, restaurant apps, etc. Each of these require specific contexts (time, location) for the app to be used.

For example, if your location says you’re at the airport, it’d ask you if you wanted to check in.

![](https://medium2.global.ssl.fastly.net/max/2000/1*tMC4yXGh7wp926yYbVVviw.png)**

**We want to invite users to use an instant app when they need it the most.**

By prompting the user to open the app when they needed it, we hoped to:

1. Increase the app’s visibility, allowing the user to know its existence. Without surfacing apps through prompt, they’re buried as one of thousands of apps on the App Store.

1. Allow I the user to become more productive. When in a certain context, there’s a high likelihood that a user has a need to be met. Providing that initial prompt allows users to accomplish that need.

### Deep Linking Apps

One of the most powerful features on mobile apps is the ability to deep link into other apps. We use it almost every day when we use our mobile web browser and find ourself opening an installed app.

At Google I/O, Ellie Powers presented the situation where a friend messages you a Buzzfeed URL. After clicking on it, your phone would open the native Buzzfeed app.

Our app would become a middle man between the mobile web browser and open the intended native app directly.

**From a user’s perspective, we’d be recreating Instant Apps on iOS.**

## 4. Building the Best Use Cases

*This is the step where all of your technical skills come into play. When working in teams, it’s important to flush out design and technical details on how you want to implement the solution to the initial problem.*

—

After establishing the task list for what needed to be done, we were ready for the hackathon.

### Implementation

Currently, opening an iOS app requires the app to be installed. If we wanted to be able to open an app that isn’t installed, we needed something that could run within an iOS app. That’s why we opted for React Native. React Native apps can be interpreted within the iOS app during runtime because it is based on JavaScript.

Similar to how Google has servers set up to serve Android apps to Android devices, we set up our own servers to store and serve our own apps. When a user wanted to use an app, the app would request for the app from a server with an app ID. The server responds with the source code of the requested app. OneApp would then [hot reload](https://facebook.github.io/react-native/blog/2016/03/24/introducing-hot-reloading.html) the requested app

### Product Design

*It’s important to ask ourselves how to design a solution for those 3 use cases. We want to keep in mind how a user should feel while using our app, and if we’re able to create a good experience that solves the problem at hand.*

—

We wanted OneApp to become the invisible middle man between the user and the apps they wanted to use. In order to allow users to find the app they need, we grouped all apps into 3 levels of visibility: push, recommended and browse.

**Push-level **apps get surfaced in two ways: through push notifications or through opening the app when the user’s context meets specific requirements. For example, you are at the Moscone Center during WWDC. These are brought to your attention if we’re over 90% sure you want to use this app.

**Recommended-level** apps are more loose than push in terms of requirements. These apps depend on some context, or how frequent you use the app.

**Browse-level** apps are all of the other apps. You may have never used them, you may use them frequently, but you aren’t in a context where we want to make them visible to you.

Depending on the context, the app gets opened in different ways.

* If it was through a push notification, we open the app directly because we know the user was interested in what the app had to offer.

* If the app is in a very specific context and the user opens the app from the home screen, we greet them and ask if they would like to use the most recommended app.

* In most cases where the user opens the app directly, we provide app recommendations as well as the ability to browse all app. This flow is similar to an App Store, but allows a user to immediately open an app versus having install as the only option.

### Visual Design

Good visual design is a key part of many winning hackathon projects. We were in an environment where we had to iterate fast and allow developers to quickly pull assets from the designer’s work.

We chose to use [Figma](http://figma.com) to design our UI. Since Figma lives in the web, it allowed developers on our team to explore and export all assets through a simple URL.

—

The first thing we designed was what our landing page would look like. Since some of our app’s functionality depends on context, we have different UI’s depending on the user’s context.

![](https://medium2.global.ssl.fastly.net/max/2000/1*i8v4IiugfHxhw1ycmHsfFw.png)**

![](https://medium2.global.ssl.fastly.net/max/2000/1*eAIAxhxS8H74t1S2_Ue4Ag.png)**

![](https://medium2.global.ssl.fastly.net/max/2000/1*_2UR12yHflFkw6HbeGDw2w.png)**

One of the best use cases are for airport checkin. We designed some mocks for our developers to prototype for our demo.

![](https://medium2.global.ssl.fastly.net/max/2000/1*1zICjbxSA8wtm3LJpIivag.png)**

![](https://medium2.global.ssl.fastly.net/max/2000/1*_YFT24sNAukKNhIqFT6VNA.png)**

![Mockups for a demo checkin app](https://medium2.global.ssl.fastly.net/max/2000/1*vtEtIb80QzuFQR5lEYRZ3w.png)*Mockups for a demo checkin app*

Maybe you want to check out the flights dashboard when you’re at the airport!

![Mockup for flights dashboard departing from SFO](https://medium2.global.ssl.fastly.net/max/2000/1*JABGYr-parV-qE9nTL5qJQ.png)*Mockup for flights dashboard departing from SFO*

Here are some of the instant apps that can be recommended to our users

![Mockups for recommended apps (including MooCast, our winning app from last year)](https://medium2.global.ssl.fastly.net/max/3800/1*Pc1p4wy90252f3H37q10Tw.png)*Mockups for recommended apps (including MooCast, our winning app from last year)*

## 5. Demo

We had 5 minutes to present our hack. We split our presentation into three parts:

1. **Problem:** Why did we build this app, and what we’re trying to solve.

1. **Demo: **What we managed to implement within 24 hours.

1. **Technology: **What we used to build this and what challenges we faced

1. **Potential: **What is the potential for this app

Skip to 42:20 to see the demo for our app.

<iframe src="https://medium.com/media/6d86430c8e90724291f7333f6278ddd7" frameborder=0></iframe>

## Takeaways

Hackathons are all about learning, having fun and feeling the satisfaction of making something awesome. For us, we were excited to turn an idea into a reality, and see how instant apps would feel on iOS.

![Team Hack the North after 24 hours of hacking(Michael Yoo, Zheng Tao, Kartik Talwar, Joey Pereira and myself)!](https://medium2.global.ssl.fastly.net/max/4036/1*tHZ12e10T-GCCwNVFviTAA.png)*Team Hack the North after 24 hours of hacking(Michael Yoo, Zheng Tao, Kartik Talwar, Joey Pereira and myself)!*

—

*If you are also interested in building ideas, designing solutions to problems or learning about technology and hacking, we want you to come to Hack the North. [Apply now](https://hackthenorth.com/)!*
