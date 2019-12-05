---
layout: single
author_profile: true
title: "Deploying a React app with GitHub Pages"
---
A journey of building and deploying a React.js application with GitHub Pages.

_With a few hours to kill on a lazy Sunday afternoon..._

GitHub Pages makes it very easy to quickly deploy a web application that only needs a front-end, which is a great medium to use if you for example, wanted to showcase an app or two for an online web developer portfolio.

While you can pretty much use any front-end framework and deploy to GitHub Pages, I’ve chosen to use React.js since I wanted to recycle some old project code into this project. If you're interested in working with the same tech stack[^1] , make sure you have a _working development environment specific to your programming flavor of choice[^2]_, as well as a GitHub account.

[^1]: tech stack: OS X, React.js, Semantic UI, Git, Node.js
[^2]: YMMV on getting your own workspace setup, as there can be multiple variables with languages, packages, and operating systems to select from - if you are in doubt, please consult the [official React documentation](https://reactjs.org/). Also, if you get stuck during initial configuration, _it’s probably a configuration or package dependency_

## Working with React.js

Let me be clear about this whole write-up, it most certainly is not a tutorial. There are a vast number of tutorials and other resources out there that will serve you way better.

Instead, take this as an overview of the fundamental procedures you can take if you wanted to deploy your own project application within the outlined tech stack.

So with all that being said, let's get back on track to working with React.js

**At a 10,000’ overview:**

Create the project directory, then change to that directory

```sh
$ create-react-app myTodoApp/
$ cd myTodoApp/
```

Now it's time for some different boilerplate code

```javascript
// edit src/App.js with the following code:

// Import React and ReactDOM
import React from 'react'
import ReactDOM from 'react-dom'

// Render component into the DOM
ReactDOM.render(
<h1>My todo app</h1>,
document.getElementById('root')
);
```

Fire it up! - Run the command and then in your web browser, visit `localhost:3000`

```sh
$ npm run start
```

---

So up to this point, the following work has been performed:

- [x] Steps were taken to ensure your workspace supports working in React
- [x] `create-react-app <projectName>` will install React and all essential libraries to facilitate a basic framework that you can now use to create an application
- [x] `npm run start` builds a development copy of your application, and serves it in a web browser
- [x] When you visit `localhost:3000` in a browser, you should be able to confirm the app loads and displays something on the page

Not too bad for a high level overview! It gets you up and running with a basic outline of steps you can use to make other React specific projects.

Again there is a fair amount of information that is not being covered, so if you aren't entirely clear on the steps so far that's okay! I strongly encourage you to spend 15 minutes to explore the pieces you aren't sure about to help expand knowledge in those areas, and then return to see if your question(s) still persist - rinse and repeat as necessary.

## Extending your project

Not going to spend too much time here, just covering some high points...

I've elected to use Semantic UI mainly because of prior experience having worked with it pretty extensively in various professional projects, and with that I have accumulated a bunch of small _"feature showcase examples"_ - you know, those little micro-projects you make to demo a concept feature or some functionality to Product Management... so I've decided to recycle some of those feature code snippets into this project.

To include Semantic in your project, you'll need to first install the package and then import it in your code.

Installing Semantic UI

```sh
$ npm i semantic-ui-react --save
```

Including Semantic UI in code

```javascript
import { Button, Container, Segment, Grid, Header } from "semantic-ui-react";
```

Example of a Semantic UI button:

```javascript
<Button
    name="hamburgerbutton"
    icon="bars"
    color="blue"
    onClick={handleMenuItemClick}
/>
```

Should you fancy some documentation for [Semantic UI](https://semantic-ui.com)? 

There are some pretty sick themes you can make to have your application really stand-out with a highly polished look. If you haven't ever worked with Semantic UI before I highly encourage you to give it a go.

So that about covers the actual app development for this particular project write-up, since I mainly wanted to capture the steps to cover deployments with GitHub Pages.

## Deploying to GitHub Pages

We still need to add the facilities to be able to deploy to GitHub Pages. To achieve this, we need two things, the `gh-pages` package installed in our project workspace as well as adding a few key components to the `package.json` file.

Install the `gh-pages` as a dev-dependency package

```sh
$ npm i --save-dev gh-pages
```

Adding the `homepage` property

```json
"homepage": "https://gitname.github.io/your-project-name"
```

This is the `magic part` of using GitHub Pages to host your application. Whenever you `npm run deploy` your application it will use this information. Definitely a piece of cake!

Adding the `predeploy` and `deploy` commands

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

The `predeploy` command will just build a production copy of the application locally - it's pretty good practice to perform a build locally before deploying. Even better if you are leveraging CI/CD within your workflow, as the `predeploy` script could be extended to build and deploy to a DEV or QA environment for testing purposes before going to production.

The `deploy` command will perform a build, and then deploy the application to your GitHub Pages site. Bear in mind this is a trigger command which should not be used lightly, please understand what you're doing and know for sure before executing this one!

Finally, here are the steps to actually deploy your application.

Build locally and test:

```sh
$ npm run build
```

Deploy your app to GitHub Pages:

```sh
$ npm run deploy
```

That's it! You should now see your application live at your own GitHub project page. In regards to clean up and pushing code, it's entirely up to you and if you are utilizing any CI/CD workflows.

For context on clean up and committing, one approach you could take may look like this:

1. Build and test locally, make sure you're happy before deploying to production
2. Commit and push your code; If you're on a feature branch then open a pull request, then merge into Master
3. Deploy your application from the Master branch

And hypothetically a CI/CD workflow could follow this outline:

1. Commit hook captures your new code commit, and proceeds to do the following:
   - build
   - execute automated tests
     - if all checks and tests pass
   - deploy to a target endpoint (example: DEV, QA)
2. Once the prior step completes, and you are happy with the results, another build trigger could be a one-button `deploy master` button, in which case:
   - the new code commit is then accepted into branch `master`
   - The deployment script process triggers a deployment to production with your new changes

## Recap

Hopefully you now have some insight into working with React.js as well as what the procedure looks like to deploy a front-end application to GitHub Pages.

Here is a summary of steps taken to build and deploy:

- [x] Verified you have a working development environment
- [x] Constructed a new React.js project
- [x] Spun up a local working copy of the project
- [x] Tested and confirmed the project is working in your web browser
- [x] Deployed your application to your `gh-pages` site
- [x] Validated the deployment was successful, and your application is functioning as intended

Not a bad way to spend a few hours on a Sunday afternoon! You by now have an overview of the process to construct an application, make some changes, and deploy - all very handy skills to refine and use throughout your software development endeavours.

**Check it out here:** [todo-app](https://adamdubey.github.io/todo-app)

Glad I've gotten around to working on this one, until next time...
