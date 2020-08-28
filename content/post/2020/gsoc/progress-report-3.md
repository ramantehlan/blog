---
title: "2nd Evaluation of nteract-play"
date: 2020-08-04T10:38:40+05:30
lastmod: 2020-08-04T10:38:40+05:30
draft: true
keywords: ["GSOC", "Raman Tehlan", "progress report", "nteract-play", "ramantehlan", "2nd evaluation"]
description: "2nd Evaluation for nteract-play project for Google Summer of Code"
tags: []
categories: []
author: "Raman Tehlan"

images: ["https://user-images.githubusercontent.com/29037312/82077369-ebc98900-96fc-11ea-8bc6-ce835bd89593.jpg"]

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
# enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""

---

<!--more-->

<p style="text-align: justify;">
The 2nd evaluation of GSoC is complete, and I have passed it (Yay!). I had less time than usual in my 2nd phase/month to work because I had to give my university exams from 1st July till 15th July. I was able to wrap up the FileExplorer component and complete the Github integration by making the save feature work. 
</p>

# FileExplorer

<p style="text-align: justify;">
Initially, I was going to use the component created for nteract Desktop. But after considering the efforts required to make that component work with nteract web, creating a new component from scratch seemed like a better option. So, below is the FileExplorer component, used to load files and folders from Github repo. 
</p>

<img src="https://user-images.githubusercontent.com/29037312/90346794-ae510080-e049-11ea-942a-cdd34b505cfa.gif" />

# Saving back to Github.

<p style="text-align: justify;">
Once you make your changes to files, you can save your changes back to Github. The logic of Github integration was discussed in the <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/progress-report-1/">first report</a>.  
</p>

# 3rd phase
August is the 3rd or the last phase of the GSoC period. So this month I will be working on the binder and nteract integration. Also, all the minor features will be added, like the introduction section, or dynamic routing etc. 


