---
title: "GSoC 2020: Final Report of nteract play"
date: 2020-08-20T22:53:30+05:30
lastmod: 2020-08-20T22:53:30+05:30
draft: true
keywords: ["GSOC", "Raman Tehlan", "nteract", "nteract web", "nteract play", "ramantehlan", "nteract SDK", "ramantehlan"]
description: "Final report on the GSoC 2020 project with nteract and NumFOCUS."
tags: []
categories: []
author: "Raman Tehlan"

images: ["https://images.unsplash.com/photo-1531262951893-05a0ffb31b27?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80"]

# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: true
toc: true
autoCollapseToc: false
postMetaInFooter: true
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
<img src="https://images.unsplash.com/photo-1531262951893-05a0ffb31b27?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1350&q=80" />
</p>

On 31st August 2020, the 3rd and final phase of Google Summer of Code will end. I had a really good time working with nteract this summer, and it turned out to be a unique experience. This blog is my final report on the project, and I will talk about the implementation, the source etc.

# Project

**Title:** Reproducible computing with nteract play

**Organization:** <a href="https://numfocus.org/">NumFOCUS</a>

**Project:** <a href="http://nteract.io/">nteract</a>

**Abstract:** This project aims to support reproducible computing using nteract and Binder—the ability to start an interactive session via a unique URL, with content provided by any version control system and executed in a remote environment. To begin with, Github API can be used to fetch and save content, but the scope of the project can be adjusted to deal with different VCS. The Github repo can be launched on a binder instance, and the code samples can run on it.

## **Implementation**
In my <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/intro/">proposal</a>, I divided my work into 3 phases. However, when I started working on the application, I began with UI/UX Integration. 

- Github Integration
- MyBinder Integration
- UI/UX Integration

### 1st Month

- Before starting to write code, I created the moke ups of the application in Figma and shared it with Safia. I also made a logical flow for the Github Integration. Initially, I also spent some time in sharping my React and other skills. 

- One can say it was a slow start, but I believe in "Think twice and code once". So when I started working, things were moving fast. 

- I started by developing a component inventory in React from the mockups and tested it in a storybook in `UI-web` repository. Right after creating new components, I integrated them with the `nteract/web` application. 
<img src="https://user-images.githubusercontent.com/29037312/91600198-2d690180-e985-11ea-9bbb-63be300a1ee8.png" />

- Along with this, I was also testing Github integration features like fetching content, folders etc. and was adding them to the application. I completed the OAuth server and launched it via vercel and successfully implemented the Github OAuth.

- I also added a Landing page and Authentication page to the application.
<img src="https://user-images.githubusercontent.com/29037312/91600338-6bfebc00-e985-11ea-8875-74e1d4de4688.png" />

### 2nd Month

- I had half time this month due to exams, but because I made extra efforts(Worked on the weekends) in the first month, I was able to catch up. I added the file explorer component to the application. I completed the last part of Github integration, which was saving back the changes.

### 3rd Month

- I added Notification and Notebook component, which marks the completion of UI/UX integration. I did the code cleaning and formatting, added documentation and comments. I fixed the routing issues and some other minor issues. I also added console logs. Launched and connected to the MyBinder server.

You can read more about my journey and implementation in the following blogs.

- <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/intro/">The open-source summer of 2020</a>
- <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/proposal/">Enabling Reproducible computing in nteract play</a> **`Proposal`**
- <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/progress-report-1/">What's it like to strategize and build the sails for nteract-play</a> **`Progress Report 1`**
- <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/progress-report-2/">1st Evaluation of nteract-play</a> **`1st Evaluation`** 
- <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/progress-report-3/">2nd Evaluation of nteract-play</a> **`2nd Evaluation`**
- <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/demystifying-nteract-sdk/">Demystifying nteract SDK</a>
- <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/final-report/">GSoC 2020: Final report of nteract play</a> **`Final Report`**


## **Source Code**

The source code of the work I did this summer can be found in the following repositories. 

