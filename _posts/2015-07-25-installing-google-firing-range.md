---
layout: post
title: Installing Google Firing Range
---

Google Firing Range is a "test bed for web application security scanners, providing synthetic, wide coverage for an array of vulnerabilities". It's [available on GitHub](https://github.com/google/firing-range) and also has a [publicly available instance](https://public-firing-range.appspot.com/) on Google AppEngine.

The testbed itself is great, but the project's `README` mention's nothing on how to install it, nor could I find any instructions on other sites. So just in case it will prove useful to you, here's a short guide and a [shell script](https://gist.github.com/ianmuscat/0ae912cb06b078b9f7c9) (I've only tested it on Ubuntu 14.04 LTS)

## Pre-requisites
Before you start, you need to install the Java JRE/JDK. If you need help getting that installed, head over to [this neat article](https://www.digitalocean.com/community/tutorials/how-to-install-java-on-ubuntu-with-apt-get) by Digital Ocean.

You'll also need to install Apache Ant. Apache Ant is a tool that is used for automating software builds.


	sudo apt-get install ant


## Download Firing Range and its depencancies
Once you have the Java JRE/JDK installed, clone the Git repository to a directory on your computer.


	git clone https://github.com/google/firing-range.git

Since Firing Range is meant to run on Google App Engine, you'll need to download and unzip the [Google App Engine SDK for Java](https://cloud.google.com/appengine/downloads) in order to run it.

Next you'll need to set the path to the SDK in `build.xml`. Open up the file in your favourite editor.


	nano firing-range/build.xml

Find the following line and change the location of the SDK to where ever you placed it on your computer.

	<property name="appengine.sdk" location="../.."/>

Next, we'll need to compile the project using Apache Ant. This will create a `war` directory which will contain the compiled application.

	ant compile

That's it! Now we just need to run the built-in server bundled with the Google App Engine SDK.

	appengine-java-sdk-1.9.23/bindev_appserver.sh firing-range/war

You can also choose to change the address and port the server binds to. In the below example I've changed the binging of the web server to bind on all interfaces on port 8080.

	appengine-java-sdk-1.9.23/bindev_appserver.sh --address=0.0.0.0 --port=8080 firing-range/war


## Shell script
Here's a shell script to do this automatically (tested on Ubuntu 14.04 LTS)

<script src="https://gist.github.com/ianmuscat/0ae912cb06b078b9f7c9.js"></script>