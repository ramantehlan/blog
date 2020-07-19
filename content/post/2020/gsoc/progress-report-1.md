---
title: "What's it like to strategize and build the sails for nteract-play"
date: 2020-06-10T16:26:45+05:30
lastmod: 2020-06-14T16:26:45+05:30
draft: true
keywords: [ "GSOC", "raman tehlan", "progress report", "nteract-play", "ramantehlan"]
description: "1st Progress report by Raman Tehlan on nteract-play project for Google Summer of Code"
tags: []
categories: []
author: "Raman Tehlan"

images: ["https://user-images.githubusercontent.com/29037312/84971664-da7bfe00-b13a-11ea-8b2c-f019f9bcaf87.jpg"]


# You can also close(false) or open(true) something for this content.
# P.S. comment can only be closed
comment: true
toc: true
autoCollapseToc: false
postMetaInFooter: true
hiddenFromHomePage: false
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
  enable: true
  options: "{
    'x': 0,
    'y': 0,
    'line-width':1.5,
    'line-length':20,
    'text-margin': 10,
    'font-size': 12,
    'font-color':'black',
    'line-color': 'black',
    'element-color': 'black',
    'fill': 'white',
    'yes-text': 'Yes',
    'no-text': 'No',
    'arrow-end': 'block',
    'scale': 0.9
  }"

sequenceDiagrams: 
  enable: false
  options: ""

---

<!--more-->

<img src="https://user-images.githubusercontent.com/29037312/84971664-da7bfe00-b13a-11ea-8b2c-f019f9bcaf87.jpg">

<p style="text-align: justify;">
Building an application is like building a ship. At various stages, you have to wear different hats of diverse perspectives to understand what goes where next and plan accordingly. At one point, you are thinking about the engine(algorithm), and at another, you are thinking about the design. You have to consider every small detail, to keep the boat afloat amidst storms of technical crises and bugs along with taking care of the fact that every passenger is provided with their own safety kits, here pointing towards the accessibility factor. 
</p>

<p style="text-align: justify;">
That’s how I feel while I sail my ship of <a href="https://github.com/nteract/play">nteract-play</a>, which I have to develop while learning the required skills. Also, we don’t talk much about how writing open-source code which is public can be intimidating for people (well, it is- at least for me!).  I thank my stars for the fact that I have <a href="https://twitter.com/captainsafia">Safia</a> as my mentor as she is the one getting me through this and making it easier for me to work on my project. In the first two weeks, Safia and I have taken some critical decisions about the same and they have proven to be wise, indeed. If you have not read the <a href="https://ramantehlan.github.io/blog/post/2020/gsoc/proposal/">initial proposal</a>, I would recommend you to give it a read in order to connect with this piece better. 
</p>

Let’s look at the in-depth progress so far, shall we?

# Workflow

<p style="text-align: justify;">
I am working on a different repository, before moving the code to nteract-play. Now you must be wondering why, so let’s just kill the suspense already because I am working on it to eventually make it a part of <a href="https://nteract.io/applications">nteract ecosystem</a>. It will not only lead to individual success, instead, but it shall also influence both the projects and push forward towards success.
</p>

<p style="text-align: justify;">
My initial proposal constituted of an auto-save mode to save changes when you run your notebook or the cell. However, we decided to go with just user-save mode since we don’t have enough time or bandwidth for the same; however, we always have an option of adding it later. I found this paper “<a href="https://arxiv.org/abs/1909.04352">Automatic Code Summarization: A Systematic Literature Review</a>” which can be helpful to choose the right method to generate auto-commits.
</p>

## Auto-Save-Mode

```flowchart
st=>start: Get Github Details
user/repo/branch
e=>end: Run
e2=>end: Run

c1=>condition: Repo Exist
c2=>condition: User Logged in
c3=>condition: Wants to Save
c4=>condition: User is owner 
of repo or forked

op1=>operation: Throw Error
op2=>operation: On Cell Run
op3=>operation: Login using OAuth
op4=>operation: Fork the Repo
op5=>operation: Generate Commit message
op6=>operation: Save

io=>inputoutput: Get and Edit 
Content

st->c1
c1(no)->op1
c1(yes)->io
io->op2->c2
c2(no, below)->c3
c3(no)->e
c3(yes, right)->op3
op3(right)->c4
c2(yes)->c4
c4(no, right)->op4->op5
c4(yes)->op5->op6->e2
```

