---
title: Github Actions
tags:
  - javascript
emoji: 👋
---

### How to get started in four simple steps

```js
name;
```

#### name

The name of your workflow will be displayed on your repository’s actions page.

#### on

The events that occur on GitHub that will cause your workflow to be executed. For example, you can run your workflow on push and pull_request triggers, which will let you build your code and run your tests in a Continuous Integration workflow. You can add additional constraints on these triggers, like running when certain files or changed or when a certain branch is pushed to.

#### jobs

A list of the jobs that run as part of the workflow. Each job will run independently of the others, and will run on a different virtual environment. Jobs may have a name to make them easily identifiable in the UI or in logs. Jobs contain a set of steps that will be executed, in order. This workflow has a single job, the build job.

jobs.<job-id>.runs-on
The type of runner to use to run the given job on, either a runner provided by GitHub or a self-hosted runner that you configure. GitHub provides three main types of runners: Linux (named ubuntu-latest), Windows (named windows-latest) and macOS (named macos-latest).

jobs.<job-id>.steps
A list of the steps that will run as part of the job. Each step will run one after another, all on the same virtual environment. By default, if any step fails then the entire job will stop. In this workflow, the build job contains three steps:

The first step uses an action named actions/checkout@v2. This is an action provided by GitHub that will check out your repository onto the runner, so that it can be built and tested.
The second step uses an action named actions/setup-node@v1. This is an action provided by GitHub that will set up a particular version of Node.js on the runner. Arguments can be provided to the action in the with section; in this example, the node-version argument is set to 12, which instructs the action to put Node.js version 12 in the PATH for subsequent steps.
The final step runs programs on the command-line. By default, these programs will be run with bash (on Linux and macOS) or PowerShell (on Windows). A single command may be specified, or multiple commands can be specified by starting them with a leading pipe (|) symbol.

In this case, a Node.js continuous integration build will be performed by running npm ci to download and install packages from the npm registry, then running npm run build to run the build script specified by the project, and finally running npm test to run any unit tests in the project.

```ts

name: CI for Node.js Project
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]
jobs:
  build:
    runs-on: ubuntu-latest
    name: Build and Test
    steps:
    - uses: actions/checkout@v2
      name: Check out repository
    - uses: actions/setup-node@v1
      name: Set up Node.js
      with:
        node-version: 12
    - run: |
        npm ci
        npm run build
        npm test
      name: Build and Test

```
