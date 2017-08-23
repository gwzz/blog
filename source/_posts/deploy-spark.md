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

#Install MongoDB


MongoDB provides officially supported packages in their own repository. This repository contains the following packages:

Package Name	Description
mongodb-org	A metapackage that will automatically install the four component packages listed below.
mongodb-org-server	Contains the mongod daemon and associated configuration and init scripts.
mongodb-org-mongos	Contains the mongos daemon.
mongodb-org-shell	Contains the mongo shell.
mongodb-org-tools	Contains the following MongoDB tools: mongoimport bsondump, mongodump, mongoexport, mongofiles, mongooplog, mongoperf, mongorestore, mongostat, and mongotop.
The mongodb-org-server package provides an initialization script that starts mongod with the /etc/mongod.conf configuration file.

See Run MongoDB Community Edition for details on using this initialization script.

These packages conflict with the mongodb, mongodb-server, and mongodb-clients packages provided by Ubuntu.

The default /etc/mongod.conf configuration file supplied by the packages have bind_ip set to 127.0.0.1 by default. Modify this setting as needed for your environment before initializing a replica set.

Install MongoDB Community Edition

NOTE
To install a different version of MongoDB, please refer to that version’s documentation. For example, see version 3.2.
MongoDB only provides packages for 64-bit LTS (long-term support) Ubuntu releases. For example, 12.04 LTS (precise), 14.04 LTS (trusty), 16.04 LTS (xenial), and so on. These packages may work with other Ubuntu releases, however, they are not supported.

1
Import the public key used by the package management system.

The Ubuntu package management tools (i.e. dpkg and apt) ensure package consistency and authenticity by requiring that distributors sign packages with GPG keys. Issue the following command to import the MongoDB public GPG Key:

Copy
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
2
Create a list file for MongoDB.

Create the /etc/apt/sources.list.d/mongodb-org-3.4.list list file using the command appropriate for your version of Ubuntu:

Ubuntu 12.04
Copy
echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu precise/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
Ubuntu 14.04
Copy
echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
Ubuntu 16.04
Copy
echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
3
Reload local package database.

Issue the following command to reload the local package database:

sudo apt-get update
4
Install the MongoDB packages.

Install the latest stable version of MongoDB.

Issue the following command:

sudo apt-get install -y mongodb-org
Run MongoDB Community Edition

Most Unix-like operating systems limit the system resources that a session may use. These limits may negatively impact MongoDB operation. See UNIX ulimit Settings for more information.

The MongoDB instance stores its data files in /var/lib/mongodb and its log files in /var/log/mongodb by default, and runs using the mongodb user account. You can specify alternate log and data file directories in /etc/mongod.conf. See systemLog.path and storage.dbPath for additional information.

If you change the user that runs the MongoDB process, you must modify the access control rights to the /var/lib/mongodb and /var/log/mongodb directories to give this user access to these directories.

1
Start MongoDB.

Issue the following command to start mongod:

sudo service mongod start
2
Verify that MongoDB has started successfully

Verify that the mongod process has started successfully by checking the contents of the log file at /var/log/mongodb/mongod.log for a line reading

[initandlisten] waiting for connections on port <port>
where <port> is the port configured in /etc/mongod.conf, 27017 by default.

3
Stop MongoDB.

As needed, you can stop the mongod process by issuing the following command:

sudo service mongod stop
4
Restart MongoDB.

Issue the following command to restart mongod:

sudo service mongod restart
5
Begin using MongoDB.

To help you start using MongoDB, MongoDB provides Getting Started Guides in various driver editions. See Getting Started for the available editions.

Before deploying MongoDB in a production environment, consider the Production Notes document.

Later, to stop MongoDB, press Control+C in the terminal where the mongod instance is running.

Uninstall MongoDB Community Edition

To completely remove MongoDB from a system, you must remove the MongoDB applications themselves, the configuration files, and any directories containing data and logs. The following section guides you through the necessary steps.

WARNING
This process will completely remove MongoDB, its configuration, and all databases. This process is not reversible, so ensure that all of your configuration and data is backed up before proceeding.
1
Stop MongoDB.

Stop the mongod process by issuing the following command:

sudo service mongod stop
2
Remove Packages.

Remove any MongoDB packages that you had previously installed.

sudo apt-get purge mongodb-org*
3
Remove Data Directories.

Remove MongoDB databases and log files.

sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongodb



# Set Up Production Server for Rails App