---
title: create_spark_app_use_sbt
date: 2017-05-23 23:53:03
tags:
---
## What is SBT?
sbt is an open source build tool for Scala and Java projects, similar to Java's Maven or Ant.

Its main features are:

* native support for compiling Scala code and integrating with many Scala test frameworks
* build descriptions written in Scala using a DSL
* dependency management using Ivy (which supports Maven-format repositories)
* continuous compilation, testing, and deployment
* integration with the Scala interpreter for rapid iteration and debugging
* support for mixed Java/Scala projects

sbt is the de facto build tool in the Scala community， used by the Lift web framework and Play Framework.

## Install SBT
Use [Homebrew](https://brew.sh/ "Homebrew") (for Mac)

``
$ brew install sbt
``

or

[Download](http://www.scala-sbt.org/download.html "sbt") ZIP or TGZ package from offcial site, and expand it (for other platforms).

## SBT new command
The below tutorial assumes you`ve installed sbt 0.13.13 or later.

If you’re using sbt 0.13.13 or later, you can use sbt new command to quickly setup a simple Hello world build. Type the following command to the terminal.

``
$ sbt new sbt/scala-seed.g8
....
Minimum Scala build.

name [My Something Project]: hello

Template applied in ./hello
``

When prompted for the project name, type your project name. For example, hello. This will create a new project under a directory named hello.

