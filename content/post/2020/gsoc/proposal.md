---
title: "Enabling Reproducible Computing in nteract Play"
date: 2020-05-27T04:40:08+05:30
lastmod: 2020-05-27T04:40:08+05:30
draft: false
keywords: ["nteract", "gsoc", "google summer of code", "2020", "NumFOCUS", "ramantehlan", "raman tehlan"]
description: "This will allow you to share your
public notebooks from Github via a unique URL, and let other people start a session to reproduce your
work."
tags: []
categories: []
author: "Raman Tehlan"

images: ["https://user-images.githubusercontent.com/29037312/82072552-8625ce80-96f5-11ea-951d-a893dc60358d.jpg"]

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: true
toc: true
autoCollapseToc: false
postMetaInFooter: false
hiddenFromHomePage: false
# You can also define another contentCopyright. e.g. contentCopyright: "This is another copyright."
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

<!--more-->

<p align="center">
<img src="https://user-images.githubusercontent.com/29037312/82077369-ebc98900-96fc-11ea-8bc6-ce835bd89593.jpg" />
</p>

<p style="text-align: justify;">
<a href="https://summerofcode.withgoogle.com/projects/#4917324802424832">My project</a> is accepted for <a href="https://summerofcode.withgoogle.com/">GSoC</a> 2020 for the <a href="https://nteract.io/">nteract organization</a> under <a href="https://numfocus.org/">NumFOCUS</a>. If you haven't already read the
announcement post, read it <a href="/blog/post/2020/gsoc/intro">here</a>. I am excited to spend my summer developing nteract play to support
reproducible computing.
</p>


<p style="text-align: justify;">
This post is to describe the proposal briefly. I will cover all the significant steps and topics, some of the
topics will also be explained in sub-posts. Note some steps might be altered during development, but most
will remain the same.
</p>


<p align="center" style="margin-top:50px;margin-bottom:50px">
<img src="https://user-images.githubusercontent.com/29037312/82098839-66a59a80-9723-11ea-8485-4c301d4e4941.gif" width="250"/>
</p>


# What is nteract?

<a href="https://nteract.io/">nteract</a> is an ecosystem of SDKs, applications, and libraries created by the <a href="https://github.com/nteract/">nteract community</a> to help you
and your team make the most of interactive notebooks and REPLs.

- <a href="https://nteract.io/sdk">Core SDK</a> to help you bring the power of notebooks to every application by enabling you to create your
own computing experience.
- A <a href="https://nteract.io/applications">Suite of applications</a> allows you to quickly create and publish notebooks in the cloud and on the
desktop.
- <a href="https://nteract.io/libraries">Libraries</a> to enhance your notebook workflows from end-to-end.

<br>
**What is nteract play?**<br><br>
<a href="https://play.nteract.io/">nteract play</a> is a web application that provides an interactive playground for users to run code samples
against a Binder instance.

<p align="center" style="margin-top:50px;margin-bottom:50px">
<img src="https://user-images.githubusercontent.com/29037312/82072552-8625ce80-96f5-11ea-951d-a893dc60358d.jpg" width="800"/>
</p>

# Proposal

<p style="text-align:justify;">
My proposal is to add support for reproducible computing in nteract play. <b>This will allow you to share your
public notebooks from Github via a unique URL, and let other people start a session to reproduce your
work.</b> This will also allow you and others to make edits and save them back to Github.
</p>

## Why this proposal?
There are many uses cases of reproducible computing, few are mentioned below:

- It will empower researchers to easily showcase their findings without fretting if users can set up the
environment.
- It will save your time when reproducing someone’s work.
- It can be used by professors and teachers to teach their class.
- New students can use it to quickly learn and test different concepts.

# Phases

This project is divided into three phases.

## Phase 1: **Github Integration**

<p style="text-align:justify;">
We take Github's details from the URL query or the menu and use <a href="https://developer.github.com/v3/">GitHub API</a> to perform different
operations like fetching, committing, and so forth. GitHub provides the official library <a href="https://github.com/octokit/rest.js/">octokit/rest.js</a> to interact with Github API.
</p>

### User Authorizing 

<p style="text-align:justify;">
We don’t need to authorize a user to work with public repositories and to test them but is required to commit changes and to fork the repository. We can authorize users using the GitHub OAuth and save the access token in the browser web storage. Web storage has no expiration date, and even if the token gets deleted for some reason, the reauthorization is quick this time, as the app is already allowed by the user.
</p>

```javascript
localStorage.setItem("github-access-token","as2j9xl17kn30jmxc3");
```