- [nteract/web](https://github.com/nteract/nteract/tree/main/applications/web)
- [play-oauth-server](https://github.com/nteract/play-oauth-server)
- [ui-web](https://github.com/nteract/ui-web)

Further, you can look into the raised PRs to see the detailed implementation of the work.

### PRs Before coding period

- [[nteract/web] Alpha webapp layout](https://github.com/nteract/nteract/pull/4966)

### PRs During coding period

- [[nteract/web] New layout and OAuth in @nteract/web](https://github.com/nteract/nteract/pull/5167)
- [[nteract/web] Save/upload to Github and other improvements](https://github.com/nteract/nteract/pull/5240)
- [[nteract/web] Add project details in main and landing page](https://github.com/nteract/nteract/pull/5246)
- [[nteract/web] Add language detection for editor and move functions out of main file](https://github.com/nteract/nteract/pull/5249)
- [[nteract/web] Replace routes with query](https://github.com/nteract/nteract/pull/5251)
- [[nteract/web] Clean Code | Fix Formatting](https://github.com/nteract/nteract/pull/5261)
- [[nteract/web] Add notebook component and wrap up for beta and GSoC](https://github.com/nteract/nteract/pull/5257) `not merged yet`


## **Result**
I have talked about how the implementation of the project and the journey. Now let's talk about the final shape of the project. Below is the working of the application.


### UI/UX Integration

- [x] Layout
- [x] BinderMenu
- [x] Input
- [x] Menu
- [x] Button 
- [x] Avatar
- [x] Dialog
- [x] Landing Page
- [x] Auth page
- [x] Editor
- [x] Console
- [x] FileExplorer
- [x] Notification
- [x] Notebook rendering.

### Github Integration

- [x] Complete authentication
- [x] Fetch user's public info
- [x] Fetch public files and folders 
- [x] List and create a fork for repo
- [x] Save back changes to the repo or the fork 

### MyBinder Integration
- [x] Launch MyBinder instance on start.
- [x] Communicate with JupyterServer. Fetch info like sessions etc.
- [x] Execute the command on MyBinder instance
- [x] Fetch content from Github and not jupyter server.
- [x] Save back changes done to the notebook.

<img src="https://user-images.githubusercontent.com/29037312/91562211-722b7300-e95a-11ea-8fd0-b8340c788f0e.gif" />

## **Future Scope**

<p style="text-align:justify;">
Just like any application or product, there will always be more that can be done with nteract play. One of the most ambitious possibility is to integrate nteract play/web with nteract desktop, which will make it super easy to have an interactive environment connected with a remote server.
</p>

Some of the more practical things that can be done shortly are given below. 

- **Pending Tasks**
  - Upload OAuth server from the official account.
  - Update OAuth application in GitHub to point to nteract play, instead of localhost.

- **Bugs**
  - FileExplorer gets reset, fix that by storing the state to redux.
  - Handle “Github update too soon” error, which happens when we try to save changes again within ~2 minutes of saving.

- **Features**
  - We can use iterm.js or similar library to add terminal support in the console.
  - Click to copy sharable link button.
  - Add star repo button.
  - Add option to strip output from the notebook.

- **Improvements**
  - Add state verification code to Github OAuth.
  - Add a loading experience.
  - Replace local component store with the redux store.


# Acknowledgement

<p style="text-align:justify;">
I want to thank my mentor Safia(<a href="https://twitter.com/captainsafia">@captionsafia</a>). It was a pleasure working with her. I got to learn a lot from her in the past three months. She helped me throughout the coding period, and that kept things on track. Her feedbacks in each evaluation were very constructive, and I will always use them as an anchor in my developer journey. 
</p>

<p style="text-align:justify;">
I also want to thank the awesome nteract community for the platform and all the projects in it. Open source is thriving because of organisations like this. 
</p>

<p style="text-align:justify;">
I am thankful to google for creating and continuing an internship program like GSoC. I feel such programs can boost the skills of those students about to enter the industry and get familiar with FOSS culture early.
</p>

<p style="text-align:justify;">
In the end, I want to thank all the open-source libraries I used in making this application. I respect and appreciate all the hard work people have done to make the source code of so many excellent libraries for others to use.
</p>

# Conslusion


<p style="text-align:justify;">
nteract is an incredible ecosystem and community to be a part. I am glad I picked it as my organization under GSoC. I also feel great that I got to work on the nteract play project and push it towards the finish line. We will be releasing it as a public beta soon. I can't wait to see it online and use it for my projects, and hopefully, many people will find it useful too.
</p>


> Hero image by [Artur Aldyrkhanov](https://unsplash.com/@aldyrkhanov) on [Unsplash](https://unsplash.com/photos/CDpCbaOThwg)


