# CCBCC JavaScript Code Quality Guidelines

JavaScript is a dynamic language. Many bugs in web applications and common errors come from it's lack of static typing. Now, there is a large number of tools designed to help developers write the best code they can, and the FSOP team should be using them. 

#### Why unit test?
Unit testing is very important a dynamic language in helping to catch bugs and common errors. Unit testing helps with API design and creating guarantees in your code. Decide what needs to be tested, and then write code. Writing code first then unit tests encourages developers to write tests that follow the code, rather than the other way around.

#### Why lint your code?
Using a linter helps catch common mistakes and enforce code style guidelines. Some common mistakes, such as forgetting a semi-colon, can lead to bugs that are incredibly difficult and time-consuming to track down and fix.

## Tools
### Package manager
* [npm](https://www.npmjs.com/)

### Unit testing framework
* [Jasmine](https://github.com/jasmine/jasmine)

### Task runner
* [Grunt](https://github.com/gruntjs/grunt)

### Linter
* [JSHint](https://github.com/jshint/jshint)

### E2E frameworks
* [Cucumber](https://github.com/cucumber/cucumber-js)
* [Protractor](https://github.com/angular/protractor)

---

## About npm
`npm` is the package manager for [Nodejs](https://nodejs.org/en/). All of the dependencies for the web application (i.e. front-end libraries and frameworks, grunt tasks, etc.) It's like NuGet for node. It will install one or more packages and all of the required dependencies.

`npm` also allows a user to write custom commands that can be executed via `npm run <task>`. Note that the concept of "tasks" is different between `npm` and Grunt. See the [documentation](https://docs.npmjs.com/misc/scripts) for more information, and look at the `scripts` object in `package.json`. 

---
## About Grunt

Grunt is a task runner. It will do a pre-configured task for you. Some tasks are already defined and available as plugins, and there is an API for writing custom tasks as well. 

To grunt, a task is a JavaScript tool that specializes in something, like linting, unit testing, minifying, concatenating, etc. Tasks can be a single task, or a "recipe" of multiple tasks.

#### Grunt vs. Gulp
Grunt and [Gulp](https://github.com/gulpjs/gulp) are both task runners, but they differ slightly in how they run tasks. Gulp works more like UNIX-style applications. Applications can have their output piped (`|`) into other tasks, making Gulp tasks very configurable and modular. Gulp does everything "in-memory", meaning it doesn't write any of it's temporary files to disk. 

Grunt favors configuration over composition. Tasks are configured via JSON and run sequentially. This means that task order <span id="important">**is important**<span>. While running tasks, Grunt is the opposite of Gulp. If there are any temporary files they are written to disk (this *theoretically* allows Grunt to handle larger tasks than Gulp, but in practice this doesn't make much of a difference). 

---
## WebFSOP Tasks
There are several tasks that are run against the web application, and which tasks are run depends on the environment.
* [Uglify](https://github.com/mishoo/UglifyJS2)
	* Uglify is a super cool tool that not only minifies JavaScript, but also optimizies the code.   
* [JSHint](https://github.com/jshint/jshint)
	* JSHint lints your code based on a set of directives.
* [Jasmine](https://github.com/jasmine/jasmine)
	* Jasmine is a BDD unit testing framework.
* [Watch](https://github.com/gruntjs/grunt-contrib-watch)
	* More or less a convenience tool. You tell `watch` what to watch and what to do when any of the watched files change.

* **Development**
	* Watch or
	* JSHint/Jasmine run at users discretion

* **Production**
	1. JSHint
	2. Jasmine
	3. Uglify

### Devlopment
The `watch` task wraps the `jshint` and `jasmine` tasks, and will run both of those tasks automatically whenever any of the custom JavaScript files are modified (i.e. the files in `static/js/**/*.js`).

### Production
The order of these tasks is important, as stated [above](#important).
1. Use `jshint` to check syntax. Fail if code does not meet our code standards.
2. Run unit tests with `jasmine`. Fail if any code fails a unit test. We don't want regressions in production.
3. Finally, `uglify` the code. Put the smallest, fastest code in production. 

---
## Other Tasks

Use `npm i` or `npm install` to download and install all of the necessary dependencies (grunt, grunt tasks, etc.).

Use `npm run clean` to clean up the repo. This task makes it very easy to uninstall all of the `npm` packages in VSO before the application files are copied to production. Uninstalling the packages in VSO is important because many of the packages have dependencies that break the 256-character file path limit imposed by Windows. If packages are not uninstalled before copying takes place, the VSO build will fail. 

--- 
## Other Tools

Visual Studio 2013 (and later) has support for the [Task Runner Explorer](https://visualstudiogallery.msdn.microsoft.com/8e1b4368-4afb-467a-bc13-9650572db708) extension. This tool offers a convenient interface to manage all of your tasks. It allows you to run Grunt and Gulp tasks, as well as other tasks like JS & CSS minifying and SASS compilation. 

It also allows you to bind tasks to certain events. For example, binding `jshint` to `Before Build` will lint your JavaScript files before building the solution.

Scott Hanselman has written an [introductory blog post](http://www.hanselman.com/blog/IntroducingGulpGruntBowerAndNpmSupportForVisualStudio.aspx) about this tool. 