### Fetch Data
Using the octokit/rest.js, we will fetch data like directory list, file content, modification date, etc. It will not just make the app content-rich but will also take off the load from the MyBinder Instance.

```javascript
octokit.repos.getContents({
  owner:"username",
  repo:"repo",
  path:"/filepath/file.ipynb",
  ref:"master"
});
```

### Saving Data
When saving data, there can be two cases:

- <i>The user is authentic to commit to the repo</i>. In this case, changes can be easily auto-committed.

- <i>The user is not authentic to commit to the repo</i>. In this case, we will need to fork the repo first or find the already forked repo and then push the changes to auto-commit.

```javascript
octokit.repos.createFork({
  owner:"username",
  repo"repo"
});
```

There can be three cases:

 Action | Commit Quality | Commit Frequency
--------|----------------|----------------
On Change | Low | High
On Run | Medium | Medium
On Save | High | Low

For this project, we will go with `on run`. <b>We will also create a program to take in changes and generate appropriate commit message based on the changes</b>. In the future, we can incorporate the `on save` action and also allow users to pick their commit messages.

## Phase 2: **MyBinder Integration**

<p align="center" >
<img src="https://user-images.githubusercontent.com/29037312/82091141-7964a300-9714-11ea-8435-efa895bdf849.png" width="300"/>
</p>


<p style="text-align:justify;">
We plan to use <a href="https://mybinder.org/">mybinder.org</a> to launch and manage binder instances, running a jupyter-notebook from our Github repo. Once that is up, we use the <a href="https://jupyter-client.readthedocs.io/en/stable/#">jupyter-client</a> to communicate and manage jupyter kernels.
</p>

### Launching

<p style="text-align:justify;">
To  launch  a  binder instance, we  use <a href="https://packages.nteract.io/modules/rx_binder.html">rx-binder</a>,  which  uses mybinder build link[mybinder.org/build/gh/{USER}/{REPO}/{GITREF}] to launch the instance.
</p>

```javascript
const{binder}=require("rx-binder");
binder({repo:"{user}/{repo}"})
```

It returns an object with a token and URL of the remote Jupyter Server.

```json
{
...
"token":"8e_31VblTOO0Nobk0OuFtQ",
"url":"https://notebooks.gesis.org/binder/jupyter/user/ramantehlan-mybinder-play-474q6pqs/"
...
}
```

### Communicating

<p style="text-align:justify">
We use <a href="https://packages.nteract.io/modules/rx_jupyter.html">rx-jupyter</a>, which uses <a href="http://jupyter-api.surge.sh/">Jupyter-API</a> to run queries on remote Jupyter Server. We already have the URL and token, so the API calls look like this:
</p>

```
http://{url}/api/{endpoint}?_={token}
```

EndPoint  | Use
----------|----
/content | Fetch, save, delete, create, rename, list files and folders.
/sessions | Delete, create, rename, list sessions.
/kernels | Start, kill, interrupt, restart kernels.
/kernelspecs | Get kernel specs./configGet or update configuration of session.
/terminals | Create, get and delete terminal.
/status | Get status of the server.

### Executing

<a href="https://jupyter-client.readthedocs.io/en/stable/messaging.html">Messaging in Jupyter</a> uses sockets to execute commands and exchange input and output. We use <a href="https://packages.nteract.io/modules/messaging.html">@nteract/messaging</a> on the frontend to work with sockets to execute the command and fetch the output.

```javascript
constmessage=createMessage("inspect_request",{
  code:"string.for",
  cursor_pos:10,
  detail_level:1
});
```

## Phase 3: **UI/UX Integration**

To make the nteract-play application more interactive, we can create new UI/UX by introducing the following new/improved components and functionality.

- FileExplorer<br>
List all the files in the repo, which on click is visible on the editor or the viewer.
- Viewer<br>
It is to display different file types with syntax highlighting.
- Editor<br>
To edit notebooks using the nteract environment.

- Console<br>
It is placed on the bottom of the page as users are familiar with this UX, and we can console more information about binder and notebook activities.
- Notification<br>
It is to notify about the connection failure or success, or other important messages for the user.
- Loading<br>
To give a visual confirmation on processing something or loading something.

The idea is to give users a smooth and playful experience on the application, so we can also introduce more components as per requirement during the development of this project.

# Conclusion

This proposal is projected to take 3 months or so to complete, and as mentioned above, a lot of steps anddetails will change during the development. I will write a blog at the end of the GSoC period to include all the changes done in the development.

# Acknowledgement

- Hero Image and “Understanding Nteract” by <a href="https://twitter.com/fabric_8">@fabric_8</a>

