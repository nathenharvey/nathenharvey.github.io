---
layout: post
title: "Learning Chef - Part 1"
date: 2012-12-06 17:07
comments: true
categories: 
 - chef
 - devops
 - github
 - knife
 - opschef
 - opscode
 - mulpat
 - sysadmin
 - vagrant
 - virtualbox
---

## Learning Chef Series

* [Part 1](http://nathenharvey.com/blog/2012/12/06/learning-chef-part-1/) - Introduce the project, configure workstation, and register a node with hosted Chef
* [Part 2](http://nathenharvey.com/blog/2012/12/07/learning-chef-part-2/) - Download cookbooks from the community site, add MongoDB, Apache, and Passenger to our node
* [Part 3](http://nathenharvey.com/blog/2012/12/14/learning-chef-part-3/) - Start writing a cookbook to deploy our application
* [Part 4](http://nathenharvey.com/blog/2012/12/19/learning-chef-part-4/) - Finish the application deploy, introduce roles


In November of 2012, [Patrick Mulder](https://twitter.com/mulpat) posted a [request on the Chef mailing list](http://lists.opscode.com/sympa/arc/chef/2012-11/msg00389.html).  He was 

{% blockquote %}
looking for some 1-1 teaching via skype to help me get going in setting up a basic DB server from scratch, as well as a basic dev server as intermediary step.
{% endblockquote %}

I thought this would be an excellent opportunity to feed my recent addiction to Google+ Hangouts.  I would provide Patrick some one-on-one tutoring if he would agree to having the sessions [broadcast live on YouTube](http://www.youtube.com/watch?v=l7-nAHdplD4&list=PLKK5zTDXqzFM53J6-rikDrqbbY0Pu-9SP).  We had some technical issues getting our first session going in a Google+ Hangout but we were able to meet via Skype and I captured video of the session.  

Our goal is to help you get up and running on Chef by following our progress.  The intent is to have additional sessions run via Google+ Hangouts that are steamed live to YouTube.  This post includes our first session which has been broken into nine short videos.  I hope you enjoy these videos and are able to learn something about Chef, too.  Both Patrick and I are looking forward to your feedback on this experiment.

You can [watch all of the videos in the YouTube playlist](http://www.youtube.com/watch?v=l7-nAHdplD4&list=PLKK5zTDXqzFM53J6-rikDrqbbY0Pu-9SP) or keep reading and watch each video in turn.

## Introduction

In this video we introduce ourselves and the project.

<iframe width="560" height="315" src="http://www.youtube.com/embed/l7-nAHdplD4" frameborder="0" allowfullscreen></iframe>

<!-- more -->

## Overview of Chef

In this video we visit the newly launched [Chef Documentation Site](http://docs.opscode.com) and look over the [Overview of Chef](http://docs.opscode.com/chef_overview.html) diagram.

<iframe width="560" height="315" src="http://www.youtube.com/embed/2BCNpHNZzy8" frameborder="0" allowfullscreen></iframe>

For our project the Chef Workstation will be Patrick's laptop, the Chef Server will be [Opscode Hosted Chef](http://www.opscode.com/hosted-chef/), and the first node we create will be a virtual machine that is managed by [Vagrant](http://vagrantup.com).

## Register for Hosted Chef

In this video Patrick will [sign-up for a Hosted Chef account](http://www.opscode.com/hosted-chef/). We will use the free trial which allows you to manage up to 5 nodes for free.  After signing-up and verifying his email address, Patrick will [login to Hosted Chef](https://manage.opscode.com) at [https://manage.opscode.com](https://manage.opscode.com).

<iframe width="560" height="315" src="http://www.youtube.com/embed/7n_mwo9-pIA" frameborder="0" allowfullscreen></iframe>

## Invite Another User to Your Chef Organization

If you're not the only one managing your infrastructure, you'll want to invite you co-workers to join your Chef Organization.  Watch this video to see how to invite another user to join your Chef Organization.

<iframe width="560" height="315" src="http://www.youtube.com/embed/5pwVYvetEW4" frameborder="0" allowfullscreen></iframe>

## Initialize a git Repository

When managing your infrastructure as code, you'll want to store that code in some source code repository.  For this tutorial, we're going to use [git](http://git-scm.com/), a distributed version control system.  The git repository will be publicly hosted on [github](https://github.com/mulderp/learning-chef).

Your workstation will need to have Chef installed.  We verify that Patrick has already installed Chef but if you haven't installed Chef on your workstation yet, you can grab it from [http://www.opscode.com/chef/install/](http://www.opscode.com/chef/install/).

Next we create the Chef repository on the local workstation:

1.  `git clone git@github.com:opscode/chef-repo.git` This will clone the file and directory structure needed to get started with Chef.  Of course, you could also just download a zip or tar.gz of the files from [https://github.com/opscode/chef-repo/downloads](https://github.com/opscode/chef-repo/downloads).
1. `cd chef-repo` Change in to the directory that was just created.
1. `rm -rf .git` Remove the git directory from the cloned repository, we're going to create our own git repo.
1. `git init` - Initialize a new git repository for our infrastructure code.
1. Create a new repository on [github.com](http://github.com) if you'd like to store your repository there.
1. Commit the initial changes and push to your repository.

<iframe width="560" height="315" src="http://www.youtube.com/embed/KdoquSLbZOI" frameborder="0" allowfullscreen></iframe>

## Configure Knife

The Chef server provides three files that must be in the Chef repository and are required when connecting to the Chef server. For Hosted Chef and Private Chef, log on and download the following files:

* `knife.rb` - This configuration file can be downloaded from the [Organizations page](https://manage.opscode.com/organizations).
* `ORGANIZATION-validator.pem` -  This private key can be downloaded from the [Organizations page](https://manage.opscode.com/organizations).
* `USER.pem` - This private key an be downloaded from the [Change Password section of the Account Management page](https://www.opscode.com/account/password).

We'll then move this files into a `.chef` directory in our chef-repo.

<iframe width="560" height="315" src="http://www.youtube.com/embed/6UoRTvpUIZ0" frameborder="0" allowfullscreen></iframe>

## Initialize Vagrant

[Vagrant](http://vagrantup.com) is a tool that makes it super easy to launch and manage virtual machines on your local workstation.  We're going to create a Vagrant-managed virtual machine to act as our Node.  Vagrant manages each virtual machine as a "box."  Opscode makes a number of Vagrant boxes available through it's [bento project on github.com](https://github.com/opscode/bento).

1. Initialize Vagrant by running `vagrant init`
1. Modify the `Vagrantfile` so that it contains (at least) the following:

``` ruby Vagrantfile
Vagrant::Config.run do |config|
  config.vm.box = "opscode-ubuntu-12.04"
  config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/boxes/opscode-ubuntu-12.04.box"
end
```

Finally, run `vagrant up` to launch the Vagrant box.

Be sure to check [the Vagrant website](http://vagrantup.com) for more information about Vagrant.

<iframe width="560" height="315" src="http://www.youtube.com/embed/o9HtZ1nDoTI" frameborder="0" allowfullscreen></iframe>

## First Converge

The first time `vagrant up` is run for this box, it must download the file from Opscode's Amazon S3 file store.  This can take some time so, while it's running, you may want to expand your Vagrant file a bit more.  We'll configure Vagrant to use the `chef_client` provisioner.  You'll find more [information about the chef_client provisioner on the Vagrant website](http://vagrantup.com/v1/docs/provisioners/chef_server.html).

 Here are the relevant settings in our Vagrantfile by the end of the video:

``` ruby Vagrantfile
Vagrant::Config.run do |config|
  config.vm.box = "opscode-ubuntu-12.04"
  config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/boxes/opscode-ubuntu-12.04.box"

  config.vm.provision :chef_client do |chef|
    chef.chef_server_url = "https://api.opscode.com/organizations/fidor"
    chef.validation_key_path = "./.chef/fidor-validator.pem"
    chef.validation_client_name = "fidor-validator"
    chef.node_name = "patrick_vm"
  end
end
```
Be sure to check [the Vagrant website](http://vagrantup.com) for more information about Vagrant.


## Checkpoint

Congratulations!!  You've now got a working Chef development environment including:

1. A free account on Opscode's Hosted Chef.
1. A workstation configured to connect to your Hosted Chef account
1. A git repository for tracking all of your infrastructure code changes
1. A Vagrant-managed virtual machine running on your local workstation
1. The virtual machine is a node managed by Chef

<iframe width="560" height="315" src="http://www.youtube.com/embed/qgPvedOKD1I" frameborder="0" allowfullscreen></iframe>

## What's Next

In [Learning Chef - Part 2](http://nathenharvey.com/blog/2012/12/07/learning-chef-part-2/) we will grab some cookbooks from the [Opscode Community Site](http://community.opscode.com) and use those to start managing our node.

In the meantime, please let us know what you think of this post and these videos!  Drop a note in the comments or reach out to [@nathenharvey](https://twitter.com/nathenharvey) or [@mulpat](http://twitter.com/mulpat) on twitter.


