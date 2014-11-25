---
layout: post
title: "Green Screen"
date: 2012-01-02 14:17
comments: true
categories: 
  - customink
  - devops
  - greenscreen
  - hudson
  - jenkins
  - sinatra
  - sysadmin
  - testing
---
[Green Screen](https://github.com/customink/greenscreen) is a build monitoring tool that is designed to be used as a dynamic Big Visible Chart (BVC) in your work area. It lets you add links to your build servers and displays the largest possible information on a monitor so that the team can see the build status from anywhere in the room.


<img src="http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/greenscreen.jpg" width="300" height="225" alt="Green Screen Monitor" />
We use Green Screen at [CustomInk](http://www.customink.com) to look after our continuous integration servers, currently 3 Hudson servers and one Jenkins cluster. We have a monitor mounted in the engineering office that makes it easy for everyone to quickly assess the build status.

Green Screen is a simple Sinatra application that is [easy to configure and deploy](http://nathenharvey.com/blog/2012/01/02/deploying-green-screen).  It works well with any continuous integration server that conforms to the [multiple project summary reporting standard](http://confluence.public.thoughtworks.org/display/CI/Multiple+Project+Summary+Reporting+Standard).

You can see a sample Green Screen app running at [http://greenscreenapp.com](http://greenscreenapp.com).  Be forewarned, this sample Green Screen looks at all of the builds currently running on [http://ci.jenkins-ci.org](http://ci.jenkins-ci.org).  This is fine for demo purposes but you may find it to be a bit overwhelming since it's **over 300 builds** at the time of this writing.


<!--more-->

## History
Green Screen was originally implemented by [Marty Andrews](https://github.com/martinjandrews) and [announced on his blog in 2009](http://blog.martyandrews.net/2009/08/greenscreen-build-monitor-bvc.html). In the original version, a build that was in progress would blink on the screen.
![http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/4565_building.jpg](http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/4565_building.jpg)

[Rhett Sutphin](https://github.com/rsutphin) improved the layout of green screen and introduced a new color, yellow, for builds that are in progress.
![http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/4566-building.jpg](http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/4566-building.jpg)

After using these versions for a while at CustomInk, we decided that the most important thing to know was which builds were failing. Once you get past a handful of builds, it's no longer very interesting to see every build. We forked Rhett's version and created a [new layout for Green Screen](https://github.com/customink/greenscreen).

If everything is passing, the screen is basically one giant checkmark.

![http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/green.jpg](http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/green.jpg)

If there are any failing builds, they're shown in the main area while all others are displayed on the right.

![http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/4567.jpg](http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/4567.jpg)

Finally, a build that previously failed will be shown in yellow while it's rebuilding.

![http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/4567_building.jpg](http://nathenharvey.s3-website-us-east-1.amazonaws.com/blog/images/greenscreen/4567_building.jpg)
We've also added support for controlling which builds are displayed from each CI server. So that you can explicitly include or exclude builds or just go with the default behavior of showing all builds on the server.

## Deploying
I'll cover a couple of deployment options for Green Screen in my [next post](http://nathenharvey.com/blog/2012/01/02/deploying-green-screen).
