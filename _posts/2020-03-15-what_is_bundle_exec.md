---
layout: post
title: What is ‘Bundle exec’ anyway?
date: 2021-03-15
---

There are so many commands that I take for granted, I know I have to run them in order to do things but I don’t actually know what they do. One I use daily is ‘bundle exec’. I knew it had something to do with gems but I couldn't articulate what it actually did, so I looked it up.

**What is bundler used for ?**

* Resolve dependencies and versions for all the gems required in a project
* Store the calculated versions in a file so all the developers have the same gem versions
* Make sure our Ruby code has access to those specific versions of the gems
* We can use it to know which gems have new versions that will still fulfill all the other gems' * version restrictions

**Why use bundler?**

Mostly it is used to ensure that everyone is using the same version of a gem. This is useful because rubygems will tend to activate the newest version we have installed on our system. This can quickly became a problem for the following reasons:

* If I update a gem when working on a project, it will also change for other projects on my machine
* if another developer joins the project, that developer will have to download the gems with the same * versions I used
* new gems version may not be compatible with other gems that my project depends on

This is where Bundler comes into play. All projects that use Bundler will have a Gemfile file specifying the gems and version restrictions we need for each project, and also, after running Bundler, it will have a Gemfile.lock file with the specific gem versions Bundler calculated to make all the gems compatible.

When executing Bundler, it will take care of reading this Gemfile.lock file and will activate the specified versions of each gem. Now, when we require a gem, Ruby will find the gem and it will be the specified version. 

**How to Use Bundler**

We can prefix our commands with `‘bundle exec’`

When we do this, Bundler will load before our script. It will read the Gemfile.lock file, add all the paths for each gem into the $LOAD_PATH array, and then it will execute my_command. That way, our script will have the correct gems activated.
