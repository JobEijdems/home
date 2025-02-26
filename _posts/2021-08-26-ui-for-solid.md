---
layout: post
title: "Designing a UI for a Personal Online Datastore"
author: joep
permalink: /blog/ui-for-pods/
---

In this article, we'll discuss an open source, creative commons set of UI designs for a web-based personal data store.

- Click through [the demo](https://www.figma.com/proto/wkc2XEA6Lddai8n4PUU83C/Solidstarter-Prototype?page-id=327%3A0&node-id=335%3A32985&viewport=289%2C241%2C0.04754795879125595&scaling=scale-down) on figma
- View the [style book](https://zeroheight.com/756e7c07f/p/919ed8-solid-ui-kit) on ZeroHeight
- Check out the [Github Repository](https://github.com/ontola/solid-ui-designs), containing the source files

![solid-1](/img/solid-ui/solid-1.jpg)

## Why we need Personal Online Datastores

30 Years ago, the first website was created by Tim Berners-Lee.
The web was designed to be decentralized, where people would have their own servers to share their thoughts on an open internet.
But today, our web has become more centralized than every before.
A few large tech companies control most of our personal data.
Using cloud applications enabled us to access our data from every machine, but it took away a great deal of control.
Moving data from one app to the other is often difficult (or impossible), as many cloud apps have a tight integration between client and server.
For example, we can only view our facebook posts using official Facebook apps.
On the other hand, standards like e-mail, RSS, and HTML allow users to choose how they view and edit their data - we can pick our own e-mail apps, RSS readers and our own web browsers.
Wouldn't it be awesome if we could do the same thing with our social media posts, our chat messages, our todo apps and more?

One approach to solve this problem, is having a _personal online data store_, a Pod.
This is a computer that is always online, and contains your personal data.
It is similar to a service such as Dropbox or Google Drive, but it does a bit more.
Instead of only dealing with files, it deals with _structured standardized data_.
This enables a higher degree of interoperability, which means it becomes easier for app developers to re-use data.
It also hosts your online identity, stores notifications and more.

One notable project that aims to provide such a standard, is Solid.
This project was started by Tim Berners-Lee himself.
At this time, the specification is being formalized and various implementations are being worked on (such as our own [DexPod Server](https://gitlab.com/ontola/dexpod), or the [Solid-Community-Server](https://github.com/solid/community-server)).
The majority of the Solid community is focused on making all of this work, which mostly means getting the technology and the specification in good shape.
Another Pod project is [Atomic Data](https://atomicdata.dev), which is what I've been working on for the past year.
Both of these projects share the same goal: giving people more control over their data.
Because

## Designing a user interface for Pods

How would a Pod look like? How would you interact with it? What kind of UI challenges and opportunities does a Pod present?
We've partnered up with studio [Jager & Prooi](https://jagerenprooi.nl/) to answer these questions and design a user interface for Pods.
Thanks to the [SIDN Fonds](https://www.sidnfonds.nl/nieuws/techneuten-en-ontwerpers-bundelen-krachten-8-projecten-van-start) for funding this project.

We started our project off by interviewing two groups: Solid developers, and potential early adapters.
That way, we'd have a good grasp on technical opportunities and limitations, and what aspects of the UI would be most important for making the first group of users happy.

We realized that designing a Pod would pose an interesting challenge, even for experienced designers.
A Pod is not just one of many apps - it is a place where many apps could run.
It is similar to an Operating System, such as Windows or iOS: where you launch and manage apps, manage your data and manage your system.
This means it needs:

- **a homescreen** from which you can open apps and view activities
- a way to **browse through your files**, like a file manager where you can edit, organize and delete things
- a tool to **search** through your data
- a **settings app** to manage the hardware and UI
- a **notification tray** or a different way to view incoming changes and alerts
- **persistent UI elements** to quickly open search / notifications / settings
- a **way to open files with various different apps** (e.g. open a PDF in Adobe or a Browser).

These are the things that we've learned to expect from operating systems - these are also present in Windows, iOS and others.
But Pods are different for two reasons:

1. Pods are _always_ connected to the internet, which means that they can be places that others can find information
1. Pods use _structured data_ instead of _binary data_ (regular files on your computer), which means that you get new features to manage information

These differences result in new things that you might want a Pod operating system to achieve:

- **Manage external access to data**. In a Pod, you can allow other to access files without actually sending it to them. Your Pod is a server, so it's connected to the internet, which means that (if you want) others can collaborate on or view your data, too. This needs to be managed, which is something that is not actually common in other operating systems.
- **Version control / history control**. Storing structured data makes it easier to actually save various version, which means that user can undo their mistakes and see who changed what over time.
- **Structured Search**. In a regular operating system, we could search for filenames, but in a Pod, we can search through the data itself. This means that we can use the global search feature to find Todo's, appointments, playlists and more.
- **Manage personal information**. Since Pods are inherently _personal_, they are great for storing data about yourself. This includes data that you'd share publicly on your linkedin profile, or medical data that you'd want to keep private, but do want to have managed somewhere.

To keep the scope of this project manageable, we decided to focus on Home, Personal Information Management, Sharing, File Exploring and Search.

![personal data management](/img/solid-ui/solid-2.jpg)

**[Click through the demo](https://www.figma.com/proto/wkc2XEA6Lddai8n4PUU83C/Solidstarter-Prototype?page-id=327%3A0&node-id=335%3A32985&viewport=289%2C241%2C0.04754795879125595&scaling=scale-down)** to see how it turned out!
And feel free to use these designs in your own apps - we're sharing the [source files on Github](https://github.com/ontola/solid-ui-designs) under a CC-BY license for specifically that reason.
