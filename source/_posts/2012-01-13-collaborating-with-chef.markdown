---
layout: post
title: "Collaborating with Chef"
date: 2012-01-13 16:25
comments: true
categories: 
  - btmerr
  - chef
  - chmurph2
  - customink
  - devops
  - jmorton
  - opschef
  - opscode
  - web operations
---
This week at [CustomInk](http://www.customink.com), the Web Operations team was asked by the development teams to make some configuration changes on a couple of different servers.

They were simple changes, adding a line or two to the services.yml file for each application. The details really aren't important but let's look at how we worked together to implement the changes.

## Before Chef

In the past, here's how the changes likely would have been implemented.

1. Developer realizes a change is required.
1. Developer asks the ops team to make the change
1. Ops makes the update using the appropriate tools

OR

1. Developer realizes a change is required.
1. Developer considers asking the ops team to make the change but thinks better of it
1. Developer makes the change manually, Ops doesn't know, Ops can no longer provision a new server properly.

## With Chef

We've been using Chef for some time and have just started asking our developers to help maintain their own apps. This week, two applications needed to know about some additional external services. This required a simple update to a YAML file in each application. In both cases, I asked the developers to clone our chef repo, make the changes they needed, and submit a pull request.

In one instance, the simple services.yml turned into a pull request with updates to a number of nagios nrpe checks that we're running. Something that the developer didn't ask for originally but took the initiative to add while in the code.

Thanks to [@chmurph2](http://twitter.com/chmurph2) and [@jmorton](http://twitter.com/jmorton) for taking their first steps into Chef.

Is this a huge accomplishment? No.  But it is a great first step.

".@nathenharvey Working together == every engineer is on the same team and you stop celebrating (or thinking about) cross-team collaboration."

We've always worked as one team but continue to have some clear areas of responsibility. While I understand what Brian's saying, I'm not sure everyone doing everything makes sense. We're one team but we each have our strengths. Agree that we should stop celebrating about this a cross-team collaboration; it should be the norm.  But, we have to start somewhere and these were the first steps into the world of infrastructure as code for the developers. In my mind, that's a WIN!
