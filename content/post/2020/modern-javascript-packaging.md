---
title: "Modern JavaScript Packaging"
date: 2020-04-09T11:37:26+05:30
lastmod: 2020-04-12T11:37:26+05:30
draft: true
keywords: []
description: "Learn how to package Javascript"
tags: []
categories: []
author: "Raman Tehlan"

images: ["https://user-images.githubusercontent.com/29037312/79023992-48d29c00-7b9f-11ea-924c-1e0318389ec8.jpg"]

---


<img src="https://user-images.githubusercontent.com/29037312/79023992-48d29c00-7b9f-11ea-924c-1e0318389ec8.jpg" width=745px/>

In 2019, [Github announced its Package registry](https://techcrunch.com/2019/05/10/github-gets-a-package-registry/) for Javascript and few other languages, which means now you can publish and manage your packages on both Github and NPM and use any package manager client. Through this blog, I will try to explain how you can do it, and **by the end, you will know everything to build and publish your package to any registry, Github, or NPM.**

> If you are familiar with npm or package building, you can jump directly to the [publishing](#publishing) part.

# **Packages and Registry**

**A package is a piece of software that is Independent, reusable, and distributable**. In Nodejs, [each file is treated as a separate module](https://nodejs.org/api/modules.html#modules_modules), and a package is made of one or one or more modules, and it might or might not depend on other packages.

Registries stores all the packages and their different versions; they are used to distribute packages via a Package manager. Following are the registries for Javascript Packages:

- NPM Registry: [registry.npmjs.org](https://registry.npmjs.org/)
- Github Registry: [npm.pkg.github.com](https://npm.pkg.github.com/)


# **Package manager**

**A package manager is used to install, delete, and manage packages**. It searches for the package you are looking for and installs it in the `node_modules`. It serves as a client for the registry and helps you interact with it. The tree major package managers for Javascript are:

- [**npm**](https://npmjs.com/): It is the default package manager created in 2009; it communicates with the registry and works as the interface for it.

- [**yarn**](https://yarnpkg.com/): It is the most popular alternative; it supports offline cache, Deterministic Installs, License Checks. That makes it secure, fast, and reliable.

- [**pnpm**](https://pnpm.js.org/):
It is known for saving disk space by storing one package version just once on the system, and it is faster than npm.

# **Example**

For this blog, we will create a tiny and simple **package to find the distance between a given point and the origin**. I have already published this [package](https://github.com/ramantehlan/ts-packaging-101/packages/177465), and you can find the source code [here](https://github.com/ramantehlan/ts-packaging-101).

## Initialization Package

We need to create a manifesto file to tell the package manager that a repository is a javascript package, here [package.json](https://docs.npmjs.com/files/package.json) is the manifesto file. It holds all the crucial details about it, from package name to version, dependencies, etc. To do so, we will create a new folder and initialize npm init, follow the commands given below:

```bash
$ mkdir ts-packaging-101
$ cd ts-packaging-101
$ npm init -y
```

This will create a file `package.json`, which should resemble the following file. You also need to fill in the essential details in this manifesto file, like version, description, author, etc.
Here you can keep any package name, but remember **Github only supports scoped packages, so the name should be formatted as `@owner/name`** and should contain lowercase letters only, even if your owner name is in uppercase.

```json
{
  "name": "@ramantehlan/ts-packaging",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

## Install Dependencies

We will write our package in [Typescript](https://www.typescriptlang.org/), which is a superset of javascript. The reason for using Typescript are: 

- Optional static typing.
- The ability to compile down to a version of JavaScript that runs on all browsers.

To be able to use Typescript, we need to install the `typescript` module as a development dependency.

```bash
$ npm install --save-dev typescript
```

This will create a [`node_modules`](https://docs.npmjs.com/configuring-npm/folders.html) directory, which holds all the dependencies for the project. If you open it, you will see Typescript is installed there. It will also create an autogenerate [`package-lock.json`](https://docs.npmjs.com/configuring-npm/package-lock-json.html), and it describes the exact dependency tree that was generated.

## Configure

We also need to configure the Typescript to use it for our project, and we do it by adding a file [tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html). You can use the configuration given below for this example.

```json
{
  "compilerOptions": {
    "target": "es5",        /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017','ES2018' or 'ESNEXT'. */
    "module": "commonjs",   /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext'. */
    "declaration": true,    /* Generates corresponding '.d.ts' file so that the package can be used with Typescript too. */
    "outDir": "./dist",     /* Redirect output structure to the directory. */
    "strict": true,         /* Enable all strict type-checking options. */
    "esModuleInterop": true /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */
  },
  "include": ["src"],
  "exclude": ["node_modules", "dist"]
}
```

We also need to configure our `package.json` to specify the build command and our Github repository. I am assuming you are familiar with Github and can create and push your repository. If you are not, I will suggest you learn about it [here](https://resources.github.com/whitepapers/How-GitHub-secures-open-source-software/).

We need to add the **entry point** of the package, which is going to be `dist/index.js`, this file is not present yet, but will be once we build the project. We also need to provide the **method to build** it, for that we are using `tsc`(Typescript compiler). We need to provide the Github repository for the project. It is required to publish your package to Github Registry. You also need to add `files` key to package.json, to **whitelist** the files or folders you want to publish.You need to add the following lines to your `package.json` file to add the above mentions things.



```json
...
  "main": "dist/index.js",
  "scripts": {
    "build": "tsc"
  },
  "homepage":"https://github.com/ramantehlan/ts-packaging-101#README",
  "files": ["dist/**"],
  "repository":{
    "type": "git",
    "url": "git+https://github.com/ramantehlan/ts-packaging-101.git"
  },
...
```

## Program

We are going to write an elementary program for this example. It's going to be functional. However, this program is practically useless and is just for demonstration, in the working world, you will be expected to create better and useful packages. This program can be used to find the distance between the given point and the origin. Create an `index.ts` file the './src' folder and write the following program init.

```Typescript
/*******************************************************
*  This module is to find the distance between the origin
*  and the given point.  Root(x^2 + y^2)
*********************************************************/

export class Point{
 x:number
 y:number
 dist: number

 constructor(x:number ,y:number){
  this.x = x
  this.y = y
  this.dist = Math.sqrt( Math.pow(this.x, 2) + Math.pow(this.y, 2) )
 }

 getDistFromOrigin() {
   return this.dist
 }


}
```

So far, this is how your file structure looks like. If you run `npm run build`, it will also create the `dist/index.js`, which is the compiled program and is the entry point.

```bash
.
├── package.json
├── package-lock.json
├── tsconfig.json
├── node_modules
│   └── typescript
└── src
    └── index.ts
```

# **Publishing**

We have a package that we want to publish to the NPM registry or Github registry. We start by authenticating, which is a little different for NPM and Github.

## NPM

### Authenticate

You need to sign up at [npmjs.com](https://www.npmjs.com/signup) and use those credentials to log in to npm client.

```bash
$ npm login
Username: NPM_USERNAME
Password: NPM_PASSWORD
Email: (this IS public) NPM_EMAIL
```

### Publish

Now we can publish our package; to do so, use the following command.

```bash
npm publish --access public
```

We are using `--access` because since scoped naming for packages is usually used for private packages in NPM, so to bypass that, we need to specify that our package is to be public.

### Install

To Install packages from NPM registry, users can directly use the package name as shown below:

```bash
npm install @OWNER/PACKAGE_NAME
```

### Un-Publish

Unpublishing your package is not recommended. Instead, you can depreciate it. 

[According to the unpublish policy of NPM](https://www.npmjs.com/policies/unpublish), **you can't unpublish a version after 24 hours of publishing it, and you can't unpublish a package after 72 hours of publishing** and only if there are no dependents on it. Before that, to un-publish a package, you can run the following command.

```bash
npm unpublish
```


## Github

### Generating Token

To authenticate with Github, we need to generate a [personal access token](https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line). You do that by first logging into your Github account, then go to **Settings -> Developer settings -> Personal access tokens**. Click on **Generate new token**. You will be asked to provide a note(name) for the token.

<center>
<img src="https://user-images.githubusercontent.com/29037312/79050155-ce108c00-7c45-11ea-9fa1-5cb88be25331.png" width="800px">
</center>

And select the **write:packages** permissions for it and click on the **Generate token** button on the bottom of the page.

<center>
<img src="https://user-images.githubusercontent.com/29037312/79050156-cea92280-7c45-11ea-85da-aae4eaf9288c.png" width="600px">
</center>

This will generate a token for you, which you should save to a safe place as you are going to see it just once.

<center>
<img src="https://user-images.githubusercontent.com/29037312/79050569-7162a080-7c48-11ea-8ff7-2edb338adaeb.png" width="600px">
</center>

### Authenticate

There are two ways to [authenticate](https://help.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-npm-for-use-with-github-packages#authenticating-to-github-packages) now:

- By adding your access token to your ~/.npmrc file.
- By logging in to npm with your access token.

I am a little opinionated here, and I like the second method because and I am going to use that for this blog. In the first one, there are chances of the file getting committed if you backup your dotfiles, and In case you lose your token, you can always generate it back and log in again.

To authenticate, we can generate the token and login to the Github registry. We do so by following the commands given below.

```bash
$ npm login --registry=https://npm.pkg.github.com
  Username: GITHUB-USERNAME
  Password: TOKEN
  Email: PUBLIC-EMAIL-ADDRESS
```

### Publish

The package is ready, and we are authenticated to publish the packages. There are two ways to publish your package.

- [Publishing using a local .npmrc file.](https://help.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-npm-for-use-with-github-packages#publishing-a-package-using-a-local-npmrc-file)
- [Publishing using *publishConfig* in the package.json file.](https://help.github.com/en/packages/using-github-packages-with-your-projects-ecosystem/configuring-npm-for-use-with-github-packages#publishing-a-package-using-publishconfig-in-the-packagejson-file)

For this blog, we are going to use the second method; however you can use any method. The only reason for this decision is that I want to avoid creating one more file. Open your `package.json` file and add `publishConfig` section to it.

```json
...
 "publishConfig": {
    "registry":"https://npm.pkg.github.com/"
  },
...
```

Now we can publish our package; to do so, use the following command.

```bash
npm publish
```

### Install

To use any package published on Github, users need to add it to their projects .npmrc file, create this file if it doesn't already exist. They need to specify GitHub Packages URL and the account `owner`. For multiple owners, you need to specify multiple GitHub Packages URL.

```npmrc
registry=https://npm.pkg.github.com/OWNER
@OWNER:registry=https://npm.pkg.github.com
@OWNER:registry=https://npm.pkg.github.com
```

After this, you shall be able to download the packages.

```bash
$ npm install @OWNER/PACKAGE-NAME
```


### Un-Publish

[**You can't delete an entire public package or specific versions**](https://help.github.com/en/packages/publishing-and-managing-packages/deleting-a-package#about-public-package-deletion), Github restricts that to avoid breaking projects that may depend on that package. You can, however, delete private packages. To do so, you can use the command given below.

```bash
$ npm unpublish
```

# Conclusion

I hope this blog was helpful, and after reading this, you feel a little confident about creating your package and publishing it. I suggest you read more about it from the links I have provided throughout the blog, and you can also look at the [source code](github.com/ramantehlan/ts-packaging-101) and the [published package](https://github.com/ramantehlan/ts-packaging-101/packages/177465). 

If you like this blog, do follow me on [twitter](https://twitter.com/ramantehlan) and share this blog.

# Acknowledgement

- Hero image by [Kristina Paparo](https://unsplash.com/@emilep) on [Unsplash](https://unsplash.com/photos/xrVDYZRGdw4)

> Let's discuss it on [Reddit](https://www.reddit.com/search/?q=url%3Ahttps%3A%2F%2Framantehlan.github.io%2Fblog%2Fpost%2F2020%2Fmodern-javascript-packaging%2F) or [Twitter](https://twitter.com/search?q=https%3A%2F%2Framantehlan.github.io%2Fblog%2Fpost%2F2020%2Fmodern-javascript-packaging%2F)


