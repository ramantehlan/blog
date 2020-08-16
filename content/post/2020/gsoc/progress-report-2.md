---
title: "1st Evaluation of nteract-play"
date: 2020-07-16T17:59:09+05:30
lastmod: 2020-07-16T17:59:09+05:30
draft: true
keywords: ["GSOC", "Raman Tehlan", "progress report", "nteract-play", "ramantehlan", "1st evaluation"]
description: "1st Evaluation for nteract-play project for Google Summer of Code"
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
#enableOutdatedInfoWarning: false

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""

---

<!--more-->


In my last blog, I talked about two main tasks:

1. Developing the project using a blueprint created in Figma. 
2. Integrating Github API in nteract play. 

<p style="text-align: justify;">
After 1st evaluation, let’s look at how far along we are with the project.
</p>


## UI/UX Integration

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
- [ ] Notification 
- [ ] Notebook rendering.
- [ ] FileExplorer 

## Github Integration

- [x] Complete authentication
- [x] Fetch user's public info
- [x] Fetch public files and folders 
- [x] List and create a fork for repo
- [ ] Save back changes to the repo or the fork 

## MyBinder Integration

- [ ] Launch MyBinder instance on start
- [ ] Communicate with JupyterServer.
- [ ] Connect iterm.js to MyBinder instance
- [ ] Execute the command on MyBinder instance

</p>

## Conclusion

<p style="text-align: justify;">
I am glad that I passed my 1st evaluation, and I get to continue to work on the project and complete the rest of the tasks.
</p>

<p style="text-align: justify;">
<b>
The focus for the 2nd evaluation will be on implementing the notebook, saving the changes to Github and making the FileExplorer work</b>.  Safia and I feel this PR is too big, so all the pending tasks after 2nd evaluation will be done in a new PR. 
</p>



