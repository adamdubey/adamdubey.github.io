---
layout: single
author_profile: true
title: "Deploying a React app with Github Pages"
---
A journey of building and deploying a React.js project on Github Pages.

_With a few hours to kill on a lazy Sunday afternoon..._

**NOTE:** _I haven’t included any environmental prerequisites, nor preliminary steps for setting up and building out an application to follow along, this is simply a quick reference starting “right at the action”, that being said I do hope this project encourages playing around with different deployment strategies and helping to understand why and what is involved with this particular strategy using gh-pages._

Probably one of the biggest reasons for selecting to demonstrate using Github Pages is simply because I’ve never actually tried deploying any projects other than a blog to Github Pages. So in the spirit of breaking some eggs and learning new things, here are some of my project notes that may help along the way when deploying a React.js application to Github pages.

Github Pages makes it very easy to quickly deploy a web application that only needs a front-end, which is a great medium to use if you, for example, wanted to showcase an app or two for an online web developer portfolio.

I was pleasantly surprised with just how easy it is to deploy a React application, as I’ve had more than my fair share of deploying various production applications to different platforms (ex: AWS, GCP, Azure, Private-DCs, etc) and frankly, this should be no different considering it only needs a front-end.

Now onto the fun stuff! If you’re playing along at home, please be sure you double check your own code before deploying just so you don’t have any unexpected surprises as I don’t think this qualifies as a tutorial guide :smirk:

1. Install the `gh-pages` package as a dev-dependency of your application
`npm i --save-dev gh-pages`

2. Add the following properties to the `package.json` file

* Update the `homepage` property:
```
”homepage”: “https://gitname.github.io/your-project-name”
```

* Update the `”scripts”` property to add new commands:
```
“Scripts”: {
	“Predeploy”: “npm run build”
	“Deploy”: “gh-pages -d build”
}
```

As a quick overview, the `predeploy` script  simply just builds the React application and the `deploy` script actually pushes the nicely bundled code onto your new project site page!

Once I finally finished getting the app in a decent enough state that could be deployed, I went ahead and pushed it though my own test network as a sanity check that it truly was ready for Production. This served as great practice for continuing to evolve different CI/CD strategies, as well as presented a fantastic opportunity to test out the new hardware I placed into the test network rack.

Overall, this particular project to me was more about getting the opportunity to breathe some fresh life into old projects, as well as test out some configuration changes on my test network.

**Check it out here:** [todo-app](https://adamdubey.github.io/todo-app)

Glad I've gotten around to working on this one, until next time...