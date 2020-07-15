---
title: Deploying a React.js app with Github Pages
description: A journey of building and deploying a React.js application with GitHub Pages.
date: '2019-09-23'
---

_With a few hours to kill on a lazy Sunday afternoon..._


## React.js & Github Pages: Will it blend?

![will-it-blend](will-it-blend.png)

This is the first I’ve actually attempted to deploy a React.js project to Github Pages. I’ve certainly deployed way more complicated applications into all sorts of different environments, so this shouldn’t be anything too difficult, right?

(_Yea, it’s hella easy - and is a great way to showcase your work!_)

## So, let’s build a project!

Alrighty folks - today we embark upon a journey to build a _standard issue_ [To-Do App](https://github.com/adamdubey/todo-app) in React! Since this post is more about the actual deployment process, I will not cover much of the build phase since that’s been done to death already in all kinds of tutorials. At some point I will cover a tutorial with a different project in another post some time in the future...

So if you have your own React project you'd like to deploy, or if you're interested in working with the same tech stack[^1] , make sure you have a _working development environment specific to your programming flavor of choice[^2]_, as well as a GitHub account.

[^1]: tech stack: OS X, React.js, Semantic UI, Git, Node.js
[^2]: YMMV on getting your own workspace setup, as there can be multiple variables with languages, packages, and operating systems to select from - if you are in doubt, please consult the [official React documentation](https://reactjs.org/). Also, if you get stuck during initial configuration, _it's probably a configuration or package dependency_

## Building the application

A quick rundown of the project layout - the usual structure and suspects are all present:

```md
.
├── LICENSE
├── README.md
├── app-demo.png
├── package.json
├── public
│   ├── favicon.ico
│   └── index.html
├── semantic.json
└── src
  ├── App.css
  ├── App.js
  ├── App.test.js
  ├── actions
  │   ├── index.js
  │   └── index.spec.js
  ├── components
  │   ├── Footer.js
  │   ├── Link.js
  │   ├── Todo.js
  │   └── TodoList.js
  ├── containers
  │   ├── AddTodo.css
  │   ├── AddTodo.js
  │   ├── FilterLink.js
  │   └── VisibleTodoList.js
  ├── index.css
  ├── index.js
  ├── reducers
  │   ├── index.js
  │   ├── todos.js
  │   ├── todos.spec.js
  │   └── visibilityFilter.js
  └── semantic
```

_Psst: You too can make your own tree!_[^3]

[^3]: `tree` is a Linux program, and can be acquired via Homebrew if you're on OS X. Example usage: `$ tree -v -L 4 --charset utf-8`

I think if I revisit this project, I may expand some of the features such as incorporating a persistent data storage solution as well as user authentication.

For added bonus points, it'd be pretty quick to containerize and leverage some CI/CD to really boost the production value as a portfolio project app -  dare to dream as the sky's the limit!

## Deploying to GitHub Pages

Okay, up to this point you should have a working project. If you have a bunch of errors, or your code will not compile, then please do not proceed!!!

So now we need to add the facilities to be able to deploy to GitHub Pages. To achieve this, we need two things:

* The `gh-pages` package installed in our project workspace
* Updating the `package.json` file with a few new commands to enable deployments to `gh-pages`

To install the `gh-pages` as a dev-dependency package:

```sh
$ npm i --save-dev gh-pages
```

Next, within the `package.json` file you'll need to add the `homepage` property:

```json
"homepage": "https://gitname.github.io/your-project-name"
```

And this is the _"magic part"_ of using GitHub Pages to host your application - by adding the `predeploy` and `deploy` commands to the `package.json` file:

```json
"scripts": {
"predeploy": "npm run build",
"deploy": "gh-pages -d build",
"start": "react-scripts start",
"build": "react-scripts build",
"test": "react-scripts test --env=jsdom",
"eject": "react-scripts eject"
},
```

Basically whenever you execute `npm run deploy` your application it will use this information. Definitely a piece of cake!

For context, the `predeploy` command will just build a production copy of the application locally - it's a good practice to perform a build locally before deploying. Even better if you are leveraging CI/CD within your workflow, as the `predeploy` script could be extended to build and deploy to a DEV or QA environment for testing purposes before going to production.

Additionally, the `deploy` command will perform a build, and then deploy the application to your GitHub Pages site. Bear in mind this is a trigger command which should not be used lightly, please understand what you are doing and certainly know for sure before executing this one!

Finally, here are the steps to actually deploy your application.

**Build locally and test:**

```sh
$ npm run build
```

**Deploy your app to GitHub Pages:**

```sh
$ npm run deploy
```

That's it! It's really that easy! You should now see your application live at your own GitHub project page. Good Job! 🥳🎉

## Recap

Hopefully you now have some insight into working with React.js as well as what the procedure looks like to deploy a front-end application to GitHub Pages.

To summarize the steps taken to build and deploy the application:

- Configure a working development environment
- `create-react-app` a new project
- Performed some work; Iterated and refactored some more
- Spun up a local working copy of the project to test and verify work
- Deployed the application to target `gh-pages` site
- Validated the deployment was successful, and the application is functioning as intended

Not a bad way to spend a few hours on a Sunday afternoon! You now have an overview of the process to construct an application, make some changes, and deploy - all very handy skills to refine and use throughout your software development endeavors.

**Check it out here:** [todo-app](https://adamdubey.github.io/todo-app)

Thank you very much for reading!

Glad I've gotten around to working on this one, until next time...
