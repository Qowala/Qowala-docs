# Technical overview \[DRAFT\]

## Which technology to use to allow communication inside Qowala?

### 1. Matrix protocol

[Matrix](https://matrix.org) is an open standard for decentralised persistent communication. In summary, it aims to be the next generation protocol against IRC, XMPP and co.

Several server implementations already exist, among them the official one, [Synapse](https://github.com/matrix-org/synapse) is under Apache license and written in Python.

Furthermore, there are the [Vector](https://vector.im/) clients for web, iOS and Android written by the same team, with nice interface which are also under Apache license.

So, Qowala could base itself on the Matrix technology and Vector clients to have rapidly a working internal communication system. Moreover, as the protocol is entirely open, people using Qowala could easily communicate with other Matrix clients too.

There are Matrix Bridges which exist to allow to communicate between Matrix and IRC and between Matrix and XMPP for example. Qowala could maybe just be some kind of Matrix bot and develop the necessary Matrix Bridges without having to develop a special client.

Little tutorial to write [Matrix Bridges](https://github.com/matrix-org/matrix-appservice-bridge/blob/master/HOWTO.md)

Little tutorial to write [Matrix clients](https://matrix.org/docs/howtos/client-server.html)

**Pros:**

* New protocol which should help to compensate issues with older protocols. See the [comparison](https://matrix.org/docs/guides/faq.html#what-is-the-difference-between-matrix-and-irc).
* Already a quite usable base using modern technologies
* [Matrix's vision for users](https://matrix.org/docs/guides/faq.html#what-does-this-mean-for-users) is the same as Qowala
* Community is growing well. Benefiting exposure from the [Decentralized Web Summit](https://matrix.org/blog/2016/05/24/next-up-the-first-decentralized-web-summit/)

**Cons:**

* Even though Matrix has been initially released in [September 2014](https://matrix.org/docs/guides/faq.html#why-arent-you-doing-this-through-the-ietf-or-w3c-or-3gpp), and is working quite well, we are currently not sure if this protocol will really have success
* Matrix is currently built mainly by VoIP professionals and some other contributors. There is no global organisation like W3C or IETF to ensure this standard will be used worldwide. However, they plan to work with an official standard once they find it mature enough.
* Matrix's technology is modern. However, building tools around it like a bridge requires to learn and investigate in documentation a lot. There is until now no easy tutorial.

### 2. XMPP protocol

The XMPP protocol is mostly used for instant messaging between two users. However, it can also manage groups. The standard is still evolving with [XEP](https://xmpp.org/extensions/) even though it is quite slow. Some recent projects are using XMPP like [Movim](https://movim.eu/) and Salut à Toi, so there may still have opportunities to use it. Furthermore, existing XMPP servers can be useful as identity servers.

**Pros:**

* Mature protocol
* Widespread usage
* Standard protocol supported by IETF

**Cons:**

* Little issues that are today not acceptable anymore like bad management when user is connected on several clients at the same time
* No E2E encryption, only OTR is avaible, so there is some security only in conversations with two people. XEPs to improve that are all [defferred](https://xmpp.org/extensions/xep-0210.html).

### 3. IRC protocol

Simply too old. To mention that there is now a [IRCv3](http://ircv3.net/) initiative which should fix some issues in IRC like notifications.

**Pros:**

* Can manage one-to-one and group conversations

**Cons:**

* No official support for the standard

## What to use to easily integrate lots of social networks and communication services?

### 1. Matrix bridges

Currently there are IRC, Slack, Gitter and other messaging tools for teams that are available [through bridges](https://matrix.org/docs/projects/try-matrix-now.html#application-services). There is also a [Twitter bridge](https://github.com/Half-Shot/matrix-appservice-twitter), but still basic and developed by one developer.

For the moment, only the IRC bridge has been tested. It works well, but is requiring authorization from the IRC side \(maybe just a choice by the bridge developers\).

**Pros:**

* If Qowala develops Matrix bridges for social networks, it would benefit to the whole community so Qowala may benefit of more developers to help.

**Cons:**

* However, building bridges for social networks may be more complicated than other more open networks.

* Overall, with this solution, we will still have to remove some "noise" actions so that Qowala users don't have to bother about integrating services.

### 2. Granary

[This library](https://github.com/snarfed/granary) developed by an IndieWeb member allows to have one REST API for most social networks. Which means for Qowala a consistent interface for most queries following [OpenSocial Social API Server Specifications](https://opensocial.github.io/spec/2.0.1/Social-API-Server.xml#ActivityStreams-Service).

However this is only good to read content, but not to post content.

**Pros:**

* Active project

**Cons:**

* Allows only reading content
* No open source license (no license at all)

### 3. Sockethub

[Sockethub](https://github.com/sockethub/sockethub) is similary to Granary and even allows interactions in both directions.

**Pros:**

* Allows to read and write

**Cons:**

* No open source license (no license at all)
* Doesn't seem very active since one year

### 4. Bridgy

By the same author than Granary, [Bridgy](https://github.com/snarfed/bridgy) allows to pull comments but also to publish them on most social networks.    

**Pros:**

* Most social networks are available
* Still active since 2011

**Cons:**

* No open source license (no license at all)
* Available actions seem limited
* HTML is only API, so requires intermediary step

## What to use to build mobile interfaces?

### 1. Web app
Simply build a website with some optimizations for mobiles.

**Pros:**
* Easy to build
* Works on any platform
* One front-end code for everything

**Cons:**
* Limitations on some mobile platforms:
    - iOS web view is limited on purpose
    - Some features like background notifications don't work

### 2. React Native
Using Facebook's React Native framework allows to build native mobile apps for Android and iOS with one same code. It uses ReactJS as front-end framework.

**Pros:**
* All mobile features available
* One front-end code for everything

**Cons:**
* iOS app still needs a Macbook platform to be developed
* ReactJS framework is quite complex and difficult to master
* ReactJS and React Native are property of Facebook with some limitations included in the license

### 3. Service Workers
Currently work-in-progress, service workers should add some [offline features](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API) to basic web apps.

**Pros:**
* All previous web app pros:
    - Easy to build
    - Works on any platform
    - One front-end code for everything
* Allows background sync and push notifications

**Cons:**
* As still WIP, specifications are changing and mobile isn't fully supported

### 4. Apache Cordova
Apache Cordova is an open source framework for building mobile apps with one codebase. It allows to build hybrid apps which can access more features than web apps on mobiles. However, performance are a lower than native apps.

**Pros:**
* Works on any platform

**Cons:**
* Maybe a little bit complex to develop
* iOS app still needs a Macbook platform to be developed
