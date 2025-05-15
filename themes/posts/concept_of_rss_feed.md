+++
category = "technical"
title = "The Concept of RSS Feed - A Reliable Way for Publishers and Subscribers Model"
date = 2024-05-21
+++

*<strong>Preface:</strong> I have been looking for simple solutions in nearly everything related to computing. A lot of software designed these days is not designed per your requirements but as per companies' profit. Hence, most of these solutions end up sucking your time and energy and need to be replaced by more optimised solutions that would boost your productivity in the right way. RSS Feed is something that I found after searching for solutions related to subscribing to websites or creators without sucking much resources and design that is reliable to the user itself.*

*<strong>Disclaimer:</strong> The views and opinions expressed in this article are solely my own and do not necessarily reflect the official policy or position of any other individual, organization, or entity.*

## Introduction

The Internet is full of software and projects that claim to be useful and productive by design, although very few of them stand the best for user experience. Most of all, it’s important to understand the intentions behind the software and the actual behavior as compared to the promises made by the developers. A lot of them end up being not so useful or irrelevant due to impractical designs or seeking out-of-the-track benefits to compromise with the design and disturb user privacy. Many of them just go unnoticed due to the ignorance of the user base. Most of all, the worst case is compromising the user’s privacy by unnecessary means. Hence, a solution that is designed and engineered in a way that is intended with proper transparency is important for the user’s productivity and privacy. 

The subscriber and publisher model is a good example of this kind of software. Usually, content management platforms require you to create your account, which allows them to keep track of your activity and what you subscribe to. This model is kind of conventional these days and hence, mostly accepted by the huge user base. Although, it has a lot of privacy concerns and allows the owner of the platform to have an advantage of tracking and logging your activities. 

Hence, an RSS Feed is one of the ways that I found helpful in this case due to its rather straightforward design. RSS feed by design respects the privacy of the subscriber and allows a one-place solution for getting notifications and feeds from creators and websites about recent updates. 

## What is an RSS Feed? 

RSS Feed stands for Really Simple Syndication. The concept of RSS Feed is simple: To have an XML file on websites with a standard format that is updated every time an update needs to be published. These feeds are open for the users to read and fetch as per their requirements. The XML files are not very useful to read since it’s just in a markdown format that needs to be manipulated to display in a rather meaningful way. Users can fetch and deserialize these XML files with an RSS Client on their computers. 

Every time an update is made, the XML files are updated and users can receive these files from an RSS endpoint. When a user “subscribes” to an RSS feed, it means that they have a way to keep track of these XML files of that particular website and they can receive the updates made by them. This task of keeping track is done by the RSS Feed Client which keeps fetching the XML files and keeping track of the updates. 

## Design of a RSS Feed 

Subscribers expect to receive updates from websites that they subscribe to and publishers are required to post updates to these subscribers. RSS Feed provides a standard way for publishers to keep a record of the updates with timestamps and content to deliver. 

Subscribers on the other hand keep track of these XML files by fetching them from the endpoint serving it. This way, the publishers don’t know the interested subscribers in subscribing to their content or any third party to keep track of the user’s activity.

This is much different than the subscription model widely implemented. Feeds that are served to the users are derived from the interests that they which were tracked by the user’s activity on their platform. For this purpose, Sign-In serves an important role in disclosing the identity of the user. Platform providers tend to track the activities of these identities to serve feeds related to them. Since they have the data of users, it may be used for any purpose, which violates the privacy of the users.

RSS Feeds are like a broadcasts that subscribers listen to to get notified of the updates served by the publishers. RSS Feeds are derived from the data that was collected from the user but are only limited to what the user has subscribed to and is interested in receiving. 

## Why RSS Feed Strives? 

This model rather respects the user's privacy and shows relevant content that is useful for the readers. This has a positive impact on the user’s productivity since information that is irrelevant is avoided here. The simplicity of the design of this protocol allows developers to create lightweight applications on both the publisher and subscriber side. 

Another major benefit is that the feeds from various platforms are in one place i.e. the client. Users receive updates from hundreds of websites in one place allowing a faster and smoother way to keep track of the updates.

## CLI RSS Client: newsboat

One of the best CLI RSS Clients is `newsboat`. Newsboat is a simple and minimal RSS Feed client that can be installed on the CLI and it’s lightweight, minimal, and configurable. Users can subscribe to RSS Feeds by adding endpoint URLs to the .newsboat/urls files and configuring options in the .newsboat/config file. 

*The Minimalist Book has its own RSS Feed allowing users to receive updates on their RSS Feeds.*
