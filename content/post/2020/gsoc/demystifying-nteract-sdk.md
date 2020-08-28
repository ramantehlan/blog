---
title: "Demystifying nteract SDK"
date: 2020-08-16T10:38:40+05:30
lastmod: 2020-08-16T10:38:40+05:30
draft: true
keywords: ["GSOC", "Raman Tehlan", "nteract", "nteract web", "nteract play", "ramantehlan", "nteract SDK", "ramantehlan"]
description: "This blog is about understanding nteract ecosystem and nteract SDK."
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

flowchartDiagrams:
  enable: false
  options: ""

sequenceDiagrams: 
  enable: false
  options: ""

---

<!--more-->


<p align="center">
<img src="https://user-images.githubusercontent.com/29037312/90440851-87500880-e0f5-11ea-8f86-92673cd4c80c.jpeg" />
</p>

<p style="text-align: justify;">
In the past 2.5 months, I got to learn a lot of new things. I got to create complex react components; I learned about creating effective UI/UX, I feel I am better at making decisions about product development now. I also enjoyed getting familiar with developing notebook apps using nteract. 

</p>

<p style="text-align: justify;">
As I was learning more about nteract and getting more involved with the community. I noticed that people do show interest in contributing to nteract. However, only a small portion of interested people end up moving forward. What I feel is that there are not many blogs and other resources about the core principle. 

</p>


<p style="text-align: justify;">
In this blog, I will try to demystify nteract and cover nteract SDK in detail. The aim here is to make the engineering behind notebooks simple and more approachable. 
</p>

# Audience

<p style="text-align: justify;">
This blog is for anyone interested in either using nteract SDK in their project or someone who wants to contribute to it. 

There are no hard prerequisites to understand the concept. However, if you are already familiar with Javascript, RxJs, React or Redux, It will be easy for you to understand and get started with it. If you are not familiar with any or some of them, don't worry, the important thing is the willingness to learn. The language for this blog is generic and easy to understand.
</p>


# nteract organization

Let's start by looking at the zoomed-out view and see what nteract organization does and look at the overview of its ecosystem. 

<p align="center">
<img src="https://user-images.githubusercontent.com/29037312/90455308-65657e80-e113-11ea-9243-dd63f9569623.png" width="800" />
</p>


<p style="text-align: justify;">
You can find all the applications and libraries on the nteract's <a href="https://github.com/nteract"/>Github page</a>. All the libraries and some applications have their respective repositories with proper documentation for you to get started. 
</p>

<p style="text-align: justify;">
Now let's talk about nteract SDK in-depth, which is used to create interactive notebook applications.
</p>

# nteract SDK

<p style="text-align: justify;">
nteract SDK is a group of javascript packages used to create notebook apps. They all are developed and managed under a mono-repo here. This mono-repo is also used to manage applications based on nteract SDK, like nteract Desktop, nteract Web etc. 
</p>

<p style="text-align: justify;">
There is no official segmentation, but to make it easy to understand, we can divide nteract SDK into three sections. 
</p>

- Core Packages
- UI Packages
- Jupyter Packages


<p align="center">
<img src="https://user-images.githubusercontent.com/29037312/91505336-f6dfa800-e8ec-11ea-8ee9-9c12cc4eaf15.png" width="800" />
</p>


## **Core Packages**

<p style="text-align: justify;">
Core packages provide the basic/core functionality of the notebook. To use core packages, you have to import one package, @nteract/core. This package encapsulates all five core packages. The reason for encapsulating the packages in one is to keep the version the same and reduce errors due to package version mismatch. 
<br/><br/>
You can read about the principle behind core packages <a href="https://docs.nteract.io/nteract/core/overview/">here</a>. Five core packages are:
</p>

1. <a href="https://github.com/nteract/nteract/tree/main/packages/types">@nteract/types</a>
- <a href="https://github.com/nteract/nteract/tree/main/packages/actions">@nteract/actions</a>
- <a href="https://github.com/nteract/nteract/tree/main/packages/reducers">@nteract/reducers</a>
- <a href="https://github.com/nteract/nteract/tree/main/packages/selectors">@nteract/selectors</a>
- <a href="https://github.com/nteract/nteract/tree/main/packages/epics">@nteract/epics</a>

<p align="center">
<img src="https://user-images.githubusercontent.com/29037312/91542212-1b627100-e93b-11ea-9b4f-d610e3a26570.png" />
</p>

### @nteract/types
This package contains definitions of different data types used in nteract application. These data types are used to store data for kernels, notebooks, hosts etc. 

For example, below is how  `KernelspecMetadata` and `KernelspecInfo` data types are defined in this package.

```javascript
export interface KernelspecMetadata {
  display_name: string;
  language: string;
  argv: string[];
  name?: string;
  env?: {
    [variable: string]: string;
  };
}

export interface KernelspecInfo {
  name: string;
  spec: KernelspecMetadata;
}
```

### @nteract/actions

<p style="text-align: justify;">
This package contains definitions of constants and action creators that can be used to create Redux actions in nteract application. These actions can be dispatched to create new cells, launch kernels, create new notebooks, execute cells, and much more.
</p>
 
<p style="text-align: justify;">
 For example, below is how you define an action to update kernel specifications. Also note it uses the `KernelspecInfo` data type as parameters(payload), which is defined above. 
 </p>

```javascript
// Define the action type
export const SET_KERNELSPEC_INFO   = "SET_KERNELSPEC_INFO";

// Define the payload
export type SetKernelspecInfo = Action <typeof SET_KERNELSPEC_INFO,  HasContent & { kernelInfo: KernelspecInfo }>;

// Create action
export const setKernelspecInfo  = makeActionFunction <SetKernelspecInfo> (SET_KERNELSPEC_INFO);
```

