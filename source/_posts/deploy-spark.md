---
title: deploy_spark
date: 2017-07-27 13:25:51
tags:
 - spark
 - scala
 - java
---
This is a quick guide to installing, Ruby on Rails, Scala, and Spark on Linux (Ubuntu in this post).

<!-- more -->

# Set Up Ruby on Rails Development Environment
We will be setting up a Ruby on Rails development environment on Ubuntu 16.04 Xenial Xerus, including rbenv, ruby, rails, MySql, MongoDB. 

## Install Ruby
The first step is to install the dependencies for Ruby.
``` shell
sudo apt-get update
sudo apt-get install git-core curl zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev nodejs
```
Next, we are going to install ruby using a ruby version manager, rbenv or rvm. Most people prefer using rbenv these days, but if you're familiar with rvm you can follow those steps as well. I recommend using rbenv or rvm instead of directly installing from source.

### Using rbenv
Installing with rbenv is a simple two step process. First you install rbenv, and then ruby-build:
``` shell
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(rbenv init -)"' >> ~/.bashrc
exec $SHELL

git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
echo 'export PATH="$HOME/.rbenv/plugins/ruby-build/bin:$PATH"' >> ~/.bashrc
exec $SHELL

rbenv install 2.4.0
rbenv global 2.4.0
ruby -v
```
For more usage of rbenv, please go to [rbenv](https://github.com/rbenv/rbenv "rbenv").

### Using rvm
The installation for rvm is pretty simple:
```shell
sudo apt-get install libgdbm-dev libncurses5-dev automake libtool bison libffi-dev
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable
source ~/.rvm/scripts/rvm
rvm install 2.4.0
rvm use 2.4.0 --default
ruby -v
```
For more usage of rvm, please go to [rvm](https://rvm.io/ "rvm").

## Install Bundler
The last step is to install bundler:
``` shell
gem install bundler
```
Note: if you use rbenv, you need to run ```rehash``` after installing bundler.

# Set Up Production Server for Rails App