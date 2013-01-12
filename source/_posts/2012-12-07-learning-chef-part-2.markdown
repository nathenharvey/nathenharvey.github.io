---
layout: post
title: "Learning Chef - Part 2"
date: 2012-12-07 13:18
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
 - mongodb
 - apache
 - passenger
---

## Learning Chef Series

* [Part 1](http://nathenharvey.com/blog/2012/12/06/learning-chef-part-1/) - Introduce the project, configure workstation, and register a node with hosted Chef
* [Part 2](http://nathenharvey.com/blog/2012/12/07/learning-chef-part-2/) - Download cookbooks from the community site, add MongoDB, Apache, and Passenger to our node
* [Part 3](http://nathenharvey.com/blog/2012/12/14/learning-chef-part-3/) - Start writing a cookbook to deploy our application
* [Part 4](http://nathenharvey.com/blog/2012/12/19/learning-chef-part-4/) - Finish the application deploy, introduce roles

Part 2 of our Learning Chef tutorial was run as a Google+ Hangout that was streamed to YouTube.

## Review of Part 1

* [Read the blog post for Part 1](http://nathenharvey.com/blog/2012/12/06/learning-chef-part-1/)

<iframe width="420" height="315" src="http://www.youtube.com/embed/E4ibkS1LbPk" frameborder="0" allowfullscreen></iframe>

## Discuss Chef Solo vs. Chef Server
Chef Solo allows you to run Chef Cookbooks without a Chef Server.  There are a number of things that you don't get when using Chef Solo.  Check the [Chef Solo page on the wiki](http://wiki.opscode.com/display/chef/Chef+Solo) for more information.

<iframe width="420" height="315" src="http://www.youtube.com/embed/QwiPbEXhe24" frameborder="0" allowfullscreen></iframe>

<!-- more --> 

## Download a number of cookbooks from the community site

Now that we've got our Vagrant instance connected to Chef Server we can start managing the configuration of the VM with Chef.  We'll download a number of cookbooks from the [Community Site](http://community.opscode.com) and extract them into our Chef repository.

Here are the commands we ran to download each cookbook:

1. `knife cookbook site download omnibus_updater`
1. `knife cookbook site download apache2`
1. `knife cookbook site download apt`
1. `knife cookbook site download build-essential`
1. `knife cookbook site download mongodb`
1. `knife cookbook site download omnibus_updater`
1. `knife cookbook site download passenger_apache2`

After downloading each cookbook, extract it to the cookbooks directory of the chef-repo:

`tar xzvf COOKBOOK_NAME.tar.gz -C cookbooks`

Finally, upload each cookbook to the Hosted Chef server:

`knife cookbook upload COOKBOOK_NAME`

This video shows the process for grabbing the `omnibus_updater` cookbook off of the [community site](http://community.opscode.com).

1. `knife cookbook site download omnibus_updater`
1. `tar xzvf omnibus_updater-0.0.5.tar.gz -C cookbooks`
1. `knife cookbook upload omnibus_updater`

<iframe width="560" height="315" src="http://www.youtube.com/embed/d1npGSBgyrs" frameborder="0" allowfullscreen></iframe>

This video shows the process for grabbing the `mongodb` cookbook, and it's dependency, the `apt` cookbook, off of the community site.

1. `knife cookbook site download mongodb`
1. `knife cookbook site download apt`
1. `tar xzvf mongodb-0.11.0.tar.gz -C cookbooks`
1. `tar xzvf apt-1.5.0.tar.gz -C cookbooks`
1. `knife cookbook upload apt`
1. `knife cookbook upload mongodb`

<iframe width="420" height="315" src="http://www.youtube.com/embed/wyLtF261a6A" frameborder="0" allowfullscreen></iframe>

## Update the run list for our node

There are a number of ways to update a node's run list.  You can do so in a web browser while logged in to Hosted Chef or you can do so using knife.

In our session, we first used the Opscode Chef management interface.

<iframe width="420" height="315" src="http://www.youtube.com/embed/Q0BgCLSqJJU" frameborder="0" allowfullscreen></iframe>

You can also update your node's run list using knife.  In this video, we'll use knife to add mongodb to the node's run list.

1. `export EDITOR=vim` - knife uses the `EDITOR` environment variable to determine which application to launch when you edit the node.
1. Add `"recipe[mongodb]"` to the `run_list`
1. Run `chef-client` on the node using the `vagrant provision` command.

<iframe width="420" height="315" src="http://www.youtube.com/embed/5xU3A-SvdJc" frameborder="0" allowfullscreen></iframe>

We'll follow the same steps to add `passenger_apache2` to our run list.

1. `knife cookbook site download passenger_apache2`
1. `tar xzvf passenger_apache2-1.0.0.tar.gz -C cookbooks`
1. `knife cookbook site download apache2`
1. `tar xzvf apache2-1.3.2.tar.gz -C cookbooks`
1. `knife cookbook upload apache2`
1. `knife cookbook site download build-essential`
1. `tar xzvf build-essential-1.2.0.tar.gz -C cookbooks`
1. `knife cookbook upload build-essential`
1. `knife cookbook upload passenger_apache2`

We will then add `passenger_apache2` to the run list using `knife node edit patrick_vm`.  When we run `vagrant provision`, we'll hit an error that requires us to add `apt` to the run list prior to `passenger_apache2`.  

By the end of this video, the run list should look like:

```
"run_list" : [
    "recipe[apt]",
    "recipe[omnibus_updater]",
    "recipe[mongodb]",
    "recipe[passenger_apache2]"
]
```
<iframe width="420" height="315" src="http://www.youtube.com/embed/0-Bid-eiJHY" frameborder="0" allowfullscreen></iframe>

## Add port forwarding to the Vagrant instance

Finally, we updated the Vagrant configuration so that port 80 on the VM is forwarded to port 8080.  This was done by adding `config.vm.forward_port 80, 8080` to our Vagrantfile.  Here's the full Vagrantfile:

``` ruby Vagrantfile
Vagrant::Config.run do |config|
  config.vm.box = "opscode-ubuntu-12.04"
  config.vm.box_url = "https://opscode-vm.s3.amazonaws.com/vagrant/boxes/opscode-ubuntu-12.04.box"
  config.vm.forward_port 80, 8080

  config.vm.provision :chef_client do |chef|
    chef.chef_server_url = "https://api.opscode.com/organizations/fidor"
    chef.validation_key_path = "./.chef/fidor-validator.pem"
    chef.validation_client_name = "fidor-validator"
    chef.node_name = "patrick_vm"
  end
end
```
<iframe width="420" height="315" src="http://www.youtube.com/embed/ag0w_IqkgBI" frameborder="0" allowfullscreen></iframe>

## Summarizing Part 2

We now have the following in place:

* A node managed by Chef - our Vagrant VM
* The latest version of Chef (10.16.2) is running on the node
* Six cookbooks added to our local workstation
* Six cookbooks added to our Hosted Chef organization
* The run list for our node was updated
* The node has a working MongoDB database running
* The node has Apache and Passenger running
* Port Forwarding is configured on the Vagrant VM

<iframe width="420" height="315" src="http://www.youtube.com/embed/7Cxfv40w7wQ" frameborder="0" allowfullscreen></iframe>

## What's Next

In [Learning Chef - Part 3](http://nathenharvey.com/blog/2012/12/14/learning-chef-part-3/) we install some more cookbooks and start writing our own cookbook to deploy a sample Rails application.

In the meantime, please let us know what you think of this post and these videos!  Drop a note in the comments or reach out to [@nathenharvey](https://twitter.com/nathenharvey) or [@mulpat](http://twitter.com/mulpat) on twitter.

