# CCBCC JavaScript and Web App Unit Testing Guidelines

#### Why unit test?
Unit testing a dynamic language is very important in helping to catch bugs and common errors. 
Unit testing helps with API design and creating guarantees in your code. 
Decide what needs to be tested, and then write code. 
Writing code first then unit tests encourages developers to write tests that follow the code, rather than the other way around.

## Tools
### Package manager
* [npm](https://www.npmjs.com/)

### Unit testing framework
* [Jasmine](https://github.com/jasmine/jasmine)

### Test runner
* [Karma](https://karma-runner.github.io)

---

## About npm
`npm` is the package manager for [Node.js](https://nodejs.org/en/). 
All of the dependencies for the web application (i.e. front-end libraries and frameworks, grunt tasks, etc.).
It's like NuGet for node. It will install one or more packages and all of the required dependencies.

`npm` also allows a user to write custom commands that can be executed via `npm run <task>`. 
See the [docs](https://docs.npmjs.com/misc/scripts) for more information, and look at the `scripts` object in `package.json`. 

---

This document will focus on using [Jasmine](https://github.com/jasmine/jasmine) and [Karma](https://karma-runner.github.io) to write and run unit tests for a web application.

Karma
---

Karma is a test runner. It will start an instance  of a browser (or multiple browsers) and run your tests in the browser(s). It does not offer a framework or library for testing your code. It's simply a harness for your source and test code.


## Setup

Karma offers a convenient tool to configure a project for unit testing.
Run `karma init` from the command line and use the interactive utility to create Karma's configuration file.

### Configuring multiple browsers
Karma can be configured to run your tests in one or more browsers. 
`karma.browsers` is an array of browser names, such as `['Safari', 'Firefox', 'PhantomJS', 'Chrome', 'IE']`. 

### Running the tests
From your project directory type `karma start`. Karma will launch an instance of each browser specified in 
`karma.browsers` and report the results of the tests.

### Continuously watching files
Setting `karma.singleRun` to `false` will cause Karma to watch your files and run your tests each time a source or test file changes.
You can also pass `--single-run` on the command line to run only once.

Jasmine
---

Jasmine is a unit testing framework. It provides methods for testing assertions about your source code.


