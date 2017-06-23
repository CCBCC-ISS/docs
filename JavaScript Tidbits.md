# JavaScript and Web App Tips, Tricks, and Tidbits

Miscellaneous notes about JavaScript.

`for...in` enumerates the keys of an object

```javascript
    const arr = ['a', 'b', 'c', 'd'];
    for (let key in arr) { 
        let localVar = arr[key]; // 'key' is set to 0
        ...
    }
```

`for...of` enumerates the values of an object

```javascript
    cost arr = ['a', 'b', 'c', 'd'];
    for (const letter of arr) {
        console.log(letter); // 'letter' is set to 'a'
    }
```

There is a little-known syntax of `for...in` that can be incredibly useful and even elegant at times.

```javascript
    const myObj = {a: 1, b: 2, c: 3}; 
    let myKeys = [], 
        i = 0;
     
    for (myKeys[i++] in myObj);
     
    myKeys; // ['a','b','c'];
```

Read [this](https://javascriptweblog.wordpress.com/2011/01/04/exploring-javascript-for-in-loops/) for more information about `for...in` loops.

---
Use `npm i` or `npm install` to download and install all of the necessary dependencies (grunt, grunt tasks, etc.).

Use `npm run clean` to clean up the repo. This task makes it very easy to uninstall all of the `npm` packages in VSO before the application files are copied to production. Uninstalling the packages in VSO is important because many of the packages have dependencies that break the 256-character file path limit imposed by Windows. If packages are not uninstalled before copying takes place, the VSO build will fail. 

---

Visual Studio 2013 (and later) has support for the [Task Runner Explorer](https://visualstudiogallery.msdn.microsoft.com/8e1b4368-4afb-467a-bc13-9650572db708) extension. This tool offers a convenient interface to manage all of your tasks. It allows you to run Grunt and Gulp tasks, as well as other tasks like JS & CSS minifying and SASS compilation. 

It also allows you to bind tasks to certain events. For example, binding `jshint` to `Before Build` will lint your JavaScript files before building the solution.

Scott Hanselman has written an [introductory blog post](http://www.hanselman.com/blog/IntroducingGulpGruntBowerAndNpmSupportForVisualStudio.aspx) about this tool. 

---
## About Grunt

Grunt is a task runner. It will do a pre-configured task for you. Some tasks are already defined and available as plugins, and there is an API for writing custom tasks as well. 

To grunt, a task is a JavaScript tool that specializes in something, like linting, unit testing, minifying, concatenating, etc. Tasks can be a single task, or a "recipe" of multiple tasks.

#### Grunt vs. Gulp
Grunt and [Gulp](https://github.com/gulpjs/gulp) are both task runners, but they differ slightly in how they run tasks. Gulp works more like UNIX-style applications. Applications can have their output piped (`|`) into other tasks, making Gulp tasks very configurable and modular. Gulp does everything "in-memory", meaning it doesn't write any of it's temporary files to disk. 

Grunt favors configuration over composition. Tasks are configured via JSON and run sequentially. This means that task order <span id="important">**is important**<span>. While running tasks, Grunt is the opposite of Gulp. If there are any temporary files they are written to disk (this *theoretically* allows Grunt to handle larger tasks than Gulp, but in practice this doesn't make much of a difference). 

