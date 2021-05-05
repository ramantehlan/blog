---
title: "Pulse Journal"
date: 2020-05-10T15:05:47+05:30
lastmod: 2020-05-10T15:05:47+05:30
draft: false
keywords: []
description: "Pulse is a heartbeat monitor; it connects with your smart band and fetches your pulse in real-time to display it on a dashboard."
tags: []
categories: []
author: "Raman Tehlan"

images: ["https://raw.githubusercontent.com/ramantehlan/pulse/master/resources/pulse.png"]


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

<br>
<br>
<p align="center">
<img src="https://raw.githubusercontent.com/ramantehlan/pulse/master/resources/icons/logo.png" width="75">
</p>

<h1 align="center">**Pulse**</h1>
<h5 align="center">**Simple Heartbeat Monitor :heart: :bar_chart:**</h5>

<br>
<br>

**[Pulse](https://github.com/ramantehlan/pulse) is a heartbeat monitor; it connects with your smart band and fetches your pulse in real-time to display it on a dashboard.** I created this for my major submission in the final semester. This blog is to journal the steps and decisions taken while creating this project and I will try to explain things in detail, but somethings might be edgy and unclear, and that is because I am writing this after completing the project, so can't recall all the stuff.

> If you are here for just the design process, you can directly jump to that [part](#design-process).


# Backstory

This project was initially **conceptualized during a hackathon**(Ultrahack Delhi - 2019). I had this very **raw idea of analysing health data and predicting diseases**, and after teaming with 4 of my friends we came up with this idea of using the smart band(Miband 3) and ECG sensor to get data and then analyse it and together we created [**curie**](https://github.com/ramantehlan/Curie). It worked great, the exciting thing is, while presenting it, I was wearing the band and **judges could see my heartbeat in realtime on a chart!** However, we didn't win, but it was a pleasant experience.

A year later, in my final semester, I needed to create a project for submission; that's when I decided to take another look at the idea and recreate it with a more robust and practical application. That's how pulse was created.

# Vision


As I see it, in the future, Imagine a **subscription service provided by your hospitals**, with a partnership with other companies they will give you a smart bands/watch or other wearable devices, and they will then privately and securely connect with that device to analyse your health vitals in realtime, to **predict the health problems you might have in your lifetime**.

Or, think of an application to help **athletes to tap into their health insights** and help them in making smart and informed health decisions, by recommending health diets or fitness routines etc. These are just two examples. Otherwise, there are many many applications for it.


**Future needs cheap and advanced health analysis, something that can be easily and rapidly implemented even in the poorest countries**. It's not like it's not already happening; it is, but this project is just an experiment to discover and create one of the ways to implement it.

# Design Process

## Phase 1

:beginner: **Goal:**
Initially, I wanted to write the application in just one language(Go) and use the binary to distribute it via a snap or use another medium.

To do so, I also need to compile the frontend files in the binary, and for the I used [**pkger**](https://github.com/markbates/pkger), it was a little tricky to configure it, but after trying out for few days, I was able to generate `pkger.go` file which contained the frontend files.


The second thing I had to do was find a way to connect to Bluetooth devices in Go, and I came across a few options and decided to go with [**Paypal/gatt**](https://github.com/paypal/gatt) package. Even though this package wasn't maintained for a long time, it was still the most starred and forked package from other options.

However, now when I think about it, it wasn't the right package to pick, I was able to discover and connect to devices, but I wasn't able to pass data or fetch services from the Bluetooth device, even after spending countless hours I wasn't able to figure it out, and if your have to spend days to do a very simple task using a library then probably it's a wrong library you are using.

:heavy_plus_sign: **Take away**

- Maintenance/Contributors > stars or forks, It might look obvious now, but trust me, it wasn't.


## Phase 2

:beginner: **Goal**: Use another library to connect to the Miband and embed it in Go.

Since Paypal/gatt didn't work for me; I decided to use [**yogeshojha/MiBand3**](https://github.com/yogeshojha/MiBand3) to connect and work with Mibands. My goal was to have just one binary, so I wanted to compile this program with go as I did with frontend. I tried many things to do that:


- I thought of using **Cython** to transpile the code to **C** and using [**cgo**](https://golang.org/cmd/cgo/) call the functions in Go. I tried it, but it didn't work, and the reason is, even for a simple program like hello world, cython transpile it to very cumbersome C files, and even if you spend time to understand the structure of the output C file, there is no guarantee it won't change in future updates, and its because it is not designed to be used with cgo.
- I could also use **.so** files generated by Cython and call them in go using [**rainycape/dl**](https://github.com/rainycape/dl) package, and that didn't work either for the same reason as C files didn't work with cgo.
- Then I thought of using go binding for python([Go-python-3](https://github.com/DataDog/go-python3)), but while testing it, it did work, but it turned out to be somewhat tricky and wasn't a reliable solution or a long term solution.

In the end, I decided to create a separate service for Miband3 and communicate with the pulse command using gRPC. It does break my initial goal of creating a single binary for it, but it works and probably is the best solution for the given problem that could be created in a limited time. Also note, the goal of creating the binary was to make it distributable, so this service is designed in a way that you can build a **.whl** file for it and install it on your system. The ideal solution will be to make the gatt package working in Go and rewrite the Miband3 in Go, which doesn't just involve reinventing the wheel but also delays the solution.

:heavy_plus_sign: **Take away**

- **A lousy solution today is better than a good solution tomorrow. You can always optimize and make it better.**

- *Personal opinion*; I think using language extensions or binding can/should be avoided because sometimes you will think its union, but it in most cases is an intersection, and you won't even know it. You will miss out on some essential features of both the languages and the solution will depend on so many unpredictable factors which is not a good thing. I am not saying it's not useful in any case, for example, to reuse a library written in X language inside Y language, it can be used, but in most cases, it can be avoided.

## Phase 3

:beginner: **Goal:** All the part of the project are individually working, and now I had to glue them up.

Since Miband3 is handled by `mibandPulse` service/command, I could run this service on-demand using the **exec** package in Go, but after reading the docs, it turns out, it doesn't keep the programme running and terminates it after the first run. So, this option was out.

The more significant issue I encountered was when running the project together; I discovered that when the `pulse` command was running and using `Paypal/gatt` package, the `mibandPulse` command wasn't able to connect or use Bluetooth, and that's because Paypal/gatt only runs as a sudo by design and takes over the control of Bluetooth.

There were two options I could see were,

- To find out some other library for working with Bluetooth in Go.
- Separate the Bluetooth Go code and run it as independent service to only exploring surrounding services.

I decided to go with the second option, as that was fast and required less efforts then rewriting the whole code again. I created `pulseExplorer` service, which runs for 8 seconds and stream list of Bluetooth devices, this stream is used by `Pulse` command to store the list in its state, which is later sent to the users on the frontend, and when users click supported listed device, the request is sent to `mibandPulse` service to connect and fetch data from that respective device.

**Take Away**

- If you have a problem, then break it down into subproblems and then solve it, if you are still not able to solve it, then probably you need to find more ways to break it down.
- *Personal Opinion*; It's better to manage an application where services are not talking to each other directly, but via a central program, like in this application, all the services only connects to `pulse` service and not to other services directly, even when they can, as `pulseExplorer` can also directly send devices list to the frontend. However, right now it's sending it first to `pulse` and then `pulse` sends it to the frontend, this gives more control over the communication and makes it simple.

## Result

![arch](https://raw.githubusercontent.com/ramantehlan/pulse/master/resources/pulse.png)

# Conclusion

In my opinion, a vital thing to keep in mind when writing code is, to ask yourself that will it run 10 or 20 years from now, and make the decision based on this goal.

Also, read the take away at the end of each phase.


**Note**<br>

This project is more like an experiment or a prototype. So if there are bugs or better coding practices, I will appreciate it if you can politely point them out via Github issues. Also, if you like this project or my other projects, you can follow me on [Twitter](https://twitter.com/ramantehlan) or [Github](https://github.com/ramantehlan) and also maybe give this project a star. :relaxed: :star:


# Acknowledgement

- Logo made by <a href="https://www.flaticon.com/authors/trinh-ho" title="Trinh Ho">Trinh Ho</a> from <a href="https://www.flaticon.com/" title="Flaticon">www.flaticon.com</a>

 