### @nteract/reducers

<p style="text-align: justify;">
This package contains a set of Redux reducers for use in nteract applications. Reducers describe the change in the application's state in response to actions sent to the store.
</p>
 
<p style="text-align: justify;">
 Below is how reducer sets the kernel information when `SetKernelspecInfo` action is dispatched.
 </p>

```javascript
...
case actionTypes.SET_KERNEL_INFO:
      typedAction = action as actionTypes.SetKernelInfo;
      let codemirrorMode = typedAction.payload.info.codemirrorMode;
      if (!codemirrorMode) {
          codemirrorMode = typedAction.payload.info.languageName;
      }

         switch (typeof codemirrorMode) {
                 case "string":
                    // already set as we want it
                 break;
                 case "object":
                    codemirrorMode = Map(codemirrorMode as JSONObject);
                 break;
                 default:
                    // any other case results in falling back to language name
                    codemirrorMode = typedAction.payload.info.languageName;
           }

        const helpLinks = typedAction.payload.info.helpLinks
                ? List(
                    (typedAction.payload.info.helpLinks as HelpLink[]).map(
                        makeHelpLinkRecord
                    )
                  )
            : List();

        return state.setIn(
                [typedAction.payload.kernelRef, "info"],
                makeKernelInfoRecord(typedAction.payload.info).merge({
                  helpLinks,
                  codemirrorMode
                })
              );
...
```

### @nteract/selectors

<p style="text-align: justify;">
This package provides a set of selectors and functions that allow you to extract important information from the state of your nteract application. To see a full set of the data stored in application state that be extracted with this package, you can view the AppState type. 
</p>

Below is how the currentKernel selector is defined.

```javascript
/**
 * Returns the kernelspec of the kernel that we are currently connected to.
 * Returns null if there is no kernel.
 */
export const currentKernel = createSelector(
  [currentKernelRef, kernelsByRef],
  (kernelRef, byRef) => (kernelRef ? byRef.get(kernelRef) : null)
);
```

Below is how we use the selector in epics or in UI library
```javascript
import * as selectors from "@nteract/selectors";
...
kernel = selectors.currentKernel(state$.value);
...
```

### @nteract/epics

<p style="text-align: justify;">
This package contains a set of Redux-Observable epics for use in nteract applications. It is a function which takes a stream of actions and returns a stream of actions.
</p>

Below is how `acquireKernelInfoEpic` is defined.

```javascript
/**
 * Gets information about newly launched kernel.
 *
 * @param  {ActionObservable}  The action type
 */
 export const acquireKernelInfoEpic = (
    action$: Observable<actions.NewKernelAction>,
    state$: StateObservable<AppState>
 ) =>
  action$.pipe(
    ofType(actions.LAUNCH_KERNEL_SUCCESSFUL),
    switchMap((action: actions.NewKernelAction) => {
      const {
         payload: {
            kernel: { channels, kernelSpecName },
            kernelRef,
            contentRef
          }
       } = action;
      
      return acquireKernelInfo(
         channels,
         kernelRef,
         contentRef,
         state$.value,
         kernelSpecName
      );
    })
 );
```

## **UI Packages**

<p style="text-align: justify;">
UI Packages are react based components used to created different UI elements of the nteract ecosystems like notebook, cells, buttons etc. Some of the packages are stateful, but some are not and require you to set up your store. If you want to help with improving the UI of nteract, these are the packages you can explore. 
</p>

- [@nteract/editor](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/editor)
- [@nteract/monaco-editor](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/monaco-editor)
- [@nteract/mythic-notifications](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/mythic-notifications)
- [@nteract/notebook-app-component](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/notebook-app-component)
- [@nteract/presentational-components](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/presentational-components)
- [@nteract/stateful-components](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/stateful-components)
- [@nteract/styles](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/styles)
- [@nteract/directory-listing](https://github.com/nteract/directory-listing)
- [@nteract/dropdown-menu](https://github.com/nteract/dropdown-menu)
- [@nteract/logos](https://github.com/nteract/logos)
- [@nteract/markdown](https://github.com/nteract/markdown)
- [@nteract/mathjax](https://github.com/nteract/mathjax)
- [@nteract/octicons](https://github.com/nteract/octicons)
- [@nteract/outputs](https://github.com/nteract/outputs)
- [@nteract/styled-blueprintjsx](https://github.com/nteract/styled-blueprintjsx)

## **Jupyter Packages**

<p style="text-align: justify;">
Jupyter packages help in interacting with different components of Jupyter ecosystem, like jupyter server, binder etc. Following are the jupyter packages in nteract ecosystem. 
</p>

- [@nteract/host-cache](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/host-cache)
- [@nteract/messaging](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/messaging)
- [@nteract/rx-binder](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/rx-binder)
- [@nteract/rx-jupyter](https://github.com/nteract/nteract/tree/49983455451c1038a59408537e8698ebca9f074a/packages/rx-jupyter)
- [@nteract/enchannel-zmq-backend](https://github.com/nteract/enchannel-zmq-backend)

# Conclusion

<p style="text-align: justify;">
I hope this blog has given you some more confidence in getting started with nteract SDK and contribute to it. If you are planning to use it for development, this blog should be a good starting point in understanding the working of it. I will suggest you read more about it on <a href="https://github.com/nteract">Github</a> and join the community on <a href="https://nteract.slack.com/">Slack</a>
</p.

# Acknowledgment
- Hero image by [Dollar Gill](https://unsplash.com/@dollargill) on [Unsplash](https://unsplash.com/photos/0V7_N62zZcU)

