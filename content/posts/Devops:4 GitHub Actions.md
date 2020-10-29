---
title: "Devops:4 GitHub Actions"
date: "2020-11-1"
template: "post"
draft: false
slug: "github-actions"
category: "Devops"
tags:
  - "github"
  - "github actions"
  - "Dev Ops"
description: "Building a CI/CD pipeline using github actions"
socialImage: "/media/githubact.jpeg"
---


[GitHub Actions](https://github.com/features/actions) is a tool provided by GitHub to acheive CI/CD. Well what exactly is CI/CD? Let's go into a bit of history here, before CI/CD **(Continuous Integration and Continuous Delivery)** whenever a peice of code was ready for production, someone somewhere had to go into a machine and run specific commands to deploy it. CI/CD is a modern method in the software development cycle that reduces the repetitive process of deploying and/or testing software. There are a lot of other CI/CD tools as well like [Jenkins](https://www.jenkins.io/) or [CircleCI](https://circleci.com/) but GitHub actions is built direcly into github and hence is very easy to demonstrate.

In this post we will try to build a sample project and try to deploy it using GitHub actions.

Let's just fork [this repository](https://github.com/heroku/node-js-getting-started) and try to host it somewhere. Now there are 2 ways to do this:

1. Using the GitHub actions UI
2. Creating a file in .github/workflows directory

To create one through the UI, once you have created your repositiory on github, click on the Actions page of your repo. You will see a list of template solutions for you CI/CD like shown below.

![actions_list](/media/actions_list.png)

For simplicity let's click on Setup this workflow for **Deploy Node.js to Azure Web App**. You can choose any of the options that you like. Once you do that, you will be shown a file that you can edit/commit.

```yml
on:
  push:
    branches:
        - master

jobs:
  build-and-deploy:
    name: Build and Deploy
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - name: Use Node.js ${{ env.NODE_VERSION }}
      uses: actions/setup-node@v1
      with:
        node-version: ${{ env.NODE_VERSION }}
    - name: npm install, build, and test
      run: |
        # Build and test the project, then
        # deploy to Azure Web App.
        npm install
        npm run build --if-present
        npm run test --if-present
    - name: 'Deploy to Azure WebApp'
      uses: azure/webapps-deploy@v2
      with:
        app-name: ${{ env.AZURE_WEBAPP_NAME }}
        publish-profile: ${{ secrets.AZURE_WEBAPP_PUBLISH_PROFILE }}
        package: ${{ env.AZURE_WEBAPP_PACKAGE_PATH }}
```

You can also directly create a file in your repo and push it to your repository directly. Coming to what is happening in this above file let's take a look at each of the lines:

- **On:** The trigger for a particular workflow, this trigger can be a commit to master, so that you can deploy these commits automatically.
- **jobs:** list of configurations for the commands to run.
- **runs-on:** what type of container os should these commands run on.
- **with:** version of node/python etc. on which you want this to work with.
- **run:** list of commands to run when the above **on** trigger happens.

You can find a full list of these workflow commands [here](https://docs.github.com/en/free-pro-team@latest/actions/reference/workflow-syntax-for-github-actions)


One last thing to keep in mind is the credentials that have been mentioned in the file. You obviously don't want your secret credentials in your repository. Hence the use of secrets in the file. To add/modify these secrets you can go into Settings of your repository and add Secrets directly from the UI, which can then be accessed by the name you chose there. :)

Once this is all setup push this to your master branch and you can now see that on every merge to master branch there is a build that starts in the actions tab of your repository. It should look something like this

![actions_log.png](/media/actions_log.png)

Here you can check if your builds succeeded, failed, check the logs or even just cancel the deploy altogether.
This was CI/CD in a nutshell using GitHub Actions.