## User-Save-Mode


```flowchart
st=>start: Get Github Details
user/repo/branch
e=>end: Run
e2=>end: Run

c1=>condition: Repo Exist
c2=>condition: User Logged in
c4=>condition: User is owner 
of repo or forked

op1=>operation: Throw Error
op2=>operation: On Save
op3=>operation: Login using OAuth
op4=>operation: Fork the Repo
op5=>operation: User give
commit message
op6=>operation: Ask user:
output stripped?

io=>inputoutput: Get and Edit 
Content

st->c1
c1(no)->op1
c1(yes)->io
io->op2->c2
c2(no, below)->op3
op3(right)->c4
c2(yes)->c4
c4(no, right)->op4->op5
c4(yes)->op5->op6->e2
```

# Github OAuth

<p style="text-align: justify;">
I will be using the already created <a href="https://github.com/nteract/oauth-server">OAuth-server</a> for nteract-play. As my initial proposal was more about the implementation, I didn’t go in detail about the security of local storage for saving the token. But, I will be taking some measures like encryption etc. to make it more secure. Using the token, we can use <a href="https://octokit.github.io/rest.js/v18">octacat/api</a> to perform the following and more key tasks.
</p>

- Check if the user is the owner of the repo. We can do this by checking the username currently logged in and the username of the repository's owner.
- `octokit.repos.listForks`: Check if the fork already exist.
- `octokit.repos.createFork`: Create a fork.
- `octokit.repos.getBranch`: Check if a branch exists.


# Design

<img src="https://user-images.githubusercontent.com/29037312/84603563-ed799e80-aeac-11ea-9e48-1cb168a87493.gif" />

<p style="text-align: justify;">
I used <a href="https://www.figma.com">Figma</a> for the first time to create the above prototype, and it was really helpful. If you are a non-designer (like me) and have to design something, always think about making it <a href="https://developer.mozilla.org/en-US/docs/Learn/Accessibility/What_is_accessibility">accessible</a> for all. I considered it, but then Safia pointed out issues in font and colour. After reading more about it, I reconsidered it. It’s crucial-- you must think about it and improvise accordingly.
</p>

<p style="text-align: justify;">
If you are not a designer or have issues with differentiating colours or are influenced by colour-blindness -- I would recommend using colour-palettes or taking help from your designer friends. You can also use plugins like A11y-Color Contrast Checker or Color-Blind. If you are using React, then skim through <a href="https://reactjs.org/docs/accessibility.html">this page</a> once as it might serve to be of some help to you.
</p>

<p style="text-align: justify;">
I have created this new repo <a href="https://github.com/nteract/ui-web/">UI-web</a> to start building my design components further and use them in the application.
</p>

# Learning
<p style="text-align: justify;">
I have learned a lot so far. I reread the <a href="https://reactjs.org/docs/getting-started.html">React docs</a> to brush up my skills (as I have only used it once for a small project). I learned and utilised Figma for the first time for creating that design. I had only limited experience with <a href="https://storybook.js.org/">Storybook</a>, but I am enjoying it so far. I am yet to learn so much more, especially all about <a href="https://redux.js.org/">redux</a> next.
</p>

# Conclusion
<p style="text-align: justify;">
I am enthused to build my ship as I code it away and get you on board in the process. In the coming days, I will be working on building components and finally integrating Github features in the project. I hope I can complete it on time, *fingers crossed*, so by the end of phase 1 we can have a working prototype for it.
</p>

# Acknowledgment 

- Hero image by [Alonso Reyes](https://unsplash.com/@alonsoreyes) on [Unsplash](https://unsplash.com/photos/LWFdBz4d6nE)
