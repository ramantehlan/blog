---
title: "Notes on System Design"
date: 2023-08-13T23:54:30+05:30
lastmod: 2023-08-13T23:54:30+05:30
draft: true
keywords: []
description: ""
tags: ["system-design"]
categories: ["system-design"]
author: "Raman Tehlan"

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: false
toc: true
autoCollapseToc: false
postMetaInFooter: false
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
contentCopyright: false
reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false

# You unlisted posts you might want not want the header or footer to show
hideHeaderAndFooter: false

# You can enable or disable out-of-date content warning for individual post.
# Comment this out to use the global config.
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""

---

Here are some notes on system design. I will keep updating this post as I learn more about system design.

# Requirement Gathering

The first step is to understand what is it that you are building, who are you building it for, and how are they going to use it? 

The best way to do the requirement gathering is by asking questions. Here are some questions that you can ask:

- What is the problem that we are trying to solve?
- What feature can we build to solve this problem?
- Who are we building this feature for?
- How are they going to use this feature?  
- How many users are going to use this feature?

Based on the questions above, you can start building the requirements. There are two types of requirements:

- Functional Requirements
- Non-Functional Requirements

## Functional Requirements

Functional requirements are the features that you are going to build. Different features will have different requirements. For example, if you are building a chat application, you will need to build a feature that allows users to send messages to each other. If you are building a social media application, you will need to build a feature that allows users to post content on the platform.

## Non-Functional Requirements

Non-Functional Requirements are the requirements expected from the system by default. Like, the system should be available 24/7, the system should be able to handle 1000 requests per second, etc.


### Back-of-the-envelope calculation

Before we start designing, we should answer the following questions:

- How many users are going to use this feature?
    - Let's say you have 10M daily active users. Assume they are going to use this feature 10 times a day on average. That means you will have 100M requests per day. This means you will have 100M/24/60/60 = 1157 requests per second. 

- Where are the users located?
    - This helps you decide the location of your servers. If your users are located in the US, you can have your servers in the US. If your users are located in India, you can have your servers in India.


# Design

Once you have the requirements, you can start designing the system. There are multiple design phases:

- High-Level Design
- API Design
- Low-Level Design
- Database Design

## High-Level Design

High-Level Design is the first step in the design process. It is used to define the architecture of the system. It is also used to define the components of the system.

This is usually deciding the services or components that you are going to build or technologies you are going to use. It's going to evolve as you go through the design process.

The choices you make in this step depend on multiple factors like the requirements, the team, the budget, etc. Here are some important things to consider
 
- How are different components going to communicate with each other?  
  - REST API
  - Messaging Queue
  - RPC
  - WebSockets
  - Dumping data to a file and reading it from another component
  - etc.
- Database type: There are many kinds of databases you can choose from based on the requirements.
  - NoSQL
  - SQL
  - Key-Value
  - Graph
  - Time-Series
  - In-Memory Databases
- Read vs Write ratio
  - If the read-to-write ratio is high, you can use a caching layer to improve the performance or you can read from secondary databases. 
  - If the write-to-read ratio is high, you can use a database that is optimized for writing.
- Do you need a caching layer? 
  - If you have a high read-to-write ratio, and the frequency of reads is high, you can use a caching layer to improve the performance.

## API Design

API Design is the second step in the design process. It is used to define the API of the system. It is also used to define the endpoints of the system. We also define the request and response format in this step. We also define other aspects of the API like authentication, authorization, language etc.

## Low-Level Design

This is the third step in the design process. It is used to define the internal architecture of the system. It is also used to define the internal components of the system. We also define the internal communication between the components in this step.

The Algorithm which we pick has a huge impact on the performance of the system. We should pick the algorithm based on the requirements. Having a deep understanding of the algorithm is very important, as it's going to help you pick the right algorithm for the right problem. Every algorithm has a trade-off, some have better time complexity, some have better space complexity, some are better for small data, some are better for large data, some are better for sorted data, some are better for unsorted data, etc.

## Database Design

This is the fourth step in the design process. It is used to define the database schema of the system. It is also used to define the tables of the system. We also define the relationships between the tables in this step.

Just like an algorithm, a database schema has trade-offs too, if insert into a database that requires locking, it will be more expensive than the one which doesn't. You also need to consider that eventually, your schema will evolve, so you need to pick a schema that is easy to enhance.

There are 3 steps to designing a database schema:

### Conceptual Design
It is a high-level design of different tables/collections. It is used to define different dependencies.

### Logical Design
It is a mid-level design, where we decide the rough schema of data to be stored in them, keys to link them, etc. If you are going to have a nested list(requires locking on update) or a separate row/document for each item(requires more space), etc.

### Physical Design
It is a low-level design, where we decide the exact schema of data to be stored in them, their datatypes, etc. It might make a huge difference if the key is an int32 or int64, or if the value is a string or a byte array. It also sets the limitations of the data point, like min and max values you can store in them, or the timezone you pick. 

You can also define the indexes in this step. Based on the access policy, you can define the indexes. If you are going to access the data based on a key, you can define a primary key. If you are going to access the data based on a range, you can define a secondary index. If you are going to access the data based on a combination of keys, you can define a composite index.

# Scale 

Scale is done based on the expected load, in terms of QPS(Queries Per Second), number of connections, etc. 

# Availability

Availability is done based on where your users are located and put the servers or caching layer near them, in their zones. Then you also gotta have backup servers in case the primary servers go down, having multiple zones also helps with this. 

# Conclusion

System Design is a vast concept, and it's not possible to cover everything in a single article. There are many more things to consider, like security, monitoring, backups, reconciliation of different components, etc. This is just a high-level overview of the system design process.

Also note, this is not the only way to design a system, there are many other ways to design a system. This is just one of the ways to design a system. 

I will try to come back and update this blog as I discover more important concepts, in the mean time, you also continue reading more about it, and do share if you find something important.

# References

- [Microservices] (https://microservices.io/)
- [System Design Resources](https://github.com/InterviewReady/system-design-resources)
