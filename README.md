# Intro to NPM

## Objectives

- Introduce Node Package Manager (npm)
- Introduce [npm's online platform][npmjs]
- Ensure your environment is configured to use npm
- Review important concepts related to package management in JavaScript

## Introduction

JavaScript has been around for many years now, and continues to serve as a
critical part of the modern, interactive web. There are web developers all over
the world writing JavaScript code, each contributing their own bits of work.
That's _a lot_ of code! In fact, there is a lot of _duplicate_ code. Multiple
web developers, over the years, have solved the same problems over and over.

For these situations, we have JavaScript _packages_. A package is a file or set
of files full of existing, _reusable_ code. They are designed to be shared,
allowing many web developers to use the same code in their own projects.

To help organize these packages in relation to our own work, we use _npm_, or
_Node Package Manager_. In this lesson, we will be discussing how npm works and
why it is useful.

## The Value of Existing Code

While it is important that you learn the critical skills to problem solve with
code, it is equally important that we learn how to identify existing code that
suits our needs and incorporate it into our projects. We don't need to always be
_reinventing the wheel_ and writing code that may already exist.

In fact, with the amount of developers out in the world, it is likely someone
else has not only already invented the same wheel, but tested, upgraded and
innovated on it so that it is way better than anything we could write ourselves
in a short period of time.

Remember, programming is all about providing a solution to a problem. When 'on
the job', so to speak, no one gets bonus points for concocting a novel/clever
solution to a problem for which good open source code already existed.

## Setting Up Node Package Manager

Before we continue, let's make sure your environment is all set to work with
npm.

npm is automatically installed along with _Node.js_, which should already be
installed on your system if you've worked through the JavaScript coursework. To
confirm you have node installed, enter the following into your command line:

```sh
node -v
```

If a version appears, you have Node.js. If, by chance, you do not have Node.js
installed, you can use the [Node Version Manager][nvm] to install Node.js and
keep it up to date.

You can also double check npm by running the following:

```sh
npm -v
```

A version number should appear in your terminal. If you'd like, you can update
npm by entering the following:

```sh
npm install --global npm
# or, for short: npm install -g npm
```

Okay, we've got it installed. But what is npm exactly?

## NPM Introduction

As mentioned, npm is a package manager for JavaScript. This means that npm works
with your JavaScript project directories via the command line, allowing you to
install packages of preexisting code.

What sort of code? All kinds! Some packages are quite small, like
[isNumber][isnumber], a package that has one function: to check if a value is a
number. Some packages are much more complicated. Huge libraries and frameworks,
including [React][react] and [Express][expjs], are available as npm packages.
These larger packages are often _themselves_ built using a combination of other
packages.

This modular design, the ability to build a package using other packages, allows
for developers to continuously expand the JavaScript universe, creating new,
more powerful tools and applications on top of existing, tried and tested code.

## `npm install` and `package.json`

All JavaScript labs on Learn.co rely on npm packages for their tests. Many use the
`learn-browser` npm package, which is built using hundreds of supporting
packages, including the test framework, [Mocha][mocha].

The lessons themselves don't actually contain all of these packages' code.
Instead, they contain a list of _dependencies_ in a file called `package.json`.

The `package.json` file tells you (and `npm`) everything about what packages are
required for a specific JavaScript application, listing out each package name.

When we run the command `npm install` in a directory where a `package.json` file
is present, `npm` reads the names of each dependency from the `package.json`
file and downloads the packages from [npmjs.com][npmjs], where they are hosted.
It then begins installing those packages - _BUT!_ those packages also have
_their own_ `package.json` with their own dependencies! `npm` must also get
those packages, and if _those packages_ have any dependencies, get them as well.
So on and so on. This is what we refer to as a _dependency tree_.

If you are working in a local environment running `npm install` creates a folder
called `node_modules`, which contains all the downloaded packages. _Note_: the
`learn` gem may automatically run `npm install` when you fork a new lesson with
it.

When building a project from scratch, you may realize you _need_ some specific
package. We can install packages by running `npm install <package_name>` while
inside a project directory. If you do not have a correctly structured
`package.json` file, the install _will not work_!

## A Little More on `package.json`

The `package.json` file is a key part of sharing JS code repositories on sites
like GitHub. Instead of having to include all the dependencies' code with every
project, we just include a small file, listing out what npm needs to get for the
project.

The file also typically includes information about the project, such as the
name, version, author and license.

The `package.json` file is written in JSON, so like an object in JavaScript, it
is always wrapped in curly braces, and includes keys and values. A basic
example:

```json
{
	"name": "intro-to-npm-readme",
	"version": "1.0.0",
	"description": "An introduction to npm and package.json",
	"main": "index.js",
	"scripts": {
		"test": "echo 'hot dog'"
	},
	"dependencies": {
		"learn-browser": "^0.1.17"
	},
	"repository": {
		"type": "git",
		"url": "git+https://github.com/learn-co-curriculum/intro-to-npm-readme.git"
	},
	"author": "flatironschool",
	"license": "ISC",
	"bugs": {
		"url": "https://github.com/learn-co-curriculum/intro-to-npm-readme/issues"
	},
	"homepage":
		"https://github.com/learn-co-curriculum/intro-to-npm-readme#readme"
}
```

In your terminal, if you are in a directory with the above `package.json` file
present, running `npm test` will return "hot dog." This lesson actually does
include this `package.json` file, so try it for yourself!

This works because the command `npm test` is saying: "Hey npm, look in
`package.json` and find the script with the name of 'test', then execute its
value in the terminal."

Having this file present also means it is possible to install additional packages. There is one dependency already included:

```json
"dependencies": {
  "learn-browser": "^0.1.17"
}
```

Running something like `npm install react` will add a second dependency:

```json
"dependencies": {
  "learn-browser": "^0.1.17",
  "react": "^16.4.1"
}
```

Try it now! Following, take a look to see just how many dependencies (which
React relies on) have been added to your `node_modules` directory.

## `npm init`

Since npm relies on a `package.json` file, it has a built in command to _build_
`package.json` files. Running `npm init` on the command line will begin a series
of prompts, asking about specific content to include in the file. At the end, it
will create a file or edit an existing `package.json` file. Very handy when you
are creating your own projects from scratch!

#### Key Terms

- npm - Node Package Manager, a command line tool for handling packages of reusable JavaScript code
- Node - Node is a JavaScript runtime, allowing JavaScript to be run locally on your computer, instead of in a browser

## Conclusion

For all advanced JavaScript lessons, including React and Redux, we rely on npm
to set up a lot of things 'under the hood'. The applications we build are made
possible by the contributions of thousands of other coders before us!

**Remember!** While endlessly fun, programming is a means to an end: we have a
problem/our employer has a problem, and we give the computer instructions to
crush the problem. If available, open, and secure code already exists do not
hesitate to use it! Compared to physical goods, code snippets have less value
attributed to novelty (there is a reason you won't see "artisanal code" being
sold on [Etsy][etsy]).

[nvm]: https://github.com/creationix/nvm
[isnumber]: https://www.npmjs.com/package/isnumber
[react]: https://www.npmjs.com/package/react
[expjs]: https://expressjs.com/
[mocha]: https://mochajs.org/
[npmjs]: https://www.npmjs.com/
[etsy]: https://etsy.com

<p class='util--hide'>View <a href='https://learn.co/lessons/intro-to-npm-readme'>Node Package Manager</a> on Learn.co and start learning to code for free.</p>